---
title: "Jetpack Compose color picker with hex values"
publishDate: "19 August 2023"
description: "A simple yet powerful Jetpack Compose color picker!"
tags: ["jetpack-compose"]
ogImage: "/thumbnails/color-picker.png"
---
A very common component needed for an app is a simple yet powerful color picker.

Android unfortunately doesn’t offer one out of the box and that’s why I made my own.
It’s implemented with a simple `AlertDialog` and it allows both some pre-made options and the input from the user via hex values.

> This obviously isn’t the most user friendly design, but it’s great for a user base of developers or designers.

## The code
<script src="https://gist.github.com/Giuliopime/2739a199a51e9f8531aa2ab172fdb868.js"></script>

The picker receives:
- an initial color to display
- a list of colors (strings in the hex format) that renders and displays to the user
- a function which will be called when a **valid** color gets choosen by the user

It requires some utility functions too: some simple ones that transform strings to color objects and a trickier one, the `Color.contrastColor()` which, based on a given color, determines if a text placed above it should be White or Black.

## Demo
![Color Picker demo](~/assets/jetpack-demos/color-picker.gif "Color Picker demo")

## Source code
You can find the full code for the demo in this article on my [GitHub repo](https://github.com/Giuliopime/jetpack-demos/tree/main) ([link to the exact file](https://github.com/Giuliopime/jetpack-demos/blob/main/app/src/main/java/dev/giuliopime/jetpackdemos/demos/colorpicker/ColorPickerScreen.kt))

Peace ✌🏼
