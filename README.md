#Mini DOM Ready

This code was inspired by Dustin Diaz and [the smallest DOM ready code ever](http://www.dustindiaz.com/smallest-domready-ever) and is intended to be copied and pasted into the HEAD of your document.

This should work in IE6+, > FF 3.5, and everything else.

Dustin's technique uses polling to determine the state of the document, while this implementation uses native DOM events when possible, falling back to polling. I fealt it was worth sacrificing a few bytes for the sake of leveraging native DOM events whenever possible. I am fairly pleased with the result (.25 Kb minified). By default we create a global `domReady` method which should work exactly like the jQuery syntax:

```
//     $(function() { … });
//jQuery(function() { … });
domReady(function() { … });
```

You can even define your own method name in case you don't like the name "domReady". For example, you could change `domReady` to `blah`, then you could write the following code:

```
blah(function() { 
	alert("I'm not very good at naming functions.");
});
```

###Why is this useful?

Because you *should* be loading jQuery (and other scripts) at the very bottom of the page, immediately before the closing `</body>` tag.  However, when using a CMS you might need to render some inline code which should execute on DOM ready… but jQuery hasn't loaded yet!  So instead of writing the following:

```
$(function() {
	$('.slider').Swipe();
});
```

… you would instead write:

```
domReady(function() {
	$('.slider').Swipe();
});
```

##Tidbit
You could rename "domReady" to a dollar sign `$` or `jQuery`, which would allow for a seamless way to use jQuery syntax before it's even loaded.  You could just keep your inline code the exact same.  However, I advise against this as it will make your code confusing - others may think you have actually loaded jQuery.
