---
title: "Approach towards a better transition between html5 videos"
date: 2020-12-27T01:24:24+05:30
Description: ""
Tags: ["Javascript","Source change","HTML5","Canvas","video"]
Categories: ["Instuctional"]
DisableComments: false
---

An approach to switch videos dynamically in the same video element by changing the source and smoothen that transition using a canvas.
<!--more-->

As a part of a recent project, I had a model that would generate a video based on the input. It was essential for me to add this to the already playing video, to look like a continuous stream. The natural approach is to have multiple video elements and switch between them either by hiding videos or playing with opacity. Still, since my videos were generated in realtime, this wasn't possible. I believe the proper way is to [dynamically create div elements](https://www.techiedelight.com/dynamically-create-div-javascript/). However, here is a different workaround that I used due to my incompetency in JS. 

Javascript provides a powerful element called [Canvas](https://www.tutorialspoint.com/html5/html5_canvas.htm) to draw graphics dynamically. Quite simply, It is a whiteboard, and you can draw on it using Js. But how does this help? 
The idea is to overlay our video element with a canvas with the next frame after sending the input, change the video source in the background, and remove the canvas when the new video starts playing. Video generation needs to be quick here, else the user is stuck staring at an image of the last frame of the video, and that'll be really sloppy work. 

In this code example, our canvas is named 'mycanvas', and the video element is 'vid'.  This function draws the video frame to a canvas when it is called. 

{{< gist lavanaythakral 5568c15f01642e186c5bc7c2ea681a0f >}}

The function below changes the source of the video element. An event handler removes the canvas as soon as the new video starts playing, and then we remove the event handler itself. 

{{< gist lavanaythakral 3d9e494894b2b3455ee7dfb4c3578f6c >}}

Now all that's left is to call these functions in succession on receiving an input.
Please note that ```event.keyCode``` and ```event.which``` have been [depreciated](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/keyCode) and should not be used. 
I am using them for the purpose of this explanation since they are still compatible with Chrome. 

{{< gist lavanaythakral 7b660f4e314f8b534b3c8519cfb7f917 >}}

I hope this helps. 