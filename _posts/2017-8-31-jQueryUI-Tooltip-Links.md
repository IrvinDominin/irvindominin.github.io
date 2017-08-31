---
layout: post
title: jQueryUI - Tooltip with links
category: Dev
tags: [jQuery, ]
---

<a href="http://api.jqueryui.com/tooltip/">jQuery UI Tooltip</a> is a jQuery UI plugin that allows you to use a custom tooltip instead of the standard title attribute. It can contain various kind of data, but is not possibile to click links inside the displyed tooltip data.

The reason why is that the cursor enter the tooltip for clicking the link, and the mouseout event of the triggering element hide the tooltip itself.

It's a bit tricky I know, but it's possibile to workaround this issue using the following code.

```js
$(function () {
    $(document).tooltip({
        content: function () {
            return $(this).prop('title');
        },
        show: null, 
        close: function (event, ui) {
            ui.tooltip.hover(
            function () {
                $(this).stop(true).fadeTo(400, 1);
            },    
            function () {
                $(this).fadeOut("400", function () {
                    $(this).remove();
                })
            });
        }
    });
});
```

Currently we can't expect that the jQuery UI team add this feature.

You can play with this code in the following jsFiddle:
<iframe width="100%" height="300" src="//jsfiddle.net/IrvinDominin/jLkcs/5/embedded/js,html,css,result/dark/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>