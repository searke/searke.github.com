---
layout: post
title: Unicode Art
excerpt: Ascii art is a popular way of recreating images out of characters. I haven't seen it made out of Chinese characters, even though they work well for this purpose. This is some annotated Mathematica code on how to do this.
---

#Unicode Art
-----

Ascii art is a popular way of recreating images out of characters. I haven't seen it made out of Chinese characters, even though they work well for this purpose. This is some annotated Mathematica code on how to do this.

First, we need the unicode ids of the characters we are interested in using:

    ids = Range[19968, 19968 + 2000];

For each id, we need to get an idea for how light that id's character is on a scale from 0 to 1. First make a function that counts the number of black pixels and then apply this to all the characters and normalize the results. 

    lightness = 
        Composition[Total, Flatten, ImageData, 
        Rasterize[#, RasterSize -> {13, 16}] &, FromCharacterCode];

    lightnessTable = 
        Rescale[#, {Min@#, Max@#}] &@
        ParallelMap[lightness, ids];

Then we make a function that takes a darkness specification from 0 to 1 and returns the unicode character index of an appropiate character. There are more efficient ways of doing this of course and it doesn't need to be very precise to have the wanted effect: 

    colorToCharacterIndex[n_] := First@Nearest[Rule@@@sortedCharacters, n]

This code make a small sized grayscale image from an example image built into Mathematica:

    exampleImage = 
        ColorConvert[#, "GrayScale"] &@ImageResize[#, 100] &@
        ExampleData[{"TestImage", "Lena"}];

For each pixel, we get the corresponding Chinese Character and put it in a grid:

    GraphicsGrid@
        Map[FromCharacterCode@colorToCharacterIndex@# &, 
            ImageData@exampleImage, {2}];

This can be manually resized and rasterized. Getting the parameters correct in practice requires some trial and error:

![Chinese Unicode Art]({{ site.url }}/assets/chineseCharacterTest.png)

