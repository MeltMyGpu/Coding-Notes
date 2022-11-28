#Functionality 
### Back Links


# Content
Shader are small, self contained programs that run on your gpu during each step of [[The graphics pipeline]]. 
Although many of the shaders have default implementations that you either cannot change yourself, or you often won't need to, there are no default implementations of the **vertex shader** or **fragments shader.** You are required to provide OpenGL with your own implementation of these, either compiled from a hardcoded CStribg or loaded from a file into a CStribg. 
Shaders must be compiled before from source code by the hardware that will be running them, therefore this is handled by the OpenGL API. Presumably this is done because different hardware will require the shaders to be complied in different ways, so abstracting this to the API allows hardware creators to implement the specific detail without requiring the developer to provide different source code.

Compiled shaders must then be linked with a [[Shader program]] before being used by OpenGL to render anything.