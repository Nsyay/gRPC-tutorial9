### Reflection

1. Unary, server streaming, dan bi-directional streaming RPC adalah metode komunikasi yang digunakan dalam RPC (Remote Procedure Calls)
* Unary RPC adalah model request dan respone yang tergolong sederhana. Metode ini cocok digunakan jika client mengirim data yang kecil.
* Server streaming RPC adalah model dimana client mengirim sebuah request dan server merespon dengan banyak message. Metode ini cocok ketika server dibutuhkan untuk mengirim banyak data ke client, tetapi client tidak
* Bi-directional streaming RPC adalah model dimana client dan server mengirim message dua arah secara simultaneously. Metode ini cocok ketika client dan server sama-sama harus mengirimkan data secara berkelanjutan, sehingga dapat terjadi real-time communication dan data synchronization

2. Terdapat beberapa aspek sekuritas yang harus diperhatikan dalam implementasi gRPC, yaitu :
* Authentication --> pastikan bahwa client ter-otentikasi untuk melakukan komunikasi dengan menggunakan TLS (Transport Layer Security)
* Authorization --> Terapkan otorisasi untuk mengontrol hal-hal yang dapat dilakukan client setelah diautentikasi
* Data encryption --> melakukan enkripsi data yang lalu lalang antar client dan server, seperti end-to-end encryption

3. Beberapa isu yang dapat terjadi ketika menggunakan implementasi Bi-directional streaming terutama dalam aplikasi chat yaitu :
* Harus dapat dipastikan bahwa akses dapat dikelola secara bersamaan, memastikan konsistensi data, dan menghindari data races
* Memastikan bahwa koneksi client tetap terhubung dan bagaimana memberikan pesan ketika client akan disconnect
* Memastikan bahwa pesan yang dikirim secara bersamaan sesuai dengan urutan pengiriman
* Melakukan end-to-end encryption data untuk mencegah pencurian data sensitif

4. Menggunakan `tokio_stream::wrappers::ReceiverStream` memiliki keuntungan dan kerugian, diantaranya :
Keuntungan :
* Cocok untuk asynchronous gRPC service
* Fleksibel terhadap berbagai sumber data
* Mudah dikombinasikan dengan utilitas lain dari Tokio
Kerugian :
* Ada beberapa fitur yang tersedianya di Tonic gRPC framework
* Ada kemungkinan isu kompatibilitas dan peningkatan kompleksitas

5. untuk memfasilitasi code reuse, modularity, dan maintainability , gRPC menyediakan modul yang terstruktur, terdapat service separation juga yang memudahkan code reuse dan maintainability

6. Menurut saya, pada implementasi MyPaymentService dapat menggunakan metode lain seperti server streaming untuk data transaksi yang lebih banyak. Selain itu dapat juga diterapkan security yang mencegah akses yang tidak terautentikasi dan kebocoran data

7. Beberapa dampak penggunaan gRPC sebagai communication protocol, yaitu :
* gRPC menggunakan pendekatan contract-fist dengan interface dan kontrak ditentukan menggunakan Protocol Buffer
* penggunaan protocol buffer mengurangi ukuran payload dan dapat meningkatkan performa
* Mendukung banyak programming language
* Cocok untuk mocroservices architecture
* Menggunakan HTTP/2 sebagai transport protovol yang menyediakan fitur multiplexing, header compression, dan server push

8. HTTP/2 dibandingkan yang lain
Keuntungan :
* Mendukung multiplexing --> mengizinkan lebih dari satu request dan response secara asynchronous
* Mendukung header compression --> mengurangi overhead sending header information
* Mendukung server push --> server dapat secara aktif mengirim resource ke client bahkan sebelum di request
Kerugian :
* Lebih kompleks dibandingkan HTTP/1.1
* Memerlukan penggunaan memori dan processing power yang lebih banyak
* Beberapa web browser belum mendukung HTTP/2

9. Perbedaan REST APIs dengan gRPC dalam komunikasi yaitu gRPC lebih efisien dalam real-time communication tanpa perlu tambahan latency atau overhead

10. pendekatan berbasis skema gRPC dengan Protocol Buffers memiliki kelebihan seperti tipe data yang kuat, serialisasi yang efisien, dan penegakan skema, sehingga cocok digunakan untuk komunikasi yang mengutamakan performa dan memiliki tipe data yang jelas. Sementara itu, schema-less nature of JSON dalam payload REST API memberikan fleksibilitas, kemudahan penggunaan, dan interoperabilitas, yang membuatnya cocok untuk pengembangan yang cepat, struktur data yang bisa berubah-ubah, dan komunikasi yang mudah dimengerti. Pilihan antara kedua ini tergantung pada berbagai faktor seperti kebutuhan performa, kebutuhan pemodelan data, dan preferensi pengembangan
