# Buffer Objects

Buffer objects contain a data store holding a fixed-sized allocation of server memory. This chapter specifies commands to create, manage, and destroy buffer objects.


    void GenBuffers( sizei n, uint *buffers );
  
The command GenBuffers returns n previously unused buffer object names in buffers. These names are marked as used, for the purposes of GenBuffers only, but they acquire buffer state
only when they are first bound with BindBuffer (see below), just as if they were unused.

    void CreateBuffers( sizei n, uint *buffers );
    
    
CreateBuffers returns n previously unused buffer names in buffers, each representing a new buffer object initialized as if it had been bound to an unspecified
target.


    void DeleteBuffers( sizei n, const uint *buffers );

Buffer objects are deleted by calling DeleteBuffers, buffers contains n names of buffer objects to be deleted. After a buffer object is
deleted it has no contents, and its name is again unused.


### Creating and Binding Buffer Objects 

A buffer object is created by binding an unused name to a buffer target. The binding is effected by calling

    void BindBuffer( enum target, uint buffer );
   
BindBuffer may also be used to bind an existing buffer object. If the bind is successful no change is made to the state of the newly bound buffer object, and any
previous binding to target is broken.


