---
title: SharkGuard
description: A shark detector for drone footage, trained on more than 120 hours of flights I filmed myself.
summary: Flew a drone for 120+ hours, labeled 500+ frames and trained a YOLOv5 model to spot sharks near surfers.
year: 2022
context: Gap-year project
group: ml
order: 1
tools: [Python, PyTorch, YOLOv5s, DJI Mini 2]
facts:
  - label: Data
    value: 120+ flight hours, 500+ labeled frames
links:
  - label: Code on GitHub
    url: https://github.com/pierre-phu/shark-detector
card: /assets/img/sharkguard/card.jpg
image: /assets/img/sharkguard/card.jpg
cover: /assets/img/sharkguard/cover.jpg
cover_alt: Four people watching the sunset over a surf beach, seen from a drone
redirect_from:
  - /2022-11-15-shark/
---

You have probably heard that a falling coconut is more likely to kill you than a shark. That holds worldwide, but it hides a lot: far more people walk under palm trees every day than surf in waters where sharks hunt.

## The problem

Friends living on Réunion Island told me shark attacks there have become much more frequent in recent years, which they link to overfishing. Whole beaches are now closed to surfers. I had just spent more than three months surfing in Indonesia and Australia, so I know that fear first-hand. I started looking into how attacks are prevented.

## How attacks are prevented today

- Shark nets with a mesh small enough that sharks cannot get through.
- Catching and tagging the largest sharks, then tracking them with offshore buoys.
- Magnetic-field deterrents worn by surfers, still experimental.

These methods are invasive for marine life, and none of them is fully reliable. Consumer drones opened up another option: watching risky areas from the air.

## What I built

New South Wales in Australia funds drone programs that spot sharks from above. Inspired by them, I trained my own detector:

1. I flew more than 120 hours with my DJI Mini 2 over surf spots.
2. I extracted frames from the footage and labeled more than 500 of them.
3. I trained a YOLOv5s object detection model on that dataset.

## Results

Below, the model running on footage I filmed of a bull shark in a nature reserve in Australia. So far I have evaluated it qualitatively, on videos like this one.

<figure>
  <video src="{{ '/assets/video/shark-detection.mp4' | relative_url }}" poster="{{ '/assets/img/sharkguard/detection-poster.jpg' | relative_url }}" width="1280" height="720" autoplay muted loop playsinline aria-label="Drone footage of a bull shark with the model's bounding box following it"></video>
  <figcaption>YOLOv5s tracking a bull shark in drone footage.</figcaption>
</figure>

## Try it yourself

The code and the trained YOLOv5s weights are on [GitHub](https://github.com/pierre-phu/shark-detector). Point it at any YouTube video and it runs the detector on it.
