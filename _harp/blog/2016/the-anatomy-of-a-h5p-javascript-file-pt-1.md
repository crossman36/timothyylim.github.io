### the anatomy of a h5p javascript file pt 1

For someone pretty new to javascript, the code structure of a h5p javascript file took me a bit of time to get my head around. Essentially, it can broken down to the following components:

1. 'constructor function' which creates the H5P object

2. 'attach function' which attaches the content defined in the constructor to the page

The code skeleton looks like this:

```
var H5P = H5P || {};
 
H5P.GreetingCard = (function ($) {
  /**
   * Constructor function.
   */
  function C(options, id) {
    // Extend defaults with provided options
  };
 
  /**
   * Attach function called by H5P framework to insert H5P content into
   * page
   *
   * @param {jQuery} $container
   */
  C.prototype.attach = function ($container) {
  };
  
  return C;
})(H5P.jQuery);
```

Let's build the [hello world tutorial](https://h5p.org/tutorial-greeting-card) but without the image for the sake of simplicity. 

To create a greeting of 'Hello world!' we need to extend the constructor of the H5P object so that it is created with some text:

```
  function C(options, id) {
    // Extend defaults with provided options
    this.options = $.extend(true, {}, {
      greeting: 'Hello world!'
    }, options);
    
    this.id = id;
  };
```

This simply allows the object to extend its options to now have a greeting attribute (it doesn't have to be called greeting) as 'Hello world!'. 

Next, we have to attach the text to the page itself. The H5P framework interacts with the page by giving the page a container that will be displayed to user. We can put things into this container by adding to our attach function we defined earlier:

```
  /**
   * Attach function called by H5P framework to insert H5P content into
   * page
   *
   * @param {jQuery} $container
   */

  C.prototype.attach = function ($container) {
    // Set class on container to identify it as a greeting card
    // container.  Allows for styling later.
    $container.addClass("h5p-greetingcard");
    
    // Add greeting text.
    $container.append('<div class="greeting-text">' + this.options.greeting + '</div>');
  };
```

This creates a new div on the page which is populated by the text we defined earlier in 'this.options.greeting'. 

We can go back over the file to add an image if we want to. The final result would look something like this:

```
var H5P = H5P || {};
 
H5P.GreetingCard = (function ($) {
  /**
   * Constructor function.
   */
  function C(options, id) {
    // Extend defaults with provided options
    this.options = $.extend(true, {}, {
      greeting: 'Hello world!',
      image: null
    }, options);
    // Keep provided id.
    this.id = id;
  };
 
  /**
   * Attach function called by H5P framework to insert H5P content into
   * page
   *
   * @param {jQuery} $container
   */
  C.prototype.attach = function ($container) {
    // Set class on container to identify it as a greeting card
    // container.  Allows for styling later.
    $container.addClass("h5p-greetingcard");
    // Add image if provided.
    if (this.options.image && this.options.image.path) {
      $container.append('<img class="greeting-image" src="' + H5P.getPath(this.options.image.path, this.id) + '">');
    }
    // Add greeting text.
    $container.append('<div class="greeting-text">' + this.options.greeting + '</div>');
  };
 
  return C;
})(H5P.jQuery);
```
