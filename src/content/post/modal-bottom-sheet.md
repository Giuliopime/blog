---
title: "ModalBottomSheet and the system navigation bar"
publishDate: "18 August 2023"
description: "An improved version of the ModalBottomSheet that works well with the system navigation bar!"
tags: ["jetpack-compose"]
ogImage: "/thumbnails/modal-bottom-sheet.png"
---
The material 3 version of the `ModalBottomSheet` is quite simple to use in Jetpack Compose (*see [this guide](https://developer.android.com/jetpack/compose/layouts/material#bottom-sheets)*), but the default version isn’t pixel perfect.  
It might end up behind the system navigation bar or lag behind it when closing.  
![ModalBottomSheet default and custom demo](~/assets/jetpack-demos/modal-bottom-sheet.gif "ModalBottomSheet demos")  
As you can see from this simple demo, the default sheet lags behind the navigation bar when closing, while our custom one feels a bit better.  

## The fix
First, make sure you tell compose that you are going to handle insets yourself, by adding this piece of code in your activity  
```kotlin
WindowCompat.setDecorFitsSystemWindows(window, false)
```  

Here is an example of a full activity for reference  

<script src="https://gist.github.com/Giuliopime/7a0d0ae61501f80acf341ea87cf66eee.js"></script>  

Now we just need the the sheet to **ignore the system navigation bar insets**, we can do this by passing a `WindowInsetsthat` doesn’t take count of that, for example `WindowInsets.displayCutout` (*those probably aren’t the best WindowInsets to use but they get the job done for this demo*).  

If you don’t do anything else, the sheet content will go behind the navigation bar, because it doesn’t take count of its insets, so we **wrap the content in a `Column` and apply the `Modifier.padding(bottom = bottomPadding)` modifier to it**.  
The `bottomPadding` is calculated outside of the Column scope via `WindowInsets.navigationBars.asPaddingValues().calculateBottomPadding()`.  
If we were to call this method inside the ModalBottomSheet we would not get a valid padding since those insets have already been consumed.  

Here is the improved ModalBottomSheet:  
<script src="https://gist.github.com/Giuliopime/4ad502981b8169550a8197360000dd5c.js"></script>  

## Source code
You can find the full code for the demo in this article on my [GitHub repo](https://github.com/Giuliopime/jetpack-demos/tree/main) ([link to the exact file](https://github.com/Giuliopime/jetpack-demos/blob/main/app/src/main/java/dev/giuliopime/jetpackdemos/demos/bottomsheet/ModalBottomSheetScreen.kt))  

Hope this helped ^^