#CoreNode
### Back Links
[[The-Game-Engine-Index]]


# Overview
OpenGL is a specification for an API that allows developers to access and use GPU hardware in a standardised way, this specification is implemented by the graphic card manufacturers. This allows developers to interact with different hardware on different platforms via one common interface, with the implementation detail of this interface left up to the GPU manufacturers.

OpenGL functions via ‘states’, referred to as ‘Contexts’. The job of a program implementing OpenGL is to control and change these contexts in order to get the desired effect, the state machine can only be in one context at a time, which allows from the sharing of commands that will perform differing functions depending on the machines current context.

OpenGL is composed of ‘objects’, each representing a subset of OpenGL’s state.



