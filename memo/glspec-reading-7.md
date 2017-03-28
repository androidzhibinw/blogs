
# Programs and Shaders 

A shader specifies operations that are meant to occur on data as it moves through different programmable stages of the OpenGL processing pipeline, starting with vertices specified by the application and ending with fragments prior to being written to the framebuffer.

To use a shader, shader source code is first loaded into a shader object and then compiled. A shader object corresponds to a stage in the rendering pipeline referred to as its shader stage or shader type.


One or more shader objects are attached to a program object. The program object is then linked, which generates executable code from all the compiled shader objects attached to the program.

Shader stages including vertex shaders, tessellation control shaders, tessellation evaluation shaders, geometry shaders, fragment shaders, and compute shaders can be created, compiled, and linked into program objects.

Vertex shaders describe the operations that occur on vertex attributes. Tessellation control and evaluation shaders are used to control the operation of the tessellator. Geometry shaders affect the processing of primitives assembled from vertices. Fragment shaders affect the processing of fragments during rasterization . A single program object can contain all of these shaders, or any subset thereof.

Compute shaders perform general-purpose computation for dispatched arrays of shader invocations , but do not operate on primitives processed by the other shader types.

Shaders can reference several types of variables as they execute. *Uniforms*  are per-program variables that are constant during program execution.*Buffer variables* are similar to uniforms, but are stored in buffer object memory which may be written to, and is persistent across multiple shader invocations. *Subroutine uniform variables* are similar to uniforms but are context state, rather than program object state.*Samplers* are a special form of uniform used for texturing, *Images* are a special form of uniform identifying a level of a texture to be accessed using built-in shader functions.*Output variables* hold the results of shader execution that are used later in the pipeline.

### Shader Objects 

To create a shader object, use the command:

    uint CreateShader( enum type );
    
The shader object is empty when it is created. The type argument specifies the type of shader object to be created and must be one of the values in table indicating the corresponding shader stage. A non-zero name that can be used to reference the
shader object is returned. 

| type        | Shader Stage    |   
| ------------- |:-------------:|
| VERTEX_SHADER     | Vertex shader| 
| TESS_CONTROL_SHADER | Tessellation control shader|
|TESS_EVALUATION_SHADER |Tessellation evaluation shader |
| GEOMETRY_SHADER|Geometry shader|
|FRAGMENT_SHADER|Fragment shader|
|COMPUTE_SHADER| Compute shader|

    void ShaderSource( uint shader, sizei count, const char * const *string, const int *length );
    
The command *ShaderSource* loads source code into the shader object named shader.The ShaderSource command sets the source code for the shader to the text strings in the string array.

Once the source code for a shader has been loaded, a shader object can be compiled with the command *CompileShader* 

    void CompileShader( uint shader );
    
Each shader object has a boolean status, COMPILE_STATUS , that is modified as a result of compilation. This status may be queried with *GetShaderiv*. This status will be set to TRUE if shader was compiled without errors and is ready for use, and FALSE otherwise. Compilation can fail for a variety of reasons as listed in the OpenGL Shading Language Specification. 


Each shader object has an information log, which is a text string that is over- written as a result of compilation. This information log may be queried with *GetShaderInfoLog* to obtain more information about the compilation attempt.


Shader objects can be deleted with the command *DeleteShader*:

    void DeleteShader( uint shader );

If shader is not attached to any program object, it is deleted immediately. Otherwise, shader is flagged for deletion and will be deleted when it is no longer attached to any program object. If an object is flagged for deletion, its boolean status bit DELETE_STATUS is set to true.

### Shader Binaries 

Precompiled shader binaries may be loaded with the command *ShaderBinary*:

    void ShaderBinary( sizei count, const uint *shaders, enum binaryformat, const void *binary, sizei length );
    
### Program Objects 

A program object is created with the command *CreateProgram*: 

    uint CreateProgram( void );
    
Program objects are empty when they are created. A non-zero name that can be used to reference the program object is returned. If an error occurs, zero will be returned.

To attach a shader object to a program object, use the command *AttachShader*:

    void AttachShader( uint program, uint shader );

Shader objects may be attached to program objects before source code has been loaded into the shader object, or before the shader object has been compiled. Multiple shader objects of the same type may be attached to a single program object, and a single shader object may be attached to more than one program object.

To detach a shader object from a program object, use the command *DetachShader*:

    void DetachShader( uint program, uint shader );
    
In order to use the shader objects contained in a program object, the program object must be linked. The command *LinkProgram*:

    void LinkProgram( uint program );

This command will link the program object named program. Each program object has a boolean status, LINK_STATUS , that is modified as a result of linking. This status may be queried with *GetProgramiv*.

Each program object has an information log that is overwritten as a result of alink operation. This information log may be queried with *GetProgramInfoLog* to obtain more information about the link operation or the validation information.


If a program has been linked successfully by *LinkProgram* it can be made part of the current rendering state for all shader stages with the command *UseProgram*:
 
    void UseProgram( uint program );
    
If program is non-zero, this command will make program the current program object. This will install executable code as part of the current rendering state for each shader stage present when the program was last linked successfully.


#### Program Interfaces 

When a program object is made part of the current rendering state, its executable code may communicate with other GL pipeline stages or application code through a variety of interfaces. When a program is linked, the GL builds a list of active
resources for each interface. Examples of active resources include variables, interface blocks, and subroutines used by shader code.

The GL provides a number of commands to query properties of the interfaces of a program object. Each such command accepts a programInterface token, identifying a specific interface. The supported values for programInterface are as follows:

- UNIFORM corresponds to the set of active uniform variables
- UNIFORM_BLOCK corresponds to the set of active uniform blocks
- ATOMIC_COUNTER_BUFFER corresponds to the set of active atomic counter buffer binding points
- PROGRAM_INPUT corresponds to the set of active input variables used by the first shader stage of program
- PROGRAM_OUTPUT corresponds to the set of active output variables used by the last shader stage of program
- others ... 

