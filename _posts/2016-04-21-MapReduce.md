---
layout: page
permalink: /postgres/
color: deep-purple
title:  "Postgres"
date:   2016-04-20
---

### Mongo Project

Mongo is a cross-platform document-oriented database that is classified as a NoSQL database. This makes the integration of data in some applications easier and faster. The project we focused on in this course was querying data that related to census data. Task one was finding the most distant city pairs in each country. The first step was to “map” the outcome into stacks: 

``` Python
var mapCode = function() {
   emit(this.CountryID,
     { "data":
		[
			{
				"name": this.City,
				"lat":  this.Latitude,
				"lon":  this.Longitude
			}
		]
	});
}
```

Next you have to go through those stacks and reduce them:
``` Python
var reduceCode = function(key, values) {

	var reduced = {"data":[]};
	for (var i in values) {
		var inter = values[i];
		for (var j in inter.data) {
			reduced.data.push(inter.data[j]);
		}
	}

	return reduced;
}
```
The final step is to actually query them to find the result you are searching for. 
``` Python
var finalize =  function (key, reduced) {

	if (reduced.data.length == 1) {
		return { "message" : "This Country contains only 1 City" };
	}

	var max_dist = 0;
	var city1 = { "name": "" };
	var city2 = { "name": "" };

	var c1;
	var c2;
	var d;
	for (var i in reduced.data) {
		for (var j in reduced.data) {
			if (i>=j) continue;
			c1 = reduced.data[i];
			c2 = reduced.data[j];
			d = Math.sqrt((c1.lat-c2.lat)*(c1.lat-c2.lat)+(c1.lon-c2.lon)*(c1.lon-c2.lon));
			if (d > max_dist && d > 0) {
				max_dist = d;
				city1 = c1;
				city2 = c2;
			}
		}
	}

	return {"city1": city1.name , "city2": city2.name, "dist": max_dist + "	is farthest"};
}
```
This will return the two closest cities. 
