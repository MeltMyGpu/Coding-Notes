#Implementation #NeedsFillingOrNotes

### Back links
[[Shader program]]


## The struct data

```rust
pub struct Program{
    id: gl::types::GLuint, // pointer
    gl: gl::Gl,            // gl ref pointer
}
```

## The implementation / methods

```rust
impl Program{
    // takes a slice of Shader structs // These are only required frok linking //
    pub fn from_shaders(gl: &gl::Gl, shaders: &[Shader]) -> Result<Program,String> {
        // create a program as shader target
        let program_id = unsafe {gl.CreateProgram()};
        // iterates and attaches shaders provided //
        for shader in shaders {
            unsafe { gl.AttachShader(program_id, shader.id()); }
        }
        // Links program to our GL context.
        unsafe { gl.LinkProgram(program_id); }
        
        // ERROR handling //
        let mut success: gl::types::GLint = 1;
        // fetches linking status // 0 == failure //
        unsafe{
            gl.GetProgramiv(program_id,gl::LINK_STATUS, &mut success)
        }

        if success == 0{
            let mut len: gl::types::GLint = 0;
            unsafe{
                gl.GetProgramiv(program_id,gl::INFO_LOG_LENGTH, &mut len);
            }
            let error: CString = create_whitespace_cstring_with_len(len as usize);
            unsafe {
                gl.GetProgramInfoLog(
                    program_id,
                    len,
                    std::ptr::null_mut(),
                    error.as_ptr() as *mut gl::types::GLchar
                );
            }
            return Err(error.to_string_lossy().into_owned());
        }
        // Detach shaders // required for shaders to be dropped //
        for shader in shaders {
            unsafe { gl.DetachShader(program_id, shader.id()); }
        }
        Ok(Program
            {
                gl: gl.clone(),
                id: program_id
            })
    }
    // Sets itself as the gl_program
    pub fn set_used(&self){
        unsafe {
            self.gl.UseProgram(self.id);
        }
    }
    // Getters //
    pub fn id(&self) -> gl::types::GLuint{
        self.id
    }
}
```

## Avoid memory leak

```rust
// Implement drop function call to C function //
impl Drop for Program{
    fn drop(&mut self) {
        unsafe {
            self.gl.DeleteProgram(self.id);
        }
    }
}
```


### Error handling

![[Error buffer#^3f92fb]]