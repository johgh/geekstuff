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
: ~~~javascript
    // declaration
    var surname;
    // declaration and assignment
    var name = "Tom";
    // assignment
    name = "Andy";
~~~

> Note: undeclared variables are available globally

Logic
: ~~~javascript
    15.234 === 15.234 // true
    '10' === 10 // false
~~~

Loops
: ~~~javascript
    var i = 1; while (i < 10) { alert(i); i = i + 1; }
    for (var i = 1; i < 10; i++) { ... }
    var object1 = {a: 1, b: 2}; for (var property1 in object1) { console.log(object1[property1]); }
~~~

Creating function
: ~~~javascript
    var add = function (a, b) { return a + b; };
~~~

Closures (function that returns function)
: ~~~javascript
    var add = function (a) {
        return function (b) {
            return a + b; // inner function has access to outer function variables (scoping rules)
        };
    };
    var addFive = add(5);
    alert(addFive(10));
~~~

Creating object
: ~~~javascript
    var jedi = {
    name: "Yoda",
        age: 899,
        talk: function () { alert("another... Sky... walk..."); }
    };
    // modifying object after creation
    var dog = {};
    dog.bark = function () { alert("Woof!"); };
~~~

Arrays
: ~~~javascript
    var emptyArray = [];
    var shoppingList = ['Milk', 'Bread', 'Beans'];
    shoppingList[0];
    shoppingList.length;
    shoppingList.push('A new car'); shoppingList.pop();
~~~

Defining complex data structures mixing objects and arrays
: ~~~javascript
    scales = {
        'Ionian': {'form': ['1','2','3','4','5','6','7'], 'quality': 'major'},
        'Dorian': {'form': ['1','2','♭3','4','5','6','♭7'], 'quality': 'minor'},
        'Phyrgian': {'form': ['1','♭2','♭3','4','5','♭6','♭7'], 'quality': 'minor'},
        'Lydian': {'form': ['1','2','3','♯4','5','6','7'], 'quality': 'major'},
        'Mixolydian': {'form': ['1','2','3','4','5','6','♭7'], 'quality': 'dominant'},
        'Aeolian': {'form': ['1','2','♭3','4','5','♭6','♭7'], 'quality': 'minor'},
        'Locrian': {'form': ['1','♭2','♭3','4','♭5','♭6','♭7'], 'quality': 'diminished'}
        }
~~~

Altering object
: ~~~javascript
    var arrchordsurl = {};
    arrchordsurl[id] = {};
    arrchordsurl[id].key = key;
~~~

Check if some variable is set
: ~~~javascript
    if (typeof var != 'undefined') {
~~~

String/array manipulation
: ~~~javascript
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
~~~

Math
: ~~~javascript
    // convert string to int and perform modulus
    var tonesvalue = parseInt(tones[value])%12;
~~~

isNumber
: ~~~javascript
    function isNumber(n) { return !isNaN(+n) && isFinite(n) }
~~~

Pass server side var to javascript (php)
: ~~~javascript
    var obj = <?php echo json_encode($php_variable); ?>;
~~~

# DOM

Retrieve element
: ~~~javascript
    var pageHeader = document.getElementById('page-header');
    var pageHeader = document.querySelector('#header'); // returns only one element, if multiple match selector, only the first will be returned
~~~

Retrieve NodeList (array of DOM elements)
: ~~~javascript
    document.getElementsByTagName
    document.getElementsByClassName
    var buttons = document.querySelectorAll(.btn);
~~~

DOM manipulation
: ~~~javascript
    var div = document.createElement('div');
    div.textContent = "Sup, y'all?";
    div.setAttribute('class', 'note');
    document.body.appendChild(div);

    div.parentNode.removeChild(div);
~~~

# Events

Click event
: ~~~javascript
    var handleClick = function (event) { // do something! };
    var button = document.querySelector('#big-button');
    button.addEventListener('click', handleClick);
~~~

Submit event (one-liner)
: ~~~javascript
    document.getElementById("addtask_form").addEventListener("submit", function(e){
        var jobName = document.getElementById("form_name").value;
        /* do something; */
        e.preventDefault();
    });
~~~
        
DOM loaded and ready (jQuery $(function() {...}))
: ~~~javascript
    window.addEventListener('DOMContentLoaded', function (event) {
    // do something
    };);
~~~

Page fully loaded (jQuery $(window).load(function() {...})
: ~~~javascript
    window.addEventListener('load', doSomething);
~~~

Copy text to clipboard
: ~~~javascript
    // <input type="text" value="Hello World" id="myInput">
    // <button onclick="copyToClipboard()">Copy text</button>
    function copyToClipboard() {
      var copyText = document.getElementById("myInput");
      copyText.select();
      document.execCommand("copy");
      alert("Copied the text: " + copyText.value);
    }
~~~

# Ajax and JSON

Ajax call
: ~~~javascript
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            alert(this.responseText);
        }
    };
    xhttp.open("GET", "file.txt", true);
    xhttp.send();
~~~
        
Convert js object into JSON
: ~~~javascript
    var jsonString = JSON.stringify({
        make: "McLaren",
        model: "MP4-12C",
        miles: 5023
    });
~~~

Convert string into js object 
: ~~~javascript
    var car = JSON.parse(jsonString);
    // and set property
    car.model = "P1";
~~~

# LocalStorage and sessionStorage

Store and retrieve data from sessionStorage and localStorage
: ~~~javascript
    sessionStorage.setItem('key', 'value');
    var data = sessionStorage.getItem('key');
~~~


LocalStorage and SessionStorage only saves string, use json to save objects
: ~~~javascript
    localStorage.setItem('user', JSON.stringify({
        username: 'htmldog',
        api_key: 'abc123xyz789'
    }));

    var user = JSON.parse(localStorage.getItem('user'));
~~~

Clear and removeItem from localStorage and sessionStorage
: ~~~javascript
    localStorage.clear(); localStorage.removeItem('user');
~~~

> Note: LocalStorage data doesn't expire like SessionStorage data, that only lasts while browser is open
