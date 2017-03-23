# Dataflow Model 


 Below shows a block diagram of the GL. Some commands specify geometric objects to be drawn while others specify state controlling how objects are handled by the various stages, or specify data contained in textures and buffer objects.

 ![Dataflow Fig](./glspec-dataflow.png)
 
 The ﬁrst stage assembles vertices to form geometric primitives such as points,line segments, and polygons. In the next stage vertices may be transformed and lit,followed by assembly into geometric primitives. Tessellation and geometry shaders may then generate multiple primitives from a single input primitive. Optionally, the results of these pipeline stages may be fed back into buffer objects using transform feedback.
 

 
