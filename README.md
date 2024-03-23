## Commit 1 : Handle Request
Pada commit ini, saya membuat inisialisasi program rust untuk memberikan suatu response ke web server. Terdapat 2 method yang dibuat di commit ini, yaitu main dan handle_connection. Method handle_request digunakan untuk mengirim request ke web server sedangkan method main digunakan untuk menjalankan program keseluruhan dan dalam hal ini, menyuruh handle_connection untuk mengirim request ke 127.0.0.1:7878. Ketika dibuka 127.0.0.1:7878, halaman chrome menampilkan pesan bahwa tidak ada data yang dikirim ke server tersebut karena memang kita belum membuat request nya
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_vs_code_1.png)
![](https://github.com/LesmanaArya/tutorial-rust/blob/main/img/ss_chrome_output_1.png)
