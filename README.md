Checklist untuk tugas ini adalah sebagai berikut:

1. Membuat sebuah program Flutter baru dengan tema inventory seperti tugas-tugas sebelumnya.

Pertama-tama saya menginisialisasi project flutter baru di direktori C dengan menjalankan perintah berikut di command prompt.

flutter create enkom_kw_mobile
cd enkom_kw_mobile

Lalu, saya menginisialisasi repository di GitHub dengan menjalankan perintah sebagai berikut:

git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/budf93/EnKomKWMobile.git
git push -u origin main

Lalu, saya merapikan struktur proyek dengan pertama-tama menambahkan kode ini di baris pertama berkas baru menu.dart di direktori enkom_kw_mobile/lib

import 'package:flutter/material.dart';

Lalu, saya menambahkan kode baris ke-39 sampai akhir pada berkas main.dart ke file menu.dart yang baru saja dibuat. 

Lalu, saya menambahkan kode berikut di awal file main.dart untuk menghilangkan error pada line ke-34 pada file main.dart.

import 'package:shopping_list/menu.dart';

2. Membuat tiga tombol sederhana dengan ikon dan teks untuk:

Melihat daftar item (Lihat Item)
Menambah item (Tambah Item)
Logout (Logout)

Pertama-tama, saya menambahkan kode berikut pada main.dart untuk mengubah warna aplikasi menjadi indigo.

colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),

Lalu, saya mengubah sifat widget halaman saya menjadi stateless dengan mengubah MyHomePage(title: 'Flutter Demo Home Page') menjadi MyHomePage().

Lalu, pada file menu.dart, saya mengubah sifat widget halaman dari stateful menjadi stateless dengan cara mengubah bagian ({super.key, required this.title}) menjadi ({Key? key}) : super(key: key); dan menghapus final String title; sampai bawah serta menambahkan Widget build sehingga kode terlihat seperti di bawah:

class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            ...
        );
    }
}   

Tidak lupa saya menghapus fungsi State yang ada dibawah bagian stateless widget ini.

Setelah mengubah sifat widget halaman menu menjadi stateless, saya akan menambahkan teks dan card untuk memperlihatkan barang yang dijual.

Pertama-tama, Untuk menambahkan teks dan card, saya menambahkan barang-barang yang dijual. saya memulai dengan define tipe pada list saya dengan cara menambahkan kode berikut.

class ShopItem {
  final String name;
  final IconData icon;

  ShopItem(this.name, this.icon);
}

Lalu dibawah kode MyHomePage({Key? key}) : super(key: key);, saya menambahkan barang-barang yang dijual (nama, harga, dan icon barang tersebut).

final List<ShopItem> items = [
    ShopItem("Lihat Item", Icons.checklist),
    ShopItem("Tambah Item", Icons.add_shopping_cart),
    ShopItem("Logout", Icons.logout),
];

Selanjutnya saya menambahkan kode dibawah ini didalam Widget build.

return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Shopping List',
        ),
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'PBP Shop', // Text yang menandakan toko
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((ShopItem item) {
                  // Iterasi untuk setiap item
                  return ShopCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );  

3. Memunculkan Snackbar dengan tulisan:

"Kamu telah menekan tombol Lihat Item" ketika tombol Lihat Item ditekan.
"Kamu telah menekan tombol Tambah Item" ketika tombol Tambah Item ditekan.
"Kamu telah menekan tombol Logout" ketika tombol Logout ditekan.

Hal ini saya lakukan dengan menambahkan widget stateless baru untuk menampilkan card dengan cara menambahkan kode sebagai berikut:

class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.indigo,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

Kode berikut ini bertujuan untuk memberi tahu pengguna bahwa pengguna telah menekan tombol tertentu.

onTap: () {
    // Memunculkan SnackBar ketika diklik
    ScaffoldMessenger.of(context)
    ..hideCurrentSnackBar()
    ..showSnackBar(SnackBar(
        content: Text("Kamu telah menekan tombol ${item.name}!")));
},

4. Menjawab beberapa pertanyaan berikut pada README.md pada root folder.

Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?

Stateless widget berarti apabila pengguna melakukan sesuatu di layar maka tidak terjadi perubahan pada layar. Stateful widget berarti apabila pengguna melakukan sesuatu seperti menekan tombol di layar maka langsung muncul suatu perubahan yang ada di layar.

Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.

AppBar : Container yang memunculkan konten dan actions di bagian atas layar

Column : Melayout child widget secara vertikal

Container : Widget yang menggabungkan widget-widget untuk painting, positioning, dan sizing 

ElevatedButton : Button yang materialnya naik apabila ditekan

Icon : Icon berjenis material design

Image : menampilkan sebuah foto

Placeholder : Widget yang menggambar kotak yang mewakili lokasi widget lain suatu hari nanti akan ditambahkan

Row : Melayout child widget dengan arah horizontal 

Scaffold : Mengimplementasikan struktur visual layout material design dasar

MyApp: Ini adalah widget utama yang mewakili aplikasi Flutter. Ini adalah turunan dari StatelessWidget. Ini digunakan sebagai root dari aplikasi.

MaterialApp: Ini adalah widget yang menginisialisasi aplikasi Flutter dan mengatur berbagai parameter aplikasi seperti tema, judul, dan halaman beranda.

title: Ini adalah properti yang menentukan judul aplikasi yang akan ditampilkan di bilah atas.

theme: Ini adalah properti yang digunakan untuk mengatur tema aplikasi, termasuk warna dan gaya.

ColorScheme: Ini adalah widget yang digunakan untuk mengatur skema warna aplikasi. Dalam contoh ini, warna dasar (seedColor) diatur ke Colors.indigo.

useMaterial3: Ini adalah properti yang digunakan untuk mengaktifkan atau menonaktifkan fitur Material 3. Jika diatur ke true, maka aplikasi akan menggunakan Material 3.

MyHomePage: Ini adalah halaman beranda dari aplikasi, yang kemudian akan ditampilkan di home properti MaterialApp.

Text: Widget ini digunakan untuk menampilkan teks di dalam AppBar.

ListView: Ini adalah widget yang digunakan untuk menggulirkan kontennya. Dalam hal ini, digunakan SingleChildScrollView untuk memungkinkan konten menggulir vertikal.

Padding: Widget ini digunakan untuk menambahkan jarak atau bingkai di sekitar child widget-nya.

GridView.count: Ini adalah widget yang digunakan untuk menampilkan daftar item dalam tata letak grid dengan jumlah kolom yang ditentukan.

ShopItem: Ini adalah kelas yang digunakan untuk merepresentasikan item toko dengan nama dan ikonnya.

ShopCard: Ini adalah widget yang digunakan untuk menampilkan item toko dalam bentuk kartu (card). Ini adalah turunan dari StatelessWidget.

Material: Widget ini digunakan untuk memberikan latar belakang dengan warna dan efek material.

InkWell: Ini adalah widget yang digunakan untuk menangani sentuhan dan memberikan respons ketika item toko ditekan.

SnackBar: Ini adalah widget yang digunakan untuk menampilkan pesan kilat (flash message) ketika item toko ditekan.