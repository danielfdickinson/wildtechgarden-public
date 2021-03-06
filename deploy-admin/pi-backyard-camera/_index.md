---
imageFeatured: /assets/images/cover/rabbit-backyard-2021-08-01.jpg
slug: pi-backyard-camera
aliases:
  - /post/pi-backyard-camera/
  - /backyard-pi-sub-pages/
title: "Public Pi Backyard Camera"
author: Daniel F. Dickinson
date: 2021-09-21T02:04:37Z
publishDate: 2021-09-21T02:04:37Z
tags:
    - hosting
    - linux
    - presentations
    - raspberry-pi
    - technology
description: A short talk / presentation about using the Raspberry Pi as a Public Backyard Camera (e.g. live streamed or time lagged snapshots of a bird feeder).
summary: A short talk / presentation about using the Raspberry Pi as a Public Backyard Camera (e.g. live streamed or time lagged snapshots of a bird feeder).
layout: list-content
toc: true
featuredImageAlt: "Digitally zoomed photo of a rabbit in a grassy yard (quite distorted due to zoom level)"
---

## Preface

This is a short talk / presentation I (a member of the MakerPlace) created for fellow Makers at the [MakerPlace](https://midlandlibrary.com/the-mpl-makerplace/) at the [Midland Public Library](https://midlandlibrary.com/). It describes a few ways to use the Raspberry Pi as a public backyard camera. That is, a fellow maker was interested in using a Raspberry Pi and webcam the maker owns in order to capture (and publish) video or snapshots of a bird feeder in their private backyard. I created this page as my suggestions, and other makers presented/will present theirs on Thursday, September 23 at the Midland Makers virtual meeting.

## Software (Capture)

### Motion Sensing

The "go-to" option for the Raspberry Pi is a small program known as 'motion'.

* It is fairly simplistic and is triggered more often an 'computer vision' based systems.
* It has three major advantage over more complex computer vision software:
  1. It operates standalone. (No external processing required and no third party data concerns).
  2. It doesn't take much in the way of processing power (which is especially important for Pi/Pi B+ generation (old) models).
  3. It doesn't require much RAM (again, this is most important for old Pis).
* You can choose to only record for a period of time after motion is sensed, which increases the likelihood of capturing interesting events without unchanging footage. (For a bird feeder you will still see a lot of what the squirrels are up to though {{< emoji >}}:wink:{{< /emoji >}} {{< emoji >}}:open_mouth:{{< /emoji >}} {{< emoji >}}:unamused:{{< /emoji >}}).

### Not Covered

#### Timed Snapshots

There are many options for creating timed snapshots, but this presentation won't cover them due to time and space limitations.

#### Always Streaming

The configuration below streams only 1 (one) frame per second until motion is detected, then it streams up to 30 fps. Other streaming options which are always at full framerate are available but not covered in this presentation.

## Serving / Streaming

### Configuration & Use

* [Uploading and Sharing Captures From a Server](backyard-pi-upload-serve/)
* [Streaming Directly From Motion (Internet to Local Pi)](backyard-pi-streaming/)

### Note: Masking Out an Area

* In addition to the main configuration mentioned above, you can use a PGM image to mask out a region from the motion detection.
* It is also possible to mask a region from being recorded.
* Setting ``smart_mask_speed`` greater than zero automatically masks out areas during operation (e.g. repetitive motion such as trees swaying in the wind).

## Privacy/Legal Notes

* Do remember to make sure you are allowed by law to record the area,
* Make sure you don't inadvertently broadcast identifiable individuals who haven't agreed to be recorded and could reasonably be expected to be in the area.
  * For example, don't use this for your front door camera.
* Using this for a private fenced backyard should be fine, but I am not a lawyer, I just believe that to be a reasonable expectation.
* Watch where you aim the camera as you might otherwise publicly broadcast something you shouldn't.
* Do remember to check what is being recorded on a regular basis.
* Provide a way to be contacted so you can remove something that is an issue, should it be required to do so.
