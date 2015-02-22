---
layout: post
title: Hello Complex Networks!!!
date: 2014-08-26 16:27:31
comments: true
---

I just wanted to refresh my JavaScript programming skills along with exercising my homeworks. I searched few Network Visualization JS libraries in the net I came up with VisJS. It’s pretty easy to create networks in VisJS.

{% highlight javascript %}
var nodes = new vis.DataSet();
var edges = new vis.DataSet();

var lastNodeId = 1;
// create a network
var networkContainer = document.getElementById('mynetwork');
var histogramContainer = document.getElementById('histogram');
var data = {
nodes: nodes,
edges: edges
};
var options = {};
var network = new vis.Network(networkContainer, data, options);

function addNewNode() {
nodes.add([{id: lastNodeId, label: lastNodeId.toString()}]);

if (lastNodeId != 1) {
  randomNode = Math.floor(Math.random() * (lastNodeId));
  if (randomNode != 0)
    edges.add([{from: lastNodeId, to:randomNode }]);
}
lastNodeId++;
}
{% endhighlight %}

An another quick search on google bring up FlotCharts JS library for histograms to visualize the degree distribution of nodes in a graph.

But it’s a bit tricky to extract Degree Distribution off edges dataset. One has to first create a HashMap to map degree number of nodes to occurance number of nodes in JavaScript

{% highlight javascript %}
var h = {}; 
    edges
      .get()
      .map(function(a) { 
        return a.to 
      })
      .forEach(function (b) { 
        if (typeof(h[b]) === 'undefined') 
          h[b] = 1; 
        else h[b]++; 
      });
And then again convert that to an array to be used in Flot.

var hArray = [];
    for (var o in h) {
      hArray.push([Number(o), h[o]]);
    }

    $(function() {
      $.plot("#histogram",  [hArray]);
    });
{% endhighlight %}

