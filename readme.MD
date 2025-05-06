Reflection  

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?  

Ans:  
Unary adalah salah satu tipe RPC di mana client hanya mengirim single request dan menerima single respons, artinya client hanya bisa mengirim satu data ke server dan menunggu responsnya  

Server Streaming adalah tipe RPC di mana server dapat mengirimkan stream of respons ke client  

Bidirectional streaming merupakan tipe RPC yang di mana client maupun server bisa mengirim multiple messages dalam stream yang kontinu, artinya ini membuat komunikasinya menjadi real-time dua arah antara server dan client  

Masing-masing tipe memiliki keunggulan, misalnya Unary cocok untuk case ketika kita ingin fecth single item dari db (auth sebuah user, dll), Server Streaming cocok ketika server perlu memberikan update data/informasi secara berkala ke user (misal: update harga saham), dan Bi-directional cocok untuk case yang membutuhkan komunikasi dua arah yang interaktif, seperti real time message antar client dan server, real-time analytics, dan lain-lain.  

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?  

Ans:  
Untuk authentication, perlu beberapa metode yang sudah cukup sering digunakan, misal JWT atau OAuth2, selain itu diperlukan juga authorization untuk membatasi hak akses, dan terakhir penggunaan TLS untuk enskripsi data untuk menjaga kerahasiaan selama transmisi informasi  

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?  

Ans:  
Challenges yang mungkin akan muncul adalah masalah concurrency, di mana ketika kedua pihak (server dan client) mengirim pesan secara bersamaan, maka akan terjadi potensi race condition atau deadlock jika tidak ditangani dengan benar. Beberapa hal seperti backpressure, flow control, dan cancellation juga perlu diperhatikan  

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?  

Ans:  
Keuntungannya adalah kemudahan dalam ngeconvert tokio::sync::mpsc::Receiver menjadi stream asynchronoues, selain itu implementasi dan maintain logic dari asynchronousnya juga akan lebih mudah. Kekurangannya, buffer management menjadi issue jika tidak ditangani dengan baik. Misalnya ketika producer generate pesan lebih cepat daripada consumer ngeproses pesan tersebut, maka akan terjadi backpressure

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?  

Ans:  
Struktur yang ideal adalah dengan memisahkan module sesuai servicenya, mengabstrak common functionalities, dan memisah interface dengan implementasinya  

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?  

Ans:  
Untuk payment yang lebih kompleks, bisa menambah validasi pada data payment, integrasi dengan external payment gateway, dan handling konfirmasi transaksi asynchronus  

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?  

Ans:  
Dampak penggunaan gRPC adalah peningkatan performa secara signifikan, karena gRPC menggunakan protocl buffers untuk serialisasi biner yang lebih efisien ketimbang json/xml dan HTTP/2 untuk multiplexing, bidirectional streaming dan lain-lain  

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?  

Ans:  
Keuntungan menggunakan HTTP/2 adalah menawarkan multiplexing yang memungkinan pengiriman beberapa permintaan/respons secara paralel melalui single connection, namun ada trade off yakni implementasi dan debugging-nya akan lebih kompleksnya ketimbang HTTP/2  

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?  

Ans:  
REST API menggunakan request-response model yang berarti client mengirim request dan menunggu respons (satu arah), sedangkan gRPC (khususnya bidirectional streaming) memungkinkan klien dan server melakukan komunikasi secara real-time dan interaktif  

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?  

Ans:  
Menggunakan protocl buffers memberikan keuntungan dari sisi performa yang tinggi dan validation type yang ketat, sebaliknya JSON memberikan fleksibilitas tinggi dalam penggunaan namun dengan trade-off overhead performa