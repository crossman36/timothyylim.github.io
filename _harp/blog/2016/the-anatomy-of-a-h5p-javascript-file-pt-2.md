### the anatomy of a h5p javascript file pt 2

To get a better understanding of H5P we will build the javascript file from the ground up for the example called "Guess the Answer":

<iframe src="https://h5p.org/h5p/embed/2398" width="618" height="388" frameborder="0" allowfullscreen="allowfullscreen"></iframe><script src="https://h5p.org/sites/all/modules/h5p/library/js/h5p-resizer.js" charset="UTF-8"></script>

Start with the skeleton as we did in [pt 1](http://timothyylim.github.io/blog/2016/the-anatomy-of-a-h5p-javascript-file-pt-1):

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

From the example we know we need the following:

* a question (taskDescription)
* an image (solutionImage)
* a button (solutionLabel)
* a solution (solutionText)

We can add this to the constructor

```
  /**
   * Constructor function.
   */
  function C(params, id) {
    // Extend defaults with provided options
    this.params = $.extend({}, {
      taskDescription: '',
      solutionLabel: 'Click to see the answer.',
      solutionImage: null,
      solutionText: ''
    }, params);

	// Keep provided ID
    this.$ = $(this);
    this.id = id;

  }

```

Insert H5P object into the page with the attach function

```
  /**
   * Attach function called by H5P framework to insert H5P content into page.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.attach = function ($container) {
    this.setActivityStarted();
    this.$inner = $container.addClass('h5p-guess-answer')
      .html('<div></div>')
      .children();

    //Attach task description, if provided.
    this.addTaskDescriptionTo(this.$inner);

    //Attach image, if provided.
    this.addImageTo(this.$inner);

    //Attach solution container.
    this.addSolutionContainerTo(this.$inner);
  };
```

Finally, create seperate divs for each of the parameters we defined in the constructor

```
  /**
   * Adds a task description if provided in semantics, to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addTaskDescriptionTo = function ($container) {
    if (this.params.taskDescription) {
      $('<div/>', {
        'class': 'h5p-guess-answer-title',
        html: this.params.taskDescription
      }).appendTo($container);
    }
  };

  /**
   * Adds image to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addImageTo = function ($container) {
    var self = this;

    if (self.params.solutionImage && self.params.solutionImage.path) {
      var $imageHolder = $('<div/>', {
        'class': 'h5p-guess-answer-image-container'
      }).append($('<img/>', {
        'class': 'h5p-guess-answer-image',
        src: H5P.getPath(self.params.solutionImage.path, self.id),
        load: function () {
          self.trigger('resize');
        }
      }));

      $imageHolder.appendTo($container);
    }
  };

  /**
   * Adds a solution container to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addSolutionContainerTo = function ($container) {
    var self = this;

    self.$solutionContainer = $('<div/>', {
      'class': 'h5p-guess-answer-solution-container',
      html: this.params.solutionLabel
    }).click(function () {
      $(this).addClass('h5p-guess-answer-showing-solution').html(self.params.solutionText);
      self.trigger('resize');
    }).appendTo($container);
  };
```

The final file would look like this

```
var H5P = H5P || {};

/**
 * Guess the answer module
 * @external {jQuery} $ H5P.jQuery
 */
H5P.GuessTheAnswer = (function ($) {
  /**
   * Constructor function.
   */
  function C(params, id) {
    // Extend defaults with provided options
    this.params = $.extend({}, {
      taskDescription: '',
      solutionLabel: 'Click to see the answer.',
      solutionImage: null,
      solutionText: ''
    }, params);

    // Keep provided ID
    this.$ = $(this);
    this.id = id;

  }
  /**
   * Attach function called by H5P framework to insert H5P content into page.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.attach = function ($container) {
    this.setActivityStarted();
    this.$inner = $container.addClass('h5p-guess-answer')
      .html('<div></div>')
      .children();

    //Attach task description, if provided.
    this.addTaskDescriptionTo(this.$inner);

    //Attach image, if provided.
    this.addImageTo(this.$inner);

    //Attach solution container.
    this.addSolutionContainerTo(this.$inner);
  };

  /**
   * Adds a task description if provided in semantics, to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addTaskDescriptionTo = function ($container) {
    if (this.params.taskDescription) {
      $('<div/>', {
        'class': 'h5p-guess-answer-title',
        html: this.params.taskDescription
      }).appendTo($container);
    }
  };

  /**
   * Adds image to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addImageTo = function ($container) {
    var self = this;

    if (self.params.solutionImage && self.params.solutionImage.path) {
      var $imageHolder = $('<div/>', {
        'class': 'h5p-guess-answer-image-container'
      }).append($('<img/>', {
        'class': 'h5p-guess-answer-image',
        src: H5P.getPath(self.params.solutionImage.path, self.id),
        load: function () {
          self.trigger('resize');
        }
      }));

      $imageHolder.appendTo($container);
    }
  };

  /**
   * Adds a solution container to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addSolutionContainerTo = function ($container) {
    var self = this;

    self.$solutionContainer = $('<div/>', {
      'class': 'h5p-guess-answer-solution-container',
      html: this.params.solutionLabel
    }).click(function () {
      $(this).addClass('h5p-guess-answer-showing-solution').html(self.params.solutionText);
      self.trigger('resize');
    }).appendTo($container);
  };

  return C;
})(H5P.jQuery);
```




```
var H5P = H5P || {};

/**
 * Guess the answer module
 * @external {jQuery} $ H5P.jQuery
 */
H5P.GuessTheAnswer = (function ($) {

  /**
   * Initialize module.
   * @param {Object} params Behavior settings
   * @param {Number} id Content identification
   * @returns {Object} C Counter instance
   */
  function C(params, id) {
    this.$ = $(this);
    this.id = id;

    // Set default behavior.
    this.params = $.extend({}, {
      taskDescription: '',
      solutionLabel: 'Click to see the answer.',
      solutionImage: null,
      solutionText: ''
    }, params);
  }

  /**
   * Attach function called by H5P framework to insert H5P content into page.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.attach = function ($container) {
    this.setActivityStarted();
    this.$inner = $container.addClass('h5p-guess-answer')
      .html('<div></div>')
      .children();

    //Attach task description, if provided.
    this.addTaskDescriptionTo(this.$inner);

    //Attach image, if provided.
    this.addImageTo(this.$inner);

    //Attach solution container.
    this.addSolutionContainerTo(this.$inner);
  };

  /**
   * Adds a task description if provided in semantics, to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addTaskDescriptionTo = function ($container) {
    if (this.params.taskDescription) {
      $('<div/>', {
        'class': 'h5p-guess-answer-title',
        html: this.params.taskDescription
      }).appendTo($container);
    }
  };

  /**
   * Adds image to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addImageTo = function ($container) {
    var self = this;

    if (self.params.solutionImage && self.params.solutionImage.path) {
      var $imageHolder = $('<div/>', {
        'class': 'h5p-guess-answer-image-container'
      }).append($('<img/>', {
        'class': 'h5p-guess-answer-image',
        src: H5P.getPath(self.params.solutionImage.path, self.id),
        load: function () {
          self.trigger('resize');
        }
      }));

      $imageHolder.appendTo($container);
    }
  };

  /**
   * Adds a solution container to the provided container.
   *
   * @param {jQuery} $container The container which will be appended to.
   */
  C.prototype.addSolutionContainerTo = function ($container) {
    var self = this;

    self.$solutionContainer = $('<div/>', {
      'class': 'h5p-guess-answer-solution-container',
      html: this.params.solutionLabel
    }).click(function () {
      $(this).addClass('h5p-guess-answer-showing-solution').html(self.params.solutionText);
      self.trigger('resize');
    }).appendTo($container);
  };

  return C;
})(H5P.jQuery);
```
