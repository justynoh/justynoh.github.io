---
layout: page
title: Scotty3D
permalink: /projects/scotty3d/
---

_[back to projects](/projects/)_

For a class on computer graphics, I implemented the various components of a graphics software called _Scotty3D_. This included SVG drawing, mesh editing, ray tracing and animation components.

For SVG drawing, I implemented a series of functions to rasterize points, lines, triangles, general polygons and images with alpha compositing. For the images, transformations such as scaling and rotation were also implemented. Anti-aliasing was implemented via supersampling for basic shapes and trilinear filtering over a mipmap for images.

The next three components all came together to form a 3D modelling software with realistic model rendering. The first component was an editor for models created using a halfedge triangle mesh. Mesh operations such as edge splitting, edge collapse, edge deletion and face beveling were implemented. In addition, polygon triangulation, linear subdivision, Catmull-Clark subdivision and upsampling using loop subdivision were implemented.

Next, in order to render the models under realistic lighting, a ray tracer was written using the rendering equation. A numerical approximation to the integral over the hemisphere around each surface point was computed by adding the contribution of sampled paths of light which would have scattered off that point, scaled by the bidirectional scattering distribution function. A monte carlo method was used to determine when to cut off each ray, so as not to trace each light path for infinitely long.

The final component was to write the functions enabling simple animation of mesh models based on interpolating keyframes. Each keyframe could be created by rotating or moving each joint in the mesh. The Euler angles were stored in a rooted tree of joints. Then, interpolation between the keyframes was implemented using Catmull-Rom spline interpolation of positions over time.