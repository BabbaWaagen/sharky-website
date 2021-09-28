---
title: "Passes"
description: "Passes in the Atom Renderer"
weight: 300
toc: true
---

This section provides technical details about how passes are created and managed in the Atom Renderer.

## What are passes?  

Every detail you see in the final rendered frame is calculated through a series of passes. Passes produce images as textures, buffers, or render targets. Each image contains a specific piece of information about the scene, such as color, normals, and depth. These images of information are combined to produce more complex effects such as shadows, lighting, blur, glow, and other post-processing effects. 

Passes are logical groupings of render work with a defined input and output. Each pass takes its input, performs calculations on it, and then produces an output.

**Examples**  
Passes are a means to produce a desired visual effect. To demonstrate, consider the following examples: 
- A *forward render* pass receives a list of objects to draw and outputs a rendered image of those objects viewed from the camera's perspective in the scene. 
- A *depth of field* pass takes an image and a depth buffer and outputs a new image that mimics a real world camera's ability to focus on a specific area. 
- A *skinned mesh* pass takes a mesh's vertices, calculates movement, and outputs the new positions of the vertices.

## Contents
This section covers the following topics.
| Topics                        | Description |
|--------------------------------------|---------|
| [Pass System](pass-system/) | An overview of the pass system in Atom. |
| [Pass Template File Specification](pass-template-file-spec/) | JSON reference for pass template data (`*.pass` files). |
| [Authoring Passes](authoring-passes/) | Learn how to author passes in the pass system.  |