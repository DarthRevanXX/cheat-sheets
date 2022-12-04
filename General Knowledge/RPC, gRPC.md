Open source remote procedure framework created by Google in 2016.
A local procedure call is a function call within a process to execute some code.
A remote procedure can enables  one machine to invoke some code on another machine as if it is a local function call from user's perspective. gRPC is a popular implementation of RPC.
The core of this ecosystem is the use of Protocol Buffers as its data interchange format.
Encoding structure to data. gRPC uses Protocol Buffers to encode and send data over the wire by default. 
Protocol Buffers advantages:
 - support strongly-typed schema definitions.(proto file)
 - high performance out of the box(very efficient binary encoding), HTTP/2 (Uses Http Stream)