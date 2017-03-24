# Shared Objects and Multiple Contexts 

Objects that may be shared between contexts include buffer objects, display lists, program and shader objects, renderbuffer objects, sampler objects, sync objects, and texture objects (except for the texture objects named zero).

Some of these objects may contain views (alternate interpretations) of part or all of the data store of another object. Examples are texture buffer objects, which contain a view of a buffer object’s data store, and texture views, which contain a
view of another texture object’s data store. Views act as references on the object whose data store is viewed.

Objects which contain references to other objects include framebuffer, program pipeline, query, transform feedback, and vertex array objects. Such objects are called container objects and are not shared.


### Object Deletion Behavior 

The share list is the group of all contexts which share objects. If a shared object is not explicitly deleted, then destruction of any individual context has no effect on that object unless it is the only remaining context in the share list. Once thelast context on the share list is destroyed, all shared objects, and all other resources allocated for that context or share list, will be deleted and reclaimed by the implementation as soon as possible.

When a buffer, texture, or renderbuffer object is deleted, it is unbound from any bind points it is bound to in the current context, and detached from any attachments of container objects that are bound to the current context.

When a buffer, texture, sampler, renderbuffer, query, or sync object is deleted, its name immediately becomes invalid (e.g. is marked unused), but the underlying object will not be deleted until it is no longer in use as below.

- the object is attached to any container object
- the object is bound to a context bind point in any context
- any other object contains a view of the data store of the object


When a shader object or program object is deleted, it is flagged for deletion, but its name remains valid until the underlying object can be deleted because it is no longer in use. A shader object is in use while it is attached to any program object.
A program object is in use while it is attached to any program pipeline object or is a current program in any context.

### Sync Objects and Multiple Contexts 

When multiple GL clients and/or servers are blocked on a single sync object and that sync object is signaled, all such blocks are released. The order in which blocks are released is implementation-dependent.

### Propagating Changes to Objects 

GL objects contain two types of information, data and state. Collectively these are referred to below as the contents of an object. For the purposes of propagating changes to object contents as described below, data and state are treated consis-
tently.

Data is information the GL implementation does not have to inspect, and does not have an operational effect. Currently, data consists of:

- Pixels in the framebuffer.
- The contents of the data stores of buffer objects, renderbuffers, and textures. 

State determines the configuration of the rendering pipeline, and the GL imple- mentation does have to inspect it.

In hardware-accelerated GL implementations, state typically lives in GPU registers, while data typically lives in GPU memory.

When the contents of an object T are changed, such changes are not always immediately visible, and do not always immediately affect GL operations involving that object.(5.3)


#### Determining Completion of Changes to an object 




