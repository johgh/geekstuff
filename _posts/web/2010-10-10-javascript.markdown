---
layout: post
title:  "Javascript"
permalink:  "javascript"
date:   2015-07-25 16:30:15
category: WebDev
tags: Web
---

> For a full javascript reference, see: [w3schools.com/jsref](https://www.w3schools.com/jsref/)

# Basic

Declaration / initialization / assignment
: {% highlight javascript %}
    // declaration
    var surname;
    // declaration and assignment
    var name = "Tom";
    // assignment
    name = "Andy";
{% endhighlight %}

> Note: undeclared variables are available globally

Logic
: {% highlight javascript %}
    15.234 === 15.234 // true
    '10' === 10 // false
{% endhighlight %}

Loops
: {% highlight javascript %}
    var i = 1; while (i < 10) { alert(i); i = i + 1; }
    for (var i = 1; i < 10; i++) { ... }
    var object1 = {a: 1, b: 2}; for (var property1 in object1) { console.log(object1[property1]); }
{% endhighlight %}

Creating function
: {% highlight javascript %}
    var add = function (a, b) { return a + b; };
{% endhighlight %}

Closures (function that returns function)
: {% highlight javascript %}
    var add = function (a) {
        return function (b) {
            return a + b; // inner function has access to outer function variables (scoping rules)
        };
    };
    var addFive = add(5);
    alert(addFive(10));
{% endhighlight %}

Creating object
: {% highlight javascript %}
    var jedi = {
    name: "Yoda",
        age: 899,
        talk: function () { alert("another... Sky... walk..."); }
    };
    // modifying object after creation
    var dog = {};
    dog.bark = function () { alert("Woof!"); };
{% endhighlight %}

Arrays
: {% highlight javascript %}
    var emptyArray = [];
    var shoppingList = ['Milk', 'Bread', 'Beans'];
    shoppingList[0];
    shoppingList.length;
    shoppingList.push('A new car'); shoppingList.pop();
{% endhighlight %}

Defining complex data structures mixing objects and arrays
: {% highlight javascript %}
    scales = {
        'Ionian': {'form': ['1','2','3','4','5','6','7'], 'quality': 'major'},
        'Dorian': {'form': ['1','2','♭3','4','5','6','♭7'], 'quality': 'minor'},
        'Phyrgian': {'form': ['1','♭2','♭3','4','5','♭6','♭7'], 'quality': 'minor'},
        'Lydian': {'form': ['1','2','3','♯4','5','6','7'], 'quality': 'major'},
        'Mixolydian': {'form': ['1','2','3','4','5','6','♭7'], 'quality': 'dominant'},
        'Aeolian': {'form': ['1','2','♭3','4','5','♭6','♭7'], 'quality': 'minor'},
        'Locrian': {'form': ['1','♭2','♭3','4','♭5','♭6','♭7'], 'quality': 'diminished'}
        }
{% endhighlight %}

Altering object
: {% highlight javascript %}
    var arrchordsurl = {};
    arrchordsurl[id] = {};
    arrchordsurl[id].key = key;
{% endhighlight %}

Check if some variable is set
: {% highlight javascript %}
    if (typeof var != 'undefined') {
{% endhighlight %}

String/array manipulation
: {% highlight javascript %}
    // replace function converts text to "something and something"
    var text = "Everything and nothing.";
    text = text.replace(/(every|no)thing/gi, "something");
    // split function
    var arrFingers = result.fing.split(/[ ,]+/);
    var currentPage = window.location.pathname.split(".")[0].split("/")[1]
    // join array into string
    var tonesJoin = extraData.fretTones.join();
    // normalize string (no accents, etc)
    str.normalize('NFD').replace(/[\u0300-\u036f]/g, "").toLowerCase();
{% endhighlight %}

Math
: {% highlight javascript %}
    // convert string to int and perform modulus
    var tonesvalue = parseInt(tones[value])%12;
{% endhighlight %}

isNumber
: {% highlight javascript %}
    function isNumber(n) { return !isNaN(+n) && isFinite(n) }
{% endhighlight %}

Pass server side var to javascript (php)
: {% highlight javascript %}
    var obj = <?php echo json_encode($php_variable); ?>;
{% endhighlight %}

# DOM

Retrieve element
: {% highlight javascript %}
    var pageHeader = document.getElementById('page-header');
    var pageHeader = document.querySelector('#header'); // returns only one element, if multiple match selector, only the first will be returned
{% endhighlight %}

Retrieve NodeList (array of DOM elements)
: {% highlight javascript %}
    document.getElementsByTagName
    document.getElementsByClassName
    var buttons = document.querySelectorAll(.btn);
{% endhighlight %}

DOM manipulation
: {% highlight javascript %}
    var div = document.createElement('div');
    div.textContent = "Sup, y'all?";
    div.setAttribute('class', 'note');
    document.body.appendChild(div);

    div.parentNode.removeChild(div);
{% endhighlight %}

# Events

Click event
: {% highlight javascript %}
    var handleClick = function (event) { // do something! };
    var button = document.querySelector('#big-button');
    button.addEventListener('click', handleClick);
{% endhighlight %}

Submit event (one-liner)
: {% highlight javascript %}
    document.getElementById("addtask_form").addEventListener("submit", function(e){
        var jobName = document.getElementById("form_name").value;
        /* do something; */
        e.preventDefault();
    });
{% endhighlight %}
        
DOM loaded and ready (jQuery $(function() {...}))
: {% highlight javascript %}
    window.addEventListener('DOMContentLoaded', function (event) {
    // do something
    };);
{% endhighlight %}

Page fully loaded (jQuery $(window).load(function() {...})
: {% highlight javascript %}
    window.addEventListener('load', doSomething);
{% endhighlight %}

# Ajax and JSON

Ajax call
: {% highlight javascript %}
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            alert(this.responseText);
        }
    };
    xhttp.open("GET", "file.txt", true);
    xhttp.send();
{% endhighlight %}
        
Convert js object into JSON
: {% highlight javascript %}
    var jsonString = JSON.stringify({
        make: "McLaren",
        model: "MP4-12C",
        miles: 5023
    });
{% endhighlight %}

Convert string into js object 
: {% highlight javascript %}
    var car = JSON.parse(jsonString);
    // and set property
    car.model = "P1";
{% endhighlight %}

# LocalStorage and sessionStorage

Store and retrieve data from sessionStorage and localStorage
: {% highlight javascript %}
    sessionStorage.setItem('key', 'value');
    var data = sessionStorage.getItem('key');
{% endhighlight %}


LocalStorage and SessionStorage only saves string, use json to save objects
: {% highlight javascript %}
    localStorage.setItem('user', JSON.stringify({
        username: 'htmldog',
        api_key: 'abc123xyz789'
    }));

    var user = JSON.parse(localStorage.getItem('user'));
{% endhighlight %}

Clear and removeItem from localStorage and sessionStorage
: {% highlight javascript %}
    localStorage.clear(); localStorage.removeItem('user');
{% endhighlight %}

> Note: LocalStorage data doesn't expire like SessionStorage data, that only lasts while browser is open
