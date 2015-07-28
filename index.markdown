---
layout: index
title: Highcharts4gwt
---

<div class="jumbotron">
  <h1><img src="/images/h4gwt.png" width="80px"></img>Highcharts4gwt</h1>
  <h4>An always "up to date" GWT wrapper for highcharts</h4>
</div>

<div class="major-links">
    <a href="{{site.github_page}}"><i class="fa fa-github"></i><span >Github repositories</span></a>&nbsp;&nbsp;
    <a href="{{site.demo_page}}"><span ><img src="/images/gcp-logo.png" width="37px"></img>Demo on App Engine</span></a>
    
    <a href="https://groups.google.com/forum/#!forum/highcharts4gwt"><img src="/images/my-groups-color.png" width="50px"/>Highcharts4gwt google group</a><br/>
    <a href='https://pledgie.com/campaigns/27871'><img alt='Click here to lend your support to: highcharts4gwt and make a donation at pledgie.com !' src='https://pledgie.com/campaigns/27871.png?skin_name=chrome' border='0' ></a>
</div>




<br/>

To know more about Highcharts please have a look to [highcharts web page](http://www.highcharts.com/products/highcharts)

## How to use it (with maven) ?

* Update your `pom.xml`

{% highlight xml %}
<dependency>
    <groupId>com.github.highcharts4gwt</groupId>
    <artifactId>highcharts</artifactId>
    <version>{{site.project_version}}</version>
</dependency>
{% endhighlight %}

{% highlight xml %}
<build>
	<plugins>
		...
		<!-- GWT Maven Plugin -->
		<plugin>
			...
			<artifactId>gwt-maven-plugin</artifactId>
			<configuration>
				...
				<compileSourcesArtifacts>
					<artifact>com.github.highcharts4gwt:highcharts</artifact>
				</compileSourcesArtifacts>
			</configuration>
		</plugin> 
	</plugins>
</build>
{% endhighlight %}

* Update your `app.gwt.xml`

{% highlight xml %}
<inherits name='com.github.highcharts4gwt.highcharts' />
{% endhighlight %}

* Update your `app.html`

{% highlight xml %}
<script type="text/javascript" src="js/jquery/jquery-1.11.0.min.js"></script>
<script type="text/javascript" src="http://code.highcharts.com/highcharts.js"></script>
<script type="text/javascript" src="http://code.highcharts.com/highcharts-3d.js"></script>
<script type="text/javascript" src="http://code.highcharts.com/highcharts-more.js"></script>
{% endhighlight %}

You can have a look at the [testproject](https://github.com/highcharts4gwt/testproject) for a working example.
<br/>

## What does it look like in GWT ?

Have a look to the <a href="{{site.demo_page}}"><span ><img src="/images/gcp-logo.png" width="37px"></img>demo on App Engine</span></a> you will find java code examples.

The goal was to write an API that was as close as possible to the JavaScript API so that by reading any example in JavaScript it would be easy to write it in GWT. To do that we use a fluent API. Here is what it looks like to create some chart options (GIN injection not used yet). You can see that the ChartOptions is a pure Java object and that there is no link at all with any widget.<br/><br/>

{% highlight java %}

public void onModuleLoad()
{

    HighchartsLayoutPanel highchartsLayoutPanel = new HighchartsLayoutPanel();

    //This should be injected by GIN, here as a simple example
    HighchartsOptionFactory highchartsFactory = new JsoHighchartsOptionFactory();

    RootLayoutPanel.get().add(highchartsLayoutPanel);

    ChartOptions options = highchartsFactory.createChartOptions();
    options.chart().type("column");
    options.chart().margin().push(75);
    options.chart().options3d().enabled(true).alpha(15).beta(15).depth(50).viewDistance(25);

    options.title().text("Chart rotation demo");
    options.subtitle().text("Test options by dragging the sliders below");

    options.plotOptions().column().depth(25);

    SeriesColumn series = highchartsFactory.createSeriesColumn();

    ArrayNumber data = series.dataAsArrayNumber();
    data.push(29.9);
    data.push(71.5);
    data.push(106.4);
    data.push(129.2);
    data.push(144.0);
    data.push(176.0);
    data.push(135.6);
    data.push(148.5);
    data.push(216.4);
    data.push(194.1);
    data.push(95.6);
    data.push(54.4);

    //Event callback
    series.addClickHandler(new ClickHandler()
    {
        @Override
        public void onClick(ClickEvent clickEvent)
        {
            Window.alert("The series has been clicked");
        }
    });

    //Function callback
    series.tooltip().pointFormatter(new PointFormatterCallback()
    {
        
        @Override
        public String onCallback(Point Point)
        {
            String value = "Custom point tooltip, point " + Point.categoryAsString() + ", value: " +  Point.y();
            return value;
        }
    });

    options.series().addToEnd(series);

    // To set a function as string if needed (formatter case with no context object)
    String function = "function () " +
        "{" +
            "return 'The value for <b>' + this.x +'</b> is <b>' + this.y + '</b>';"+
        "}";
        
    options.tooltip().setFunctionAsString("formatter", function);

    //To set a field if no typed setter is available
    options.setFieldAsJsonObject("colorAxis", "{ \"minColor\" : \"#FFFFFF\", \"maxColor\" : \"#7cb5ec\"}");

    highchartsLayoutPanel.renderChart(options);
}

{% endhighlight %}

## How can it be always up to date ? 

This wrapper is generated using the JSON file that describes highcharts options. This is the same file that is used by highcharts to generate its documentation. We parse this file, then we generate the JSNI code for getter and setters method.

## Why not using moxie wrapper ?

I have used moxie wrapper both for personal and professional projects. It works fine. Thanks a lot to them, it saved me lots of time ! But their wrapper does not seemed to be maintained anymore, plus I disagree with some of their design choices.<br/><br/>

To know more about [moxiegroup](http://www.moxiegroup.com/) and their highcharts wrapper [http://www.moxiegroup.com/moxieapps/gwt-highcharts/](http://www.moxiegroup.com/moxieapps/gwt-highcharts/), have a look to the sources of that project that can be found on [sourceforge](http://sourceforge.net/projects/gwt-highcharts/) 

