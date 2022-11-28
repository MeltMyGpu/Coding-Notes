#Implementation #NeedsFillingOrNotes 

### Back links


## Overview



## Implementation

```rust
/// <summary> Creates a whitespace CString buffer with given length </summary>
fn create_whitespace_cstring_with_len(len: usize) -> CString {
    // allocate buffer size
    let mut buffer: Vec<u8> = Vec::with_capacity(len as usize +1);
    //fill with whitespace
    buffer.extend([b' '].iter().cycle().take(len as usize));
    // convert buffer to CString and return
    unsafe { CString::from_vec_unchecked(buffer)}
}
```

^3f92fb
