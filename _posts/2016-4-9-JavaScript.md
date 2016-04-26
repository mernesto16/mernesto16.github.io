---
layout: page
title: JavaScript
permalink: /JavaScript/
---

JavaScirpt was pretty hard for me to grasp this semester. One of the problems I found was that it was to forgiving of a scripting language. By this I mean that it would allow functions to run even if they weren’t written as well as they could be. This would cause confusion and also slow down processing speeds. The main way we used JavaScript this semester was when creating a login in ability to a website. The most confusing Java Script code that I developed was the one for searching for something specified by a user. 

### Examples 

```Python 
    
    $scope.search = function search(){
        console.log('Searching', $scope.find)
        socket.emit('search', $scope.find);
        $scope.find = '';
        console.log('Found:', $scope.find )
    }

```
This allowed a user to search based on pre-specified requirements. 

### Helful Links

There were some links that I found helpful when trying to understand JavaScript. These included 
http://www.w3schools.com/js/

https://www.javascript.com

https://flask-socketio.readthedocs.org/en/latest/


