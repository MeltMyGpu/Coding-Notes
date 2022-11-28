#Implementation 
### Back links
[[Shaders]]


## Overview

 
## The Structs data
```rust
pub struct Shader{
    id: gl::types::GLuint, // Unsigned int pointer to GPU mem
    gl: gl::Gl, // Reference to GL object
}
```

### The implementation / Methods
```rust
impl Shader{
    // Standard constructor
    pub fn from_source(
        gl: &gl::Gl, // gl ref
        source: &CStr, // The shader code as a string
        kind: gl::types::GLuint // an enum to represent the shader type
    ) -> Result<Shader, String>{ // returns a result <Ok / Err>
        let id = shaders_from_source(gl,source, kind)?; // gl function forward
        Ok(Shader{
                gl: gl.clone(), // Clones gl for shader construction
                // This increases the ref counter but shallow copies the struct
                id // the id 'pointer' given by Gl for the shader
            })
    }
    // More specific constructors to remove need for specifiying shader type
    pub fn from_vert_source(gl: &gl::Gl, source : &CStr) -> Result<Shader, String>{
        Shader::from_source(gl ,source, gl::VERTEX_SHADER)
    }
    pub fn from_frag_source(gl: &gl::Gl, source : &CStr) -> Result<Shader, String>{
        Shader::from_source(gl ,source, gl::FRAGMENT_SHADER)
    }
    // retrieves shader id.
    pub fn id(&self) -> gl::types::GLuint {
        self.id
    }

}
```

### Avoid memory leaking!
```rust
// We need to avoid leaking shader id, implement drop trait //
impl Drop for Shader {
    fn drop(&mut self){
        unsafe{
            self.gl.DeleteShader(self.id);
        }
    }
}
```