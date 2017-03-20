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
