---
layout: post
title: Unicode Art
excerpt: ASCII Art Is Best Made With Chinese Characters 
---

# Unicode Art
-----

Ascii art is a popular way of recreating images out of characters. I haven't seen it made out of Chinese characters, even though they work well for this purpose. This is some annotated Mathematica code on how to do this.

First, we need the unicode ids of the characters we are interested in using:

<code class="Mathematica">
    characters = FromCharacterCode /@ Range[19968, 19968 + 2000]
</code>

For each id, we need to get an idea for how light that id's character is on a scale from 0 to 1. First make a function that counts the number of black pixels and then apply this to all the characters and normalize the results. 

<code class="Mathematica">    
   lightness = 
        Total @*
        Flatten @*
        ImageData @*
        (Rasterize[#, RasterSize -> {13, 16}] &)
 
    lightnessTable = 
        Rescale[#, {Min@#, Max@#}]&@ 
        ParallelMap[lightness, ids]
</code>

Then we make a function that takes a darkness specification from 0 to 1 and returns the unicode character index of an appropriate character. There are more efficient ways of doing this of course and it doesn't need to be very precise to have the wanted effect: 

<code class="Mathematica">    
   intensityToCharacter = 
        First @*
        Nearest[Thread[lightnessTable -> characters]]
</code>

This code make a small sized grayscale image from an example image built into Mathematica:

<code class="Mathematica">
    exampleImage = 
        ColorConvert[#, "GrayScale"]& @
        ImageResize[#, 100]& @
        ExampleData[{"TestImage", "Mandrill"}]
</code>

For each pixel, we get the corresponding Chinese Character and put it in a grid:

<code class="Mathematica">
    GraphicsGrid@
        Map[intensityToCharacter, ImageData@exampleImage, {2}]
</code>

This can be manually resized and rasterized. Getting the parameters correct in practice requires some trial and error:

<img class="pure-img" src="{{ site.url }}/assets/chineseCharacterTest.png">

