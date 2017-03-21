# Introduction 
### What is the OpenGL Graphics System ?
> OpenGL (for “Open Graphics Library”) is an API (Application Programming Interface) to graphics hardware. 


### OpenGL Shading Language
>  OpenGL Shading Language Speciﬁcation deﬁnes the syntax and semantics of the programming language used to write shaders. 

### OpenGL ES
> OpenGL ES is a royalty-free, cross-platform API for full-function 2D and 3D graphics on embedded systems such as mobile phones, game consoles, and vehicles. It consists of well-deﬁned subsets of OpenGL. Each version of OpenGL ES implements a subset of a corresponding OpenGL version.

| OpenGL ES Version  | OpenGL Version it subsets |
| ------------- | ------------- |
| OpenGL ES 1.1 | OpenGL 1.5  |
| OpenGL ES 2.0  | OpenGL 2.0  
| OpenGL ES 3.0  | OpenGL 3.3  |
| OpenGL ES 3.1  | OpenGL 4.3  |

### OpenGL ES Shading Language 
> These documents deﬁne versions of the OpenGL Shading Language designed for implementations of OpenGL ES 2.0, 3.0, and 3.1 respectively, but also supported by OpenGL implementations. 

### WebGL 
> WebGL is a cross-platform, royalty-free web standard for a low-level 3D graphics API based on OpenGL ES. Developers familiar with OpenGL ES will recognize WebGL as a shader-based API using the OpenGL Shading Language, with con-
structs that are semantically similar to those of the underlying OpenGL ES API.

### Window System Bindings 
> OpenGL requires a companion API to create and manage graphics contexts, windows to render into, and other resources beyond the scope of this Speciﬁcation.There are several such APIs supporting different operating and window systems.
1. GLX - X Window System Bindings
2. WGL - Microsoft Windows Bindings
3. MacOS X Window System Bindings (CGL,AGL)
4. EGL - Mobile and Embedded Device Bindings 

### OpenCL (Open Computing Language)
>OpenCL is an open, royalty-free standard for cross-platform, general-purpose parallel programming of processors found in personal computers, servers, and mobile devices, including GPUs. OpenCL deﬁnes interop methods to share OpenCL memory and image objects with corresponding OpenGL buffer and texture objects, and to coordinate control of and transfer of data between OpenCL and OpenGL. This allows applications to split processing of data between OpenCL and OpenGL; for example, by using OpenCL to implement a physics model and then rendering and interacting with the resulting dynamic geometry using OpenGL.


# OpenGL Fundamentals 

### Execution Model 
> OpenGL is concerned only with processing data in GPU memory, including rendering into a framebuffer and reading values stored in that framebuffer.

> The GL draws primitives processed by a variety of shader programs and ﬁxed function processing units controlled by context state. Each primitive is a point,line segment, patch, pixel rectangle, or polygon. Context state may be changed independently; the setting of one piece of state does not affect the settings of others.

> Primitives are deﬁned by a group of one or more vertices. A vertex deﬁnes a point, an endpoint of a line segment, or a corner of a polygon where two edges meet. Data such as positional coordinates, colors, normals, texture coordinates, etc. are associated with a vertex and each vertex is processed independently, in order, and in the same way. 

> Commands are always processed in the order in which they are received, although there may be an indeterminate delay before the effects of a command are realized. This means, for example, that one primitive must be drawn completely before any subsequent one can affect the framebuffer. 

> Data binding occurs on call. This means that data passed to a GL command are interpreted when that command is received.  

> The GL provides direct control over the fundamental operations of 3D and 2D graphics. This includes speciﬁcation of parameters of application-deﬁned shader programs performing transformation, lighting, texturing, and shading operations, as well as built-in functionality such as antialiasing and texture ﬁltering. It does not provide a means for describing or modeling complex geometric objects, although shaders can be written to generate such objects.

> The model for interpretation of GL commands is client-server. That is, a program (the client) issues commands, and these commands are interpreted and processed by the GL (the server). The server may or may not operate on the same computer or in the same address space as the client. In this sense, the GL is network transparent. A server may maintain a number of GL contexts, each of which is an encapsulation of current GL state and objects. A client may choose to be made current to any one of these contexts.

   There are two classes of framebuffers: a window system-provided framebuffer associated with a context when the context is made current, and application-created framebuffers. The window system-provided framebuffer is referred to as the default framebuffer. Application created framebuffers, referred to as framebuffer objects, may be created as desired。

 ### Command Syntax 
 
> The Speciﬁcation describes OpenGL commands as functions or procedures using ANSI C syntax. 

    void Uniform4f( int location, float v0, float v1, float v2, float v3 );
    void GetFloatv( enum pname, float *data );
    
| Type Descriptor  | Corresponding GL Type |
| ------------- | ------------- |
| b | byte  |
| s | short  |
| i | int  |
| i64 | int64  |
| f | float  |
| d | double| 
| ub | ubyte|
| us | ushort|
| ui | uint|
| ui64 | uint64|

###　Command Execution

>Most of the Speciﬁcation discusses the behavior of a single context bound to a single CPU thread. It is also possible for multiple contexts to share GL objects and for each such context to be bound to a different thread. 

>The GL detects only a subset of those conditions that could be considered errors.This is because in many cases error checking would adversely impact the performance of an error-free program.

enum GetError( void );
 
#### Flush and Finish

Implementations may buffer multiple commands in a command queue before sending them to the GL server for execution. This may happen in places such as the network stack (for network transparent implementations), CPU code executing as part of the GL client or the GL server, or internally to the GPU hardware. Coarse control over command queues is available using the command

 void Flush( void ); 
 
 void Finish( void ); 
 
 forces all previously issued GL commands to complete. Finish does not return until all effects from such commands on GL client and server state and the framebuffer are fully realized.
