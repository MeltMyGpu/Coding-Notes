#Functionality 
### Back Links
[[Shaders]] 

# Overview
A program object contains the executable code for all stages of rendering. [[Shaders]] Are attached to the program after compilation, the shader program object is the linked to OpenGL, and the attached shaders are detached.

## Implementation


```rust
    // Load shaders onto program //
    let shader_program:Program = render_gl::Program::from_shaders(
        &gl,
        &[vert_shader, frag_shader]
    ).unwrap();
    // Set current shader program //
    shader_program.set_used();
```

## Linking complied shaders
