// ***************************
// 
// Carousel Class
// 
// ***************************

var Carousel = function(carousel) {
  
  // ***************************
  // Variables
  // ***************************
  
  var _this             = this;
  // DOM
  _this.carousel        = carousel;
  _this.slides          = _this.carousel.getElementsByClassName("slide");
  _this.leftArrow       = _this.carousel.getElementsByClassName("arrow left")[0];
  _this.rightArrow      = _this.carousel.getElementsByClassName("arrow right")[0];
  _this.dotsContainer   = _this.carousel.getElementsByClassName("dots")[0];
  _this.dots            = _this.dotsContainer.getElementsByClassName("dot");
  _this.currentSlide    = null;
  // Styles
  _this.styleContainer  = document.createElement('style');
  _this.responsiveInfo = [
    {
      "mediaQuery": "@media only screen and (min-width: 1025px)",
      "imgKey": 'xl'
    },
    {
      "mediaQuery": "@media only screen and (max-width: 1024px)",
      "imgKey": 'lg'
    },
    {
      "mediaQuery": "@media only screen and (max-width: 768px)",
      "imgKey": 'md'
    },
    {
      "mediaQuery": "@media only screen and (max-width: 480px)",
      "imgKey": 'sm'
    },
    {
      "mediaQuery": "@media only screen and (max-width: 320px)",
      "imgKey": 'xs'
    }
  ];

  // ***************************
  // Events
  // ***************************
  
  // On load
  _this.setStyleContainer();
  _this.generateIds();
  _this.createDots();
  _this.doResponsiveSlideImages();
  _this.setCurrentSlide(_this.slides[0]);
  
  
  // On left arrow click
  _this.leftArrow.onclick = function() {
    _this.gotoLeft();
    return false;
  }
  
  // On right arrow click
  _this.rightArrow.onclick = function() {
    _this.gotoRight();
    return false;
  }
  
  // On dot click
  for (var i=0; i<_this.dots.length;i++) {
    var dot = _this.dots[i];
    dot.onclick = function() {
      var id    = this.getAttribute("href").replace("#", ""); 
      var slide = document.getElementById(id);
      _this.setCurrentSlide(slide);
      return false;
    }
  }

};

// ***************************
// Functions
// ***************************

// Create the style container in the document head
Carousel.prototype.setStyleContainer = function() {
  var _this = this;
  var head  = document.head || document.getElementsByTagName('head')[0];
  _this.styleContainer.type = 'text/css';
  head.appendChild(_this.styleContainer);
}

// Generates and sets unique IDs for each slide
Carousel.prototype.generateIds = function() {
  var _this = this;
  for (var i=0; i<_this.slides.length; i++) {
    var slide = _this.slides[i];
    // Generate unique ID
    var d     = new Date()
    var id    = "c"+parseInt(d.getMilliseconds()*Math.random());
    // Assign the ID to the slide
    slide.setAttribute("id", id);
  }
}

// Creates the navigation dots based on the slides
Carousel.prototype.createDots = function() {
  var _this = this;
  for (var i=0; i<_this.slides.length; i++) {
    var slide = _this.slides[i];
    var id    = slide.getAttribute("id");
    // Generate the dot
    var dot = document.createElement("a");
    dot.setAttribute("href", "#"+id);
    dot.setAttribute("class", "dot");
    // Add to dots
    _this.dotsContainer.appendChild(dot);
  }
  _this.dots = _this.dotsContainer.getElementsByClassName("dot");
}

// Generates responsive slide image CSS from DOM 
// and injects into placeholder stylesheet
Carousel.prototype.doResponsiveSlideImages = function() {
  var _this = this;
  for (var i=0; i<_this.slides.length; i++) {
    var slide = _this.slides[i];
    var id    = slide.getAttribute("id");
    // Get image base
    var imageBase = slide.getAttribute("data-image-base");
    // Create the CSS rules
    var cssRules = _this.generateSlideCSS(id, imageBase);
    // Add CSS to document
    _this.styleContainer.appendChild(document.createTextNode(cssRules));
  }
}

