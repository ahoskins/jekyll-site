---
layout:     post
title:      DOM events in React
date:       2015-08-09
summary:    A use case for event.stopImmediatePropagation()
categories: 
---

In React, events are a bit interesting.  React is implemented using a pattern called Event Delegation, giving [performance benefits](http://davidwalsh.name/event-delegate).  Event Delegation works by having a single top-level event listener and an internal mapping to event handlers as components are mounted and unmounted.  Event handlers are then passed these abstracted events, known as Synthetic Events.  This post explains a tricky experiance I had when dealing with normal HTML document events in conjunction with React events.

Imagine a React component is listening for an onMouseUp event.

{% highlight javascript %}
    saveContent: function(e) {
        // respond to event
    }
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

What do we expect to happen?  We know `document.onmousup` is triggered in the bubbling phase, because this is the default for normal event handlers.  So we expect the React event handler bound to the `Article` tag to trigger first, then the event bubbles up, eventually triggering the `document.onmousup`.

If we wanted to only handle the event in the React event handler, the usual method to stop further bubbling is `stopPropagation()`:

{% highlight javascript %}
    saveContent: function(e) {
        // respond to event
        // ...
    	e.stopPropagation();
    }
    render: function() {
        return (
            <article onMouseUp={this.saveContent} />
        )
    }
{% endhighlight %}

 But this won't work because of Event Delegation!  Remember, the Article tag event handler is actually bound at the top-level!  The solution is to use `stopImmediateProgagation()`.  This method stops the event from being transmitted to other listener's on the **same level as well as higher**, as opposed to just higher, in which `stopProgagation()` does.  But for this to work, the `document` listener must be bound after the article listener, because event listeners on the same level are called in the order they are bound.  

I've only ran into this issue once while using React.  And of course, the easiest and probably best fix is to avoid using document events in conjunction with React.
