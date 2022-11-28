#Implementation #NeedsFillingOrNotes 

### Back links
[[Shader Struct]]
[[Shaders]]




## Examples

```rust 
fn shaders_from_source(
    gl: &gl::Gl,
    source : &CStr,
    kind: gl::types::GLuint
) -> Result<gl::types::GLuint, String> {
    // obtain shader id
    let id = unsafe {gl.CreateShader(kind)};
    // call to OpenGL to source and complie the shader
    unsafe{
        gl.ShaderSource(id,1,&source.as_ptr(), std::ptr::null());
        gl.CompileShader(id);
    }
    // Error message info fetch and setup
    let mut success: gl::types::GLint = 1;
    unsafe{
        gl.GetShaderiv(id, gl::COMPILE_STATUS, &mut success);
    }
    if success == 0{
        let mut len: gl::types::GLint = 0;
        unsafe{
            gl.GetShaderiv(id, gl::INFO_LOG_LENGTH, &mut len)
        }
        let error:CString = create_whitespace_cstring_with_len(len as usize);
        // write shader log
        unsafe{
            gl.GetShaderInfoLog(
                id,
                len,
                std::ptr::null_mut(),
                error.as_ptr() as *mut gl::types::GLchar
            );
        }
        // returns CString as rust String
        return Err(error.to_string_lossy().into_owned());
    }
    Ok(id)
}
```

### Error handling
![[Error buffer#^3f92fb]]