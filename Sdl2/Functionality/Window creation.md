#Implementation 
### Back links
[[Sdl2]]


# Initialisation

Before we do anything with SDL, we need to initialise it!

```rust
let sdl = sdl2::init().unwrap();
```

`sdl2::init()` returns an enum `Result<Sdl, String>`, we use `unwrap()` here to handle the possible error of a failed startup, if the enum returns ok, it will give us our Sdl struct, if it has an Er, it’s will return the string and `unwrap()` will terminate our program.

Now we have our SDL struct initialised as an object.

### // OpenGL attributes config //

In order to use OpenGL as our graphics API, we need to set some attributes for it before our window is created, in our case here, we are going to create a reference to our video systems OpenGL attributes, then set the context profile to ‘core’ mode, and finally set the version of OpenGL which we are going to use, in this case 4.5.

<aside> 📢 NOTE: It is safer for backward compatibility to have the default version load 3.3. It is possible to then load in features of higher versions when required based on a systems check.

</aside>

```rust
let gl_attr = video_subsystem.gl_attr(); // creates OpenGL to allow us to set some attributes and enable minimal openGL
gl_attr.set_context_profile(sdl2::video::GLProfile::Core);
// sets us to using core
gl_attr.set_context_version(4,5);
// sets version (using recent version, turn to 3.3 if having issues )
```


## Creating a window with OpenGL

We’re going to be using the video subsystem to get a builder of the Vsub, configure it, and then construct it, this will internally contain a close of our SDL object (see overview).

```rust
let video_subsystem = sdl.video().unwrap();
// OpenGl attribute config //
let window = video_subsystem
    .window("title",900,700)
    .OpenGL() // configues window to recieve OpenGl context
    .resizable()
    .build()
    .unwrap();
'main: loop{
// window / application event loop
}// once built the window will remain open while in scope, this loop ensures the window stays open.
```

