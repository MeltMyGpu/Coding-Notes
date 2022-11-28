SDL2 is a Cross-platform library that allows us to create a window and manage system events.
sdl2 is self referencing within our code, meaning that as longs as any SDL sub-object exists our initialised SDL object will not be dropped, due to all sub-object containing a reference to the original.

SDL must be configured to interact with different graphics API's, this requires the creation of the specific GAPI's context *before* the creation of the window via SDL, but after the creation of the SDL context reference.

==For the sake of the graph view, there might be no linking to information regarding the api used in examples.==

## Topics and links 
[[Window creation]]
