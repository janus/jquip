jQuery getting too big?

# Introducing jquip - aka jQuery-in-parts.

Smaller, Lighter, Faster, more modular jQuery - include only the parts you want! Don't use it, Don't include it.
Has 90% of the good parts of jQuery (rest to be added plugins as needed), small enough to drop-in as source saving an external js reference.

The core **jquip.js** is only **4.28KB** (minified and gzipped) only **13%** of the size of jQuery.

Includes 7-8x Faster DOM traversal for <= IE7. (i.e. where there's no querySelector) *see limitations
Most code has been ported from jQuery and optimized where possible, e.g. internals use underscore's native `_.each` over jquery's slower `$.each` etc.

Licence: http://www.opensource.org/licenses/mit-license.php

## What's in the box? - i.e. the 90% good parts

Methods marked with * are only partially implemented.

  - [$(selector)](http://api.jquery.com/jQuery/) 
	- $(selector, context), $(element), $(array)
	- $(callback) requires **docready** plugin.

### Methods operating on a `$(selctor)`
  
  - each
  - attr
  - bind
  - unbind
  - data
  - append
  - prepend
  - before
  - after
  - toggle*
  - hide, show, fadeIn and fadeOut *does so without animation, consider using [enhances animaiton plugin](http://playground.benbarnett.net/jquery-animate-enhanced/)*
  - eq
  - first
  - last
  - slice
  - find*
  - remove
  - val - *does not do checkbox, select, etc.*
  - html
  - addClass
  - removeClass
  - hasClass
  - trigger
  - parent
  - parents
  - parentsUntil
  - next
  - prev
  - nextAll
  - nextUntil
  - prevUntil
  - siblings
  - children
  - contents
  - scrollLeft
  - scrollTop

### Events: 

blur focus focusin focusout load resize scroll unload click dblclick 
mousedown mouseup mousemove mouseover mouseout mouseenter mouseleave 
change select submit keydown keypress keyup error

### static methods off $
  
  - $.each and Underscore's faster [_.each](http://documentcloud.github.com/underscore/#each)
  - [_.select](http://documentcloud.github.com/underscore/#select)
  - $.filter
  - $.dir
  - $.nth
  - $.sibling
  - $.map
  - $.bind
  - $.unbind
  - $.data
  - $.attrs
  - $.trim
  - $.indexOf
  - $.isFunction
  - $.isArray
  - $.isWindow
  - $isNaN
  - $.merge
  - $.extend
  - $.unique

## Plugins

Pick and choose the parts of jQuery when and add you use them.

Other parts of jQuery can be Added via Plugins which is simply a matter of copying or including the 
script after the core `jquip.js`.

### [documentReady](blob/master/jquip.docready.js)
yep, it's a plugin!

  - [$(function())](http://api.jquery.com/ready/)
  - [$.ready](http://api.jquery.com/ready/)

### [css](blob/master/jquip.css.js)

  - [$.css](http://api.jquery.com/css/)
  - [$.Width](http://api.jquery.com/width/)
  - [$.Height](http://api.jquery.com/height/)
  - $.camelCase

### [ajax](blob/master/jquip.ajax.js)
based on [David Flanagan HttpUtils](http://www.davidflanagan.com/javascript5/display.php?n=20-1&f=20/01.js) 
modfied to work like jQuery's ajax.

  - $.xhr (cross-browser XHR Native Object)
  - [$.ajax](http://api.jquery.com/jQuery.ajax/)
  - [$.getJSON](http://api.jquery.com/jQuery.getJSON/)

### [custom](blob/master/jquip.custom.js)

  - $.queryString - cached map of queryString variables 
  - $.is[Tab|Enter|Shift|...] - static functions to detect named keys pressed, e.g. `if ($.isEnter(e)) console.log("pressed enter")`
  - $.fromHtml - creates a document fragment from a html string
  - $.cancelEvent - cross-browser fn to `preventDefault()` and `stopPropogation()`, returns false.

### Limitations

Parts of jQuery that aren't ported over (because of code size) throw a "not implemented exception".
At the moment this only gets thrown for complex filters that filter on more than a tagName.

* For <= IE7 all selectors require an Id (i.e. #) or Tag Name (e.g. INPUT) in each child selector.
 
 Valid Examples:
   - TBODY TD.c1 INPUT
   - TH.c1 STRONG
   - #btnSubmit SPAN
   - TBODY INPUT[name='chkProcess']
   - TBODY INPUT[type='text']


### Contributing

I'd love help with this so pull requests are more than welcome!

The main task that needs doing is to get all the missing jQuery parts in as plugins 
and a comprehensive test suite so we can properly identify the parts of jQuery supported.

Feedback is welcome, drop me a line on twitter at [@demisbellot](http://twitter.com/demisbellot).
