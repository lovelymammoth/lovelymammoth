---
title: Layout Camera Toolkit for Maya
description: A Maya tool that streamlines camera layout for layout artists — create, manage, and navigate production cameras with precision from a single panel.
date: 2026-04-23
tags:
  - Maya
  - Python
  - Pipeline
  - Layout
  - Camera
cover:
  - images/lct_cover.jpg
weight: 2
draft: false
github: https://github.com/lovelymammoth/layout-camera-toolkit
---
<iframe width="100%" height="400" src="https://www.youtube.com/embed/1jnbaGMZZRs" title="Layout Camera Toolkit Demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Camera layout sits at the heart of every production, but the process has always been fragmented: manually positioning cameras, hunting through the outliner, toggling frustums one by one. This toolkit brings everything into one panel, letting layout artists focus on the shot instead of the software.

## The problem

Layout artists need to move fast during early production. Blocked shots get iterated on constantly — cameras get renamed, repositioned, swapped out. Maya's default workflow spreads those tasks across the viewport, the attribute editor, and the outliner, which adds friction to a job that demands precision and speed. A dedicated toolkit that centralises camera creation and management removes the technical overhead and gives the artist back their flow.

## How to use

The toolkit is divided into two areas: **Create** and **Manage**.

### Create Cameras

- Type a name directly into the panel to set the camera's identifier before creating it
- **Create from current view** — snaps a new camera to exactly where you're looking in the viewport
- **Choose lens** — pick from common focal lengths to match your shot brief
- **Create Focus Target** — attaches a focus null to the camera, ready for depth-of-field work
- **Delete** — removes the selected camera cleanly from the scene

### Manage Cameras

- **Select** — pick any camera in the scene from the panel list
- **Cycle** — step forward and backward through all cameras in sequence
- **View through selected** — jump into a camera's perspective in one click
- **Enable / Disable Frustum** — toggle the camera's frustum display per camera, keeping the viewport clean when working with multiple setups

## Notes

This toolkit started as a personal project to merge a background in photography and videography with technical artist work. The goal was to build something genuinely useful for the Layout TD role — a tool that abstracts away the repetitive parts of camera setup so artists can concentrate on composition from the earliest stage of production.

It was developed under the guidance of [Alexander Richter](https://www.alexanderrichtertd.com/) and his Python Cohort on Python for VFX — a structured programme that bridges the gap between artistic and technical pipelines in the VFX industry.

Future directions could include composition guides (Rule of Thirds, Golden Spiral), a Shot Manager with Maya Camera Sequencer integration and XML ingestion for generating camera sequences, and a Shot Type selector that positions cameras automatically based on cinematography conventions — close-up, medium, Dutch angle, low/high angle — relative to selected character rigs in the scene.