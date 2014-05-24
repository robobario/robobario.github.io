---
layout: post
title:  "Dependency Injection in Fitnesse"
date:   2014-05-24 17:54:35
categories: fitnesse
---

I work with a big suite of fitnesse tests. In this suite most of our tests retrieve services from a spring context. This is done in the most awkward way, with static fields that request beans like so: 

{% highlight java %}
private static TestService service = FitnesseContext.getBean(TestService.class);
{% endhighlight %}

This is painful because you can be sure our massive spring context is going to be loaded whenever you instantiate a test fixture. These fixtures are unit tested and the current workaround is to use jmockit to stop the context load. We have sinned.

Our goal is to make our fixtures simpler and testable without jmockit. We would prefer spring to inject services into the fixtures. My first attempt was just using the BeanFactory to autowire the fixtures. So in the constructor you would call a method like:

{% highlight java %}
FitnesseContext.inject(this);
{% endhighlight %}

{% highlight java %}
public static void inject(Object obj) {
    ctx.getBeanFactory().autowireBean(obj);
}
{% endhighlight %}

This reduces the calls to FitnesseContext right down and you can then think about doing some dirty hack to avoid calling this method on construct. An alternate constructor or overriding a protected method.

Naturally you also want to avoid adding this cruft to every test fixture, it would be nicer if slim could handle injection for you. I wanted to modify slim to do the injection but as it turns out you can already do it. You do need to depend on fitnesse's not-so-small jar but in our case we already do so that we can register custom converters.

The slim service has a parameter interactionClass, this class is something like a strategy for instantiation and method execution. It's interface is: 

{% highlight java %}
public interface FixtureInteraction {
  Object newInstance(Constructor<?> constructor, Object... initargs);
  Object methodInvoke(Method method, Object instance, Object... convertedArgs);
}
{% endhighlight %}

You can pass in a fully qualified classname to choose a different implementation, it must extend DefaultInteraction. So a dumb injecting interaction would look like:

{% highlight java %}
public class InjectingInteraction extends DefaultInteraction{
  @Override
  public Object newInstance(Constructor<?> constructor, Object... initargs) {
    Object o = super.newInstance(constructor, initargs);
    FitnesseContext.inject(o);
    return o;
  }

  @Override
  public Object methodInvoke(Method method, Object instance, Object... convertedArgs) {
    return super.methodInvoke(method, instance, convertedArgs);
  }
}
{% endhighlight %}

Then you change the slim command to pass through the name of this class and it's all go.
{% highlight bash %}
java ... slimcommand stuff ... -i org.your.path.InjectingInteraction
{% endhighlight %}
