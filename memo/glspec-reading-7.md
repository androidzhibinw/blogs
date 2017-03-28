
# Programs and Shaders 

A shader specifies operations that are meant to occur on data as it moves through different programmable stages of the OpenGL processing pipeline, starting with vertices specified by the application and ending with fragments prior to being written to the framebuffer.

To use a shader, shader source code is first loaded into a shader object and then compiled. A shader object corresponds to a stage in the rendering pipeline referred to as its shader stage or shader type.


One or more shader objects are attached to a program object. The program object is then linked, which generates executable code from all the compiled shader objects attached to the program.

Shader stages including vertex shaders, tessellation control shaders, tessellation evaluation shaders, geometry shaders, fragment shaders, and compute shaders can be created, compiled, and linked into program objects.

Vertex shaders describe the operations that occur on vertex attributes. Tessellation control and evaluation shaders are used to control the operation of the tessellator. Geometry shaders affect the processing of primitives assembled from vertices. Fragment shaders affect the processing of fragments during rasterization . A single program object can contain all of these shaders, or any subset thereof.
