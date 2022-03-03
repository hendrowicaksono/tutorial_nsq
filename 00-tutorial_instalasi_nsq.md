---
Title: Tutorial instalasi NSQ  
Author: Hendro Wicaksono 
Date: 2 Maret 2022
Comment: Sembar iseng belajar markdown.
---

# Tutorial Instalasi [NSQ]

## Apa itu [NSQ]

- Perangkat lunak untuk kebutuhan *messaging service*.
- Perangkat lunak sejenis selain NSQ: [Apache Kafka](https://kafka.apache.org/) dan [RabbitMQ](https://www.rabbitmq.com/).

## Kenapa *messaging service*
- Membantu proses didalam sistem menjadi _**asynchronous**_.
- Meningkatkan kehandalan layanan.
- Membantu proses didalam sistem melakukan proses secara paralel.

## Kenapa [NSQ]
- Pendekatan terdistribusi untuk meningkatkan kehandalan dan ketersediaan (*availability*).
- Ringan, cepat.
- Mudah diinstal dan dikelola.
- Tersedia antar muka untuk monitoring berbasis web.
- Message *Producing/Publishing* berbasis [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).
- Dukungan *driver* untuk banyak bahasa pemrogaman. 

## Langkah Instalasi

### Asumsi
- Instalasi dilakukan di Linux [Ubuntu](https://ubuntu.com/) 20.04.
- *Home Directory* adalah `/home/users`.
- Instalasi dilakukan didalam *Home Directory*.

### Unduh [NSQ]

Unduh [NSQ] dari [Halaman unduh](https://nsq.io/deployment/installing.html), pilih versi paling baru yang sesuai dengan arsitektur server. Misalnya: [Versi 1.2.1](https://s3.amazonaws.com/bitly-downloads/nsq/nsq-1.2.1.linux-amd64.go1.16.6.tar.gz).

### Ekstrak [NSQ]

- Buat folder `message_broker`.
- Ekstrak file [unduhan NSQ](https://s3.amazonaws.com/bitly-downloads/nsq/nsq-1.2.1.linux-amd64.go1.16.6.tar.gz) didalam folder `message_broker`. Kemudian _rename_ folder hasil ekstrak [unduhan NSQ](https://s3.amazonaws.com/bitly-downloads/nsq/nsq-1.2.1.linux-amd64.go1.16.6.tar.gz), menjadi _nsq_ (alasan kesederhanaan saja).

### Menjalankan service [NSQ]
- Bikin folder `run` didalam folder `message_broker`. Folder `run` ini yang akan menyimpan file log dll yang akan di-generate saat service [NSQ] dijalankan.

- Masuk ke folder `run`.
```sh
  cd run
```

- Jalankan service `nsqlookupd`:
```sh
  ../nsq/bin/nsqlookupd
```

- Jalankan service `nsqd`:
```sh
  ../nsq/bin/nsqd --lookupd-tcp-address=127.0.0.1:4160
```

- Jalankan service `nsqadmin` untuk kemudahan monitoring:
```sh
  ../nsq/bin/nsqadmin --lookupd-http-address=127.0.0.1:4161
```

- Untuk menjalankan service [NSQ], sebagai *background*, jalankan seperti ini:
```sh
  ../nsq/bin/nsqlookupd &
```
```sh
  ../nsq/bin/nsqd --lookupd-tcp-address=127.0.0.1:4160 &
```
```sh
  ../nsq/bin/nsqadmin --lookupd-http-address=127.0.0.1:4161 &
```

### Tes kirim message ke [NSQ]

Dengan curl coba *produce/publish* message dengan metode **POST**:
```sh
curl -d 'Halo dunia!' 'http://127.0.0.1:4151/pub?topic=test'
```

Jika berhasil nanti muncul karakter **OK** yang menandakan pesan sudah diterima oleh [NSQ].

Monitoring berbasis web bisa diakses pada URL http://127.0.0.1:4171/.

## Apa berikutnya?

Berikutnya kita belajar cara *consume/subscribe* ke [NSQ] pada artikel berikutnya.

Selamat mencoba!

[NSQ]: <https://nsq.io/>
