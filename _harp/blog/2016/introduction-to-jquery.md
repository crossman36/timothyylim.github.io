### introduction to jquery

*the following examples are loosely based on the tutorials at [try.jquery.com](try.jquery.com)*

**selecting elements**

The point of jquery is to lend interactivity to a web page. The first step in that process is the selection of HTML elements. Let's start with the following example

```
<html>
<head>
<title>jQuery Hello World</title>

<!--include jquery library here --> 
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script>

</head>
<body>
  <h2>My header</h2>
  <p>Let's change this text: <span>change me!</span></p>
</body>
</html>
```

To select h2, it's as simple as typing the following into the console

```
$("h2")
```
If there were more than one h2's this command would select all of them. By the way, the '$' is just a shorthand for 'jQuery'. 

Now let's select the span and then the text value contained within that span

```
$("span").text()
```

We can change the value of the span 

```
$("span").text("changed!")
```

Just to be safe, we need to make sure that the page is loaded before we execute any javascript.

```
$(document).ready(function() {
  $("span").text("changed!");
});
```

**modifying multiple elements**

Taking a slightly more complicated example

```
<div id="vacations-wrapper">
 <h1>Vacation Packages</h1>
 <ul id="vacations">
   <li class="vacation america">
     <h2>San Francisco, California</h2>
     <span class="details">$700</span>
   </li>
   <li class="vacation america">
     <h2>Washington DC, District of Columbia</h2>
     <span class="details">$400</span>
   </li>
   <li class="vacation europe">
     <h2>London, England</h2>
     <span class="details">$1,100</span>
   </li>
 </ul>
</div>
```

We can select and change all the h2 elements 

```
<script type="text/javascript">

$(document).ready(function(){
  $("h2").text("Orlando, FL")
});

</script>
```

Or we can select by id

```
$("#vacations")
```

Or by class

```
$(".america")
```

[codepen](http://codepen.io/tctt23/pen/XdevPz)
