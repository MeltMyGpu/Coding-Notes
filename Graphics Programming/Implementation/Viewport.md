#Implementation
### Back links
[[OpenGL]]

# Overview
OpenGL must be told the size of the viewport it’s rendering to, this declaration is done separately after window creation during the GL context setup.
`Viewport( x , y, width, height )`

X and Y denote the location of the bottom left of the viewport in relation of the window displaying the render, if using full width and height of window, set these to (0,0).

In order to have the GL render scale with the hosting window, a GL call-back function must be used →
`framebuffer_size_callback(window, width, height)