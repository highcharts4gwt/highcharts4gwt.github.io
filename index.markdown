---
layout: index
title: Highcharts4gwt
---

<div class="jumbotron">
  <h1><img src="/images/h4gwt.png" width="80px"></img>Highcharts wrapper for GWT</h1>
  <h4>An always "up to date" GWT wrapper for highcharts</h4>
</div>

<div class="major-links">
    <a href="{{site.github_page}}"><i class="fa fa-github"></i><span >{{site.project_name}}</span></a>&nbsp;&nbsp;
    <a href="{{site.demo_page}}"><span ><img src="/images/gcp-logo.png" width="37px"></img>Demo on App Engine</span></a>
</div>

<br/>

To know more about Highcharts please have a look to [highcharts web page](http://www.highcharts.com/products/highcharts)


##How can it be always up to date ? 

This wrapper is generated using the JSON file that describes highcharts options. This is the same file that is used by highcharts to generate its documentation. We parse this file, then we generate the JSNI code for getter and setters method.

##What does it look like in GWT ?

The goal was to write an API that was as close as possible to the JavaScript API so that by reading any example in JavaScript it would be easy to write it in GWT. To do that we use a fluent API. Here is what it looks like to create some chart options (GIN injection not used yet). You can see that the ChartOptions is a pure Java object and that there is no link at all with any widget.<br/><br/>


    ChartOptions options = (ChartOptions) JavaScriptObject.createObject();
     
    options.chart().type("column");
    options.chart().margin().push(75);
    options.chart().options3d().enabled(true).alpha(15).beta(15).depth(50).viewDistance(25);

    options.subtitle().text("Subtitle 3D");
    options.title().text("Title 3D");

    options.plotOptions().column().depth(25);

    Series series = (Series) JavaScriptObject.createObject();

    ArrayNumber data = series.data();
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

    options.series().addToEnd(series);


##Why not using moxie wrapper ?

I have used moxie wrapper both for personal and professional projects. It works fine. Thanks a lot to them, it saved me lots of time ! But their wrapper does not seemed to be maintained anymore, plus I disagree with some of their design choices.<br/><br/>

To know more about [moxiegroup](http://www.moxiegroup.com/) and their highcharts wrapper [http://www.moxiegroup.com/moxieapps/gwt-highcharts/](http://www.moxiegroup.com/moxieapps/gwt-highcharts/), have a look to the sources of that project that can be found on [sourceforge](http://sourceforge.net/projects/gwt-highcharts/) 


## Status
Still in development.<br/><br/>

Go to the [highcharts](https://github.com/highcharts4gwt/highcharts) repository to download the wrapper sources and test the wrapper. You can have a look to the [demo website]({{site.demo_page}}).<br/><br/>

The [highcharts](https://github.com/highcharts4gwt/highcharts) repository is were I put all the highcharts chart options. It is cleaner so that the chart options are not mixed with the generator code. You can use that project to test the api in your gwt project.<br/><br/>

See the project readme for more info on how to use it.
