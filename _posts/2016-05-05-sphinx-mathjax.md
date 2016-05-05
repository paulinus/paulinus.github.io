---
layout: post
title: Latex font on Sphinx's MathJax
---


Sphinx comes with a MathJax extension.  It let's you write Latex equations that are parsed by MathJax on the browser at viewing time.  Pretty cool.

The extension, however, does not set any MathJax option.  That causes MathJax to use the default font which looks quite ugly.

<center><img src="/images/2016-05-05-before.png" /></center>

Fortunately, you can add some javascript code to Sphinx's templates to configure MathJax properly, and get something like this

<center><img src="/images/2016-05-05-after.png" /></center>

Much better!

So here's how you do it.

First extend the the layout template to add a custom script.  Create the file `docs/source/_templates/layout.html` with this content

{% highlight js+cheetah  %}
{% raw  %}
{% extends "!layout.html" %}
{% set script_files = script_files + ["_static/mathjax_conf.js"] %}
{% endraw %}
{% endhighlight %}

Then add the config script `docs/source/_static/mathjax_conf.js` with

{% highlight js+cheetah  %}
MathJax.Hub.Config({
   "HTML-CSS": {
        availableFonts: ["TeX"],
        scale: 90
   }
});
{% endhighlight %}

Note that the `scale: 90` was needed to make the font size match that of the `sphinx_rtd_theme`. You might need other values for other themes.
