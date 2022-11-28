#Functionality 
### Back Links
[[OpenGL]]

# Overview
The graphics pipeline takes in a set of 3D coordinates and transforms them to coloured 2d pixels on the screen. The pipeline can be broken down into multiple steps, each requiring the output of the previous step as input.

All of these step have very specific functions and are done in parallel across the GPU’s cores, The GPU runs small programs for each step of the pipeline, these are called ‘[[Shaders]]’. Some of these shaders are configurable by the developer, meaning we can write our own shaders to replace the default ones, this provides us fine grain control over parts of the pipeline, and saves us valuable CPU time.

Shaders are written in the OpenGL Shading Language (GLSL).

Pic needed
Abstract representation of the graphics pipeline (blue shows where shaders can be changed)

## The steps of the pipeline

As input to the graphics pipeline we pass in a list of three 3D coordinates that should form a triangle in an array called ‘Vertex data’ (a collection of vertices). A vertex is a collection of data per 3D coordinate, represented using ‘vertex attributes’ that can contain any data.

<aside> 📢 For OpenGL to know how to handle the vertex data it must be told what kind of render types you want to form from it. These hints are called ‘primitives’ and are handed to OpenGL when calling drawing commands. ( `GL_POINTS` , `GL_TRIANGLES` , `GL_LINE_STRIP` )

</aside>

1.  Vertex shader: takes a single vertex as input, transforms the 3D coordinates into different 3D coordinates, does some basic processing on the vertex attributes.

2.  Primitive assembly: takes all vertices from last step as input, and assembles all points in the primitive shape given.
``
3.  Geometry shader: takes collection of vertices that form a primitive, can generate other shapes by emitting new vertices to form new ( or other ) primitives (creates second triangle in diagram above.

4.  Rasterization stage: maps the resulting primitives to pixels on the final screen, producing fragments for the next step. before the next step starts, clipping is performed, discarding all fragments that are outside of your view. (boosting performance and reducing unneeded work)

    <aside> 📢 A fragment in OpenGL is all the data required for OpenGL to render a single pixel.
    
    </aside>

5.  Fragment shader: Calculates the final colour of a pixel, this is the stage where advanced OpenGL effects are performed, the fragment shader usually contains data about the 3D scene that it can use to calculate the final pixel colour. (light, shadows, etc.)

6.  Alpha test and blending stage: checks depth and stencil values of fragments, and uses that to check if the resulting fragment is behind or in front of other objects and should be discarded as needed. This is also where opacity is calculated.
