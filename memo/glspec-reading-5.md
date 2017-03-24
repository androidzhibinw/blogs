# Shared Objects and Multiple Contexts 

Objects that may be shared between contexts include buffer objects, display lists, program and shader objects, renderbuffer objects, sampler objects, sync objects, and texture objects (except for the texture objects named zero).

Some of these objects may contain views (alternate interpretations) of part or all of the data store of another object. Examples are texture buffer objects, which contain a view of a buffer object’s data store, and texture views, which contain a
view of another texture object’s data store. Views act as references on the object whose data store is viewed.

Objects which contain references to other objects include framebuffer, program pipeline, query, transform feedback, and vertex array objects. Such objects are called container objects and are not shared.

