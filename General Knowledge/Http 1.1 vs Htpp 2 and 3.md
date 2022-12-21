In HTTP 1.1 when have 1.1 keep alive mechanism
Pipelining response should be recieved one after another. subsequent request need wait completion

In 2015 released HTTP 2. Stream appeared, multiple stream can be send independent one from another, do no need recieved in the order
Transport layer issue - push notification

In 2020 released HTTP 3. Quick protocol based on UDP introduce stream as first class citizens of transport layer share one connection.

Package loss one of the stream not affect another stream. switching on one network to another on tcp is slugish.
Use Quick introduce connection Id
The network is different but connection id is the same, use the same network