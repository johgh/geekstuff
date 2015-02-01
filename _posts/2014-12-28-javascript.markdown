---
layout: post
title:  "Javascript"
permalink:  "javascript"
date:   2014-12-28 16:30:15
category: Web
---
Arrays/objects iteration
: 
{% highlight javascript %}
$.each([ 52, 97 ], function( index, value ) {
    alert( index + ": " + value ); 
});
{% endhighlight %}

Debug
: 
{% highlight javascript %}
console.log(bla.toSource());
{% endhighlight %}

Prototyped function
: 
{% highlight javascript %}
$.fn.myExtension = function(){
    var currentjQueryObject = this;
    //work with currentObject
    return this; //you can include this if you would like to support chaining
};
{% endhighlight %}

Ternary logic, length, filter, prop...
: 
{% highlight javascript %}
function checkRoot(parent){
    child = ((parent == 'js-r-0') ? '.js-sections-read' : '.js-sections-write');
    var totalChilds = $(child + "[id!='" + parent + "']").length;
    var value = ($(child + "[id!='" + parent + "']").filter(':checked').length == totalChilds);
    $('#' + parent).prop('checked', value);
}
{% endhighlight %}

"live" event
: 
{% highlight javascript %}
$(document).on('click', '.js-changePage', function() {
});
{% endhighlight %}

$.param + serialize
: 
{% highlight javascript %}
vars = {};
vars.insert_event = 1;
vars.arr_sched = arr_sched;
varsForm = $("#form_add").serialize();
vars = $.param(vars) + '&' + varsForm
{% endhighlight %}

Radio button value
: 
{% highlight javascript %}
$('input[name="genderS"]:checked').val();
{% endhighlight %}

