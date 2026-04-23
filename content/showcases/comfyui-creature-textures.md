---
title: Creature Texturing with ComfyUI
description: A ComfyUI workflow for generating tileable creature skin textures from 3D depth maps using ControlNet and SDXL. Designed to drop into an existing creature pipeline.
date: 2026-04-01
github: https://github.com/lovelymammoth
tags:
  - ComfyUI
  - AI Art
  - Texturing
  - ZBrush
weight: 1
draft: true
---

Generate production-ready tileable creature textures directly from 3D renders. The workflow uses ControlNet's depth preprocessor as conditioning to create plausible high-frequency surface detail — scales, pores, skin microstructure — without manual painting.

## The problem

Manually painting creature surface detail at texture resolution is time-consuming and hard to keep consistent across multiple UV tiles. This workflow takes a depth pass from ZBrush or Blender and uses it as conditioning to generate tileable detail textures that match the sculpt's curvature.

## How to use

1. Export a 2K depth pass from ZBrush (use Best Preview Render with Depth channel) or Blender (Cycles depth AOV)
2. Load the ComfyUI workflow JSON from the repo
3. Connect your depth map to the ControlNet node
4. Adjust denoise strength: `0.55–0.65` for subtle variation, `0.70–0.80` for more generation

## Notes

Works best with close-up renders. At wider angles the ControlNet conditioning weakens and results become generic. For full-body shots, split the UV space into close-up zones and process each tile separately.

The repo includes a Blender compositor node group that automates the depth pass export.
