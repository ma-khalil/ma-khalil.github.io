---
published: true
layout: post
title: First Milestone
---
## Introduction

In this blog post, I'd like to give an overview of what I've been doing for the past month since I've joined SoK this year. It has been an amazing journey so far and I'm really looking forward to completing the project and seeing how the whole thing looks in the end.

In January, I had been accepted as a SoK student, in which I'm going to work to extend Peruse functionality to support visualising Jump objects on the screen. Peruse is an awesome comic book reader/creator that make reading/creating a comic book really easy and it supports the ACBF format. Some of those comic books might have something called Jump object, a Jump object is a clickable area on a comic book page which links to another page in the book, clicking on that area should navigate the reader to the target page. This can be used to create/read Interactive Fiction Books, such as Create Your Own Adventure type comic books. By the end of SoK, Peruse will be able to visualise Jump objects on pages in a nice, and attractive way, while also providing the functionality to create and preview how they'd look like on the screen.

## The Overview

Before we started this journey, I had been discussing how to go and execute the plan deducted with Leinir, my awesome mentor whom I feel very lucky to have, I've learned A LOT from him and he has been really supportive and helpful. First, we decided to try creating arbitrary jumps on different pages in any book and visualising them as just basic rectangles on the screen, so that I can get used to the code and learn more about the code base.

![](https://invent.kde.org/graphics/peruse/uploads/0149b24d71768b380869f7bce18fd368/image.png)

![](https://invent.kde.org/graphics/peruse/uploads/e18100defaf02c78d811acb79dd94f5d/image.png)

We decided to modify Peruse's ACBF Library so that it returns the Jump objects directly, instead of returning them as a list of positions, which we'll then use to directly access those objects easily in the QML or the frontend part of the Reader, and that'll help us in retrieving the `Q_PROPERTY` of those objects directly. Here's the [merged MR](https://invent.kde.org/graphics/peruse/-/merge_requests/13).

After that MR got merged, I tried experimenting with how we'd like to visualise/represent those Jump objects in a nice, and attractive way. Leinir and I settled on representing them using circular shapes, inspired by how modern interactive/point and click games work. Here is the [MR](https://invent.kde.org/graphics/peruse/-/merge_requests/12) created for this. Essentially, I created a new component to handle the Jump objects called `JumpHandler`, in which it'll take the actual Jump object from the loaded data model from the ACBF library and it'll extract from it the location, and dimensions information. Each `JumpHandler` component draws itself on the page/frame and adjusts itself according to the zooming ratio. In order to integrate that new component, we had to modify the `ImageBrowser` to support loading enough `JumpHandler`s for the Jump objects on each page, simply using a `Repeater` instance.

Here's a small video of how Reader represents the objects now:

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/izcaGrXT7UI/0.jpg)](http://www.youtube.com/watch?v=izcaGrXT7UI)

There are still some minor details that should be sorted out in the MR, then it should be ready to get merged

## Conclusion

In conclusion, I'm really happy with the progress so far, and really happy that I've joined SoK this year. It has been a great jounrey with a lot of new experiences and things to learn, I've learned a lot about QML, its tricks, and best practices (thanks to Leinir). For the next steps, we're planning to start working on Creator. Currently, Creator supports creating new Jump objects, however, it doesn't yet support modifying existing ones. So, stay tuned for the next blog post and wish me luck.
