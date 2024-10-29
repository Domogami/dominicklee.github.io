---
title: Yabai
---

## The Ultimate Tiling Window Manager

Yabai is a MacOS tiling window manager that uses binary space partitioning which sub-divides the space in half. The first window you open is opened in full screen to take up all available space. The next window that is opened however shrinks the first window to the left 50% of the screen and the new window uses the remaining 50% (splitting the screen vertically). Similarly, when a third window is created the previously created window is divided in half (horizontally) and the previous window takes up the top 25% while the new window fills the bottom 25%. This process repeats until the window becomes so small as to not be practical.

Something noteworthy about Yabai is that it prioritizes all windows in a space being shown at all times. By default no windows ever overlap (although some can be toggled to full screen) which means that the user is more conscious of which windows are open leading to less valuable windows being closed instead of falling to the back of the z-stack.

## How I Use Spaces and Windows

Personally, I use spaces (sometimes referred to as "Virtual Desktops") differently than most people. I often associate each of my 10 "spaces" with a different application or pair of applications then use keybindings to quickly switch between each space. This leads to a single full screen application being only a keypress away. For example, I often have my web browser on Space 1 and Spotify on Space 4. To switch between them, I simply use `caps + 1` to go to my web browser space and `caps + 4` to quickly jump to Spotify.