// Generates the CSS for a slide's responsive images
Carousel.prototype.generateSlideCSS = function(id, imageBase) {
  var _this   = this;
  var cssRules = "";
  for (var i=0; i<_this.responsiveInfo.length; i++) {
    var info    = _this.responsiveInfo[i];
    var query   = info.mediaQuery;
    var imgKey  = info.imgKey;
    // Generate the image path
    var sizeImg = imageBase.replace(/\.([a-zA-Z]*?$)/, "-"+imgKey+".$1");
    // Create the css rule
    cssRules += query+"{#"+id+" .overlay{background-image:url("+sizeImg+");}}"
  }
  return cssRules;
}

// Go to an arbitrary slide
Carousel.prototype.setCurrentSlide = function(slide) {
  var _this = this;
  var klass = slide.getAttribute('class');
  // Check that the slide isn't already the current slide
  if (klass == "slide") {
    _this.currentSlide = slide;
    var id = slide.getAttribute('id');
    // Make the current slide current
    _this.resetSlideClasses();
    slide.setAttribute("class", "slide current");
    // Find the corresponding dot
    var dot = null
    for (var i=0; i<_this.dots.length; i++) {
      if (_this.dots[i].getAttribute("href") == "#"+id) {
        dot = _this.dots[i];
      }
    }
    // Make the current dot current
    _this.resetDotClasses();
    dot.setAttribute("class", "dot current");
    // Disable arrows if needed
    _this.resetArrowClasses();
    var previous  = this.currentSlide.previousElementSibling;
    if (previous.getAttribute("class") != "slide") {
      _this.leftArrow.setAttribute("class", "arrow left disabled");
    }
    var next = this.currentSlide.nextElementSibling;
    if (next.getAttribute("class") != "slide") {
      _this.rightArrow.setAttribute("class", "arrow right disabled");
    }
  }
}

// Go to previous slide
Carousel.prototype.gotoLeft = function() {
  var _this     = this;
  var previous  = this.currentSlide.previousElementSibling;
  // If there is a previous slide, set to current
  if (previous.getAttribute("class") == "slide") {
    _this.setCurrentSlide(previous);
  }
}

// Go to next slide
Carousel.prototype.gotoRight = function() {
  var _this = this;
  var next  = this.currentSlide.nextElementSibling;
  // If there is a previous slide, set to current
  if (next.getAttribute("class") == "slide") {
    _this.setCurrentSlide(next);
  }
}

// Reset all the slide classes
Carousel.prototype.resetSlideClasses = function() {
  var _this = this;
  for (var i=0; i<_this.slides.length; i++) {
    var slide = _this.slides[i];
    slide.setAttribute("class", "slide");
  }
}

// Reset all the dot classes
Carousel.prototype.resetDotClasses = function() {
  var _this = this;
  for (var i=0; i<_this.dots.length; i++) {
    var dot = _this.dots[i];
    dot.setAttribute("class", "dot");
  }
}

// Reset all the arrow classes
Carousel.prototype.resetArrowClasses = function() {
  var _this = this;
  _this.leftArrow.setAttribute("class", "arrow left");
  _this.rightArrow.setAttribute("class", "arrow right");
}

// ***************************
// 
// App Class
// 
// ***************************

var App = function() {
  
  // ***************************
  // Variables
  // ***************************
  
  var _this       = this;
  _this.carousels = [];


  // ***************************
  // Events
  // ***************************
  
  // On load
  _this.instantiateCarousels();
  
  
};

// ***************************
// Functions
// ***************************

App.prototype.instantiateCarousels = function() {
  var _this     = this;
  var carousels = document.getElementsByClassName("carousel")
  
  // Instantiate carousel class from DOM objects
  for (var i=0; i<carousels.length; i++) {
    var carousel = new Carousel(carousels[i]);
    _this.carousels.push(carousel);
  }
}

// Create new instance
window.app = new App();



