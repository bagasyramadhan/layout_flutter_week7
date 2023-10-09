## Nama : Muhammad Bagas Ramadhan
## Kelas : 3G
## NIM : 2141720120

# Praktikum 1: Membangun Layout di Flutter

## Langkah 1: Buat Project Baru


## Langkah 2: Buka file lib/main.dart
### Buka file main.dart lalu ganti dengan kode berikut. Isi nama dan NIM Anda di text title.
```
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter layout: Nama dan NIM Anda',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Flutter layout demo'),
        ),
        body: const Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

### Hasil
![](ss/1helloworld.png)

## Langkah 3: Identifikasi layout diagram
Pada langkah ini dilakukan pemecahan layout menjadi elemen dasarnya:

• Identifikasi baris dan kolom

• Apakah tata letaknya menyertakan kisi-kisi (grid)?  

• Apakah ada elemen yang tumpang tindih?

• Apakah UI memerlukan tab?

• Perhatikan area yang memerlukan alignment, padding, atau borders.

Dalam konteks ini, pengaturan elemen menjadi satu kolom terdiri dari gambar, dua baris, dan satu blok teks menjadi perhatian utama. Selanjutnya, kita akan membuat diagram untuk setiap baris ini.

Baris pertama, yang kita sebut sebagai "Judul", terdiri dari tiga komponen: sebuah kolom teks, sebuah ikon bintang, dan sebuah angka. Bagian pertama dari kolom ini memiliki dua baris teks. Kolom pertama ini mengambil banyak ruang, sehingga perlu ditempatkan dalam sebuah widget yang dapat diperluas.

Baris kedua, yang kita namakan "Tombol", juga terdiri dari tiga elemen: masing-masing adalah kolom yang berisi ikon dan teks.

## Langkah 4: Implementasi title row
Menambahkan kode berikut di bagian atas metode build() di dalam kelas MyApp:
``` 
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  MyApp({super.key});

  Widget titleSection = Container(
    padding: EdgeInsets.all(32),
    child: Row(
      children: [
        Expanded(
          /* soal 1*/
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              /* soal 2*/
              Container(
                padding: const EdgeInsets.only(bottom: 8),
                child: const Text(
                  'Wisata Cafe di Batu',
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              const Text(
                'Batu, Malang, Indonesia',
                style: TextStyle(color: Colors.grey),
              ),
            ],
          ),
        ),
        /* soal 3*/
        const Icon(Icons.star, color: Colors.red),
        const Text('41'),
      ],
    ),
  );

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter layout: Muhammad Bagas Ramadhan - 2141720120',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Flutter layout demo'),
        ),
        body: Column(
          children: [
            titleSection,
          ],
        ),
      ),
    );
  }
}
```

Dari kode di atas sudah lengkah dan sudah memenuhi spesifikasi soal yang diminta, yang mana penjelasannya sebagai berikut:

Soal 1 meminta untuk meletakkan widget Column di dalam widget Expanded. Selanjutnya diminta untuk menambahkan properti crossAxisAlignment ke CrossAxisAlignment.start sehingga posisi kolom berada di awal baris.

Soal 2 meminta untuk meletakkan baris pertama teks di dalam Container, dengan padding = 8, dengan teks 'Batu, Malang, Indonesia' di dalam Column, set warna menjadi abu-abu.

Soal 3 meminta memberikan 2 item, yaitu icon bintang dan teks '41', dengan warna merah untuk icon, dan memberi padding tepi sebesar 32 piksel. 

### Hasil
![](ss/2wisata.png)

# Praktikum 2: Implementasi button row

## Langkah 1: Buat method Column _buildButtonColumn

Setelah ditambahkan method _buildButtonColumn ke dalam method build(), maka kode didalam method build() menjadi seperti kode berikut:
```
Widget build(BuildContext context) {
    Color color = Theme.of(context).primaryColor;

    Column _buildButtonColumn(Color color, IconData icon, String label) {
      return Column(
        mainAxisSize: MainAxisSize.min,
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Icon(icon, color: color),
          Container(
            margin: const EdgeInsets.only(top: 8),
            child: Text(
              label,
              style: TextStyle(
                fontSize: 12,
                fontWeight: FontWeight.w400,
                color: color,
              ),
            ),
          ),
        ],
      );
    }
  }
```

## Langkah 2: Buat widget buttonSection
Widget buttonSection telah ditambahkan untuk memasukkan ikon langsung ke dalam kolom. Teks tersebut terletak di dalam Container dengan margin hanya di bagian atas, yang berfungsi sebagai pemisah antara teks dan ikon. Kode di bawah ini digunakan untuk membuat baris yang berisi kolom-kolom dengan memanggil fungsi dan mengatur warna, ikon, dan teks sesuai dengan parameter yang diberikan untuk setiap kolom. Penggunaan 'MainAxisAlignment.spaceEvenly' bertujuan untuk menyusun kolom-kolom tersebut sehingga memiliki jarak yang sama di antara mereka.

```
Widget buttonSection = Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: <Widget>[
        _buildButtonColumn(
            const Color.fromRGBO(33, 150, 243, 1), Icons.call, 'CALL'),
        _buildButtonColumn(Colors.blue, Icons.near_me, 'ROUTE'),
        _buildButtonColumn(Colors.blue, Icons.share, 'SHARE'),
      ],
    );
```

## Langkah 3: Tambah button section ke body
```
body: Column(
          children: [
            titleSection,
            buttonSection,
          ],
        ),
```

### Hasil
![](ss/3icon.png)

## Praktikum 3: Implementasi text section

## Langkah 1: Buat widget textSection

Membuat widget textSection ke dalam method build()

```
Widget textSection = Container(
      padding: const EdgeInsets.all(32),
      child: const Text(
        'Cafe Sawah Pujon Kidul adalah tempat wisata yang terletak di desa Pujon Kidul, Malang, Jawa Timur, Indonesia. ditulis oleh Muhammad Bagas Ramadhan - 2141720120. Tempat ini menawarkan pengalaman unik dengan suasana alam yang asri, terutama sawah-sawah yang indah. Pengunjung dapat menikmati minuman dan makanan di tengah pemandangan hijau sawah, membuatnya menjadi destinasi yang populer untuk bersantai, berfoto, dan menikmati alam. Cafe Sawah Pujon Kidul adalah tempat yang sempurna untuk melarikan diri dari kehidupan perkotaan dan menikmati ketenangan pedesaan sambil menikmati hidangan lezat.',
        softWrap: true,
        textAlign: TextAlign.justify,
      ),
    );
```

## Langkah 2: Tambahkan variabel text section ke body

```
body: Column(
          children: [
            titleSection,
            buttonSection,
            textSection,
          ],
        ),
```
### Hasil
![](ss/4texts.png)

## Tambahan
Untuk menambahkan gambar ke dalam body, yang terletak sebelum titleSection, maka dapat dilakukan dengan mengubah widget Column menjadi ListView untuk membuat daftar atau tampilan berulang yang dapat dilakukan *scroll* secara vertikal ataupun horizontal. Kemudian di dalam List Widget children, manambahkan sebuah gambar yang di *load* dari folder assets, yang sebelumnya telah dibuat dan juga didefinisikan pada pubspec.yaml

```
body: ListView(
          children: [
            Image.asset('assets/pujonkidul.png'),
            titleSection,
            buttonSection,
            textSection,
          ],
        ),
```

### Hasil
![](ss/5foto.png)
