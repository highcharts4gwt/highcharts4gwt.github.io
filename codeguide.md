---
layout: default
title: Code Guide | Highcharts4gwt
slogan: A deeper view of the code
---

Page under construction


##Targeted audience

People willing to contribute or modify the generator or who want a deeper understanding of the code.<br/><br/>
    
In the following I will detail how the generator code works with the different steps of the algorithm. I will also explain some tricks I use at some point. I will try not to go into too much detail about the real code because I beleive code should be self explanatory and I would like this page to still be valid if the generator code is refactored.

##Step 0 : Design objectives

This generator was created with various design objectives, here they are :

#### Generated code must be a [fluent api](http://en.wikipedia.org/wiki/Fluent_interface)

{% highlight java %}
options.chart().options3d().enabled(true).alpha(15).beta(15).depth(50).viewDistance(25);
{% endhighlight %}

#### Code should be as close as possible to the Javascript API

Setter and getters do not start with 'get' and 'set'. <br/><br/>

Get the chart type

{% highlight java %}
options.chart().type();
{% endhighlight %}

Set the chart type

{% highlight java %}
options.chart().type("column");
{% endhighlight %}

#### Code must enable Junit testing ( especialy with MVP )

This is why we generate "mocks". So that in a test context you can inject mocks instead of Javascript Objects and you will still be able to test you Presenters ([MVP](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter)) in pure Junit tests. No need for GWTTestCase !

#### Code must be type safe (as much as possible)
#### Injection with GIN should be working


##Step 1 : Getting the option file

There are 2 modes available, an offline mode and an online mode. <br/><br/>

### Offline mode
The generator will fetch the highcharts json option file through the internet at the location specified inside the properties file. <br/><br/>

### Online mode
The generator will use a local file. This was designed to be able to work on the generator without an internet connexion. <br/><br/>


Once fetched, the filed is read and every option is parsed into a JSONObject. Now we can start build our tree.

##Setp 2 : Creating the tree

We need to create a tree that represents the hierarchy of options in highcharts. Once we will have this tree we will be able to go throught it and generate the corresponding java classes. We want to go from a dynamically typed language (JavaScript) to a statically typed language (Java). This has some implications in the way we have to go through the tree.


##Step 3 : Navigating the tree 


##Step 4 : Writting the classes


##Step 5 : Writting the fields