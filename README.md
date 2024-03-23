## Commit 1 : Handle Request
Pada commit ini, saya membuat inisialisasi program rust untuk memberikan suatu response ke web server. Terdapat 2 method yang dibuat di commit ini, yaitu main dan handle_connection. Method handle_request digunakan untuk mengirim request ke web server. Method handle_request ini kurang lebih akan membaca parameter mut TcpStream yang nantinya akan diisi oleh local port number yaitu 127.0.0.1:7878. Method main digunakan untuk menjalankan program keseluruhan dan dalam hal ini, menyuruh handle_connection untuk mengirim request ke 127.0.0.1:7878. Ketika dibuka 127.0.0.1:7878, halaman chrome menampilkan pesan bahwa tidak ada data yang dikirim ke server tersebut karena memang kita belum membuat request nya. Response yang dikirim pada umumnya adalah berupa halaman HTML seperti website pada umumnya. 
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_vs_code_1.png)
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_chrome_output_1.png)

## Commit 2: Writing a Response and Returning HTML
Pada commit ini, saya membuat response terhadap request ke 127.0.0.1:7878 yang dibuat pada Commit 1. Pada method handle_request sekarang terdapat variabel status_line yang berfungsi sebagai status untuk response yang dikirim, yaitu 1.1 200 yang berarti berhasil. Selanjutnya juga ada variabel contents yang akan membaca input file html yang mau di return. Terdapat juga variabel length untuk memastikan bahwa jumlah parameter response yang diberikan valid memenuhi format:
1. HTTP Version Status Code CRLF Reason-Phrase
2. CRLF Header
3. Message Body

Terakhir, response akan dikirim dengan menggunakan:
- format!("{status_line}\r\nContent-Length: {length}\r\n\r\ {contents}");
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_html_page_2.png)
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_vs_code_2.png)

## Commit 3: Simulating Slow Response
Commit ketiga ini adalah menghandle slow response. Seringkali ketika kita melakukan request ke website, website terlalu lama dalam memberikan response karena masalah-masalah tertentu. Di commit ini, dilakukan sedikit modifikasi pada method handle_request yaitu jika dalam 5 detik website tidak memberikan response, maka akan langsung ditampilkan file 404.html. File ini saya buat untuk memberikan info bahwa request sedang tidak bisa diproses. Sebaliknya, jika dalam 5 detik response berhasil diberikan, maka akan di return file hello.html
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_html_not_found_.png)

## Commit 4: Improving throughput using thread pool and Sending Request to Threads Using Channel
Thread pool merupakan sekumpulan thread atau tester yang dipersiapkan untuk menunggu dan meng-handle suatu task. Pembuatan thread pool ini bertujuan untuk meng-improve throughput website atau aplikasi. Thread pool juga bertujuan untuk mencegah DoS (Denial of Service) attack. DoS merupakan suatu serangan siber yang menyebabkan suatu server down akibat adanya request yang berlebihan oleh pelaku sehingga menyebabkan server menjadi penuh. Dengan adanya thread pool, akan memungkinkan server untuk memproses lebih dari satu koneksi secara bersamaan sehingga meng-improve throughput.