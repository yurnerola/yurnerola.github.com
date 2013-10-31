---
layout: post
title: "Factory Pattern"
description: ""
category: "Design Pattern"
tags: [Design Pattern]
---
{% include JB/setup %}


###Content:

 - Simple Factory
 - Factory Method
 - Abstract Factory

###Create an instance of class

Yes.U can user new.And it's so easy that mom need not to worry about i don't know how to do it.But why Factory pattern?

Let’s say you have a pizza shop, and as a cutting-edge pizza store owner in Objectville you might end up writing some code like this:

{% highlight java %}
public Pizza orderPizza(String type){

	pizza = new Pizza();

	pizza.prepare();
	pizza.bake();
	pizza.cut();
	pizza.box();
	return pizza;
}

{% endhighlight %}

But you need more than one type of pizza...

{% highlight java %}
public Pizza orderPizza(String type){

	if (type.equals("cheese")) {
		pizza = new CheesePizza();
	} else if (type.equals("pepperoni")) {
		pizza = new PepperoniPizza();
	}

	pizza.prepare();
	pizza.bake();
	pizza.cut();
	pizza.box();
	return pizza;
}

{% endhighlight %}


But the pressure is on to add more pizza types…


{% highlight java %}

public class SimplePizzaFactory {

	public Pizza createPizza(String type) {
		Pizza pizza = null;

		if (type.equals("cheese")) {
			pizza = new CheesePizza();
		} else if (type.equals("pepperoni")) {
			pizza = new PepperoniPizza();
		} else if (type.equals("clam")) {
			pizza = new ClamPizza();
		} else if (type.equals("veggie")) {
			pizza = new VeggiePizza();
		}
		return pizza;
	}
}

public class PizzaStore {
	SimplePizzaFactory factory;
 
	public PizzaStore(SimplePizzaFactory factory) { 
		this.factory = factory;
	}
 
	public Pizza orderPizza(String type) {
		Pizza pizza;
 
		pizza = factory.createPizza(type);
 
		pizza.prepare();
		pizza.bake();
		pizza.cut();
		pizza.box();

		return pizza;
	}
}

{% endhighlight %}

Franchising the pizza store with regional differences

{% highlight java %}
public class NYPizzaStore extends PizzaStore {

	Pizza createPizza(String item) {
		if (item.equals("cheese")) {
			return new NYStyleCheesePizza();
		} else if (item.equals("veggie")) {
			return new NYStyleVeggiePizza();
		} else if (item.equals("clam")) {
			return new NYStyleClamPizza();
		} else if (item.equals("pepperoni")) {
			return new NYStylePepperoniPizza();
		} else return null;
	}
}

public abstract class PizzaStore {
 
	abstract Pizza createPizza(String item);
 
	public Pizza orderPizza(String type) {
		Pizza pizza = createPizza(type);
	
		pizza.prepare();
       	. . . 
		return pizza;
	}
}

{% endhighlight %}

![enter image description here][1]


###Factory Method Pattern Definition

>The Factory Method Pattern defines an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.


![enter image description here][2]

###Abstract Factory

>Provides an interface for creating families of related or dependent objects without specifying their concrete classes.



  [1]: http://yurnerola.github.io/img/factory%20pattern.png
  [2]: http://yurnerola.github.io/img/abstract%20factory.png