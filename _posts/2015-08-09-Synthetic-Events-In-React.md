---
layout:     post
title:      React-ing to External Events
date:       2015-08-09
summary:    Using stopImmediatePropagation to stop events outside React
categories: 
---

In Facebook's React, event handlers are passed "Synthetic Events", a wrapper around native events with the benefit of being cross-browser.  By default, event handlers are triggered in the bubbling phase, but this can be switched to the capture phase by appending the string "Capture" to the event name - similar to the normal `addEventListener()`. 

Although events appear to capture and bubble, React is implemented using a pattern called Event Delegation, giving [performance benefits](http://davidwalsh.name/event-delegate). This works by having a single top-level event listener and an internal mapping to event handlers as components are mounted and unmounted.  

A tricky by-product of this is dealing with events outside of the React world. For instance, events bound to the global `document` object.

Imagine a React component is listening for an onMouseUp event.

{% highlight javascript %}
    render: function() {
    	return (
    		<article onMouseUp={this.saveContent} />
    	)
    }
{% endhighlight %}

Somewhere else in the application there is a onmouseup event bound to the `document`.

{% highlight javascript %}
    document.onmouseup = function() {
        alert('document.onmouseup');
    }
{% endhighlight %}

`document.onmouseup` is triggered in the bubbling phase, so it's expected that a mouseup in the article tag will trigger the article's event handler first because it is a child to the document.  To stop propagation to the `document` listener, the normal method is:

{% highlight javascript %}
    saveContent: function(e) {
    	e.stopPropagation();
    }
{% endhighlight %}

 But this won't work in React because of Event Delegation.  The solution is to use the much less common, `stopImmediateProgagation()` on the native event object.  This method stops the event from being transmitted to other listener's on the same level along with higher, as opposed to just higher, in which `stopProgagation()` does.

 So, in order to handle the event in the article event listener, but not the `document` listener:

{% highlight javascript %}
     saveContent: function(e) {
     	e.nativeEvent.stopImmediatePropagation();
     }
{% endhighlight %}

Also, ensure the `document` listener was bound after the article listener, because event listeners on the same level are called in the order they are bound.
