Nama : Fikri Budianto
Kelas : PBP F
NPM : 2206025306

 - Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!
 <p>Singkatnya, method Navigator.push() digunakan untuk menambahkan rute lain ke atas tumpukan screen (stack) saat ini. Halaman baru ditampilkan di atas halaman sebelumnya dan pengguna dapat kembali ke halaman sebelumnya dengan cara menekan tombol back dan meng-pop stack layar sekarang.

 Contoh penggunaan Navigator.push() adalah ketika kita ingin masuk ke dalam suatu halaman baru yang bertujuan untuk menambahkan produk dan kembali menggunakan tombol kembali ketika kita sudah selesai menambahkan tombol produk.
 
 Navigator.pushReplacement() memiliki fungsi yang kurang lebih sama dengan Navigator.push(). Namun, Navigator.pushReplacement() menggantikan stack layar teratas dan menggantikan stack layar tersebut dengan stack yang baru sehingga kita tidak bisa kembali ke layar yang stacknya sudah dihapus tersebut.
 
 Contoh penggunaan Navigator.pushReplacement() adalah ketika kita ingin masuk ke halaman baru setelah menlakukan login. Ketika kita sudah melakukan login, tentunya kita tidak ingin kembali lagi ke halaman login tersebut sehingga agar ketika kita menekan tombol back kita tetap di halaman utama digunakanlah Navigator.pushReplacement()
 </p>

 - Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!
  - Container : Menampung widget lain dan menyediakan control terhadap dimensi, padding, margin, dan dekorasi widget tersebut. Digunakan untuk menampung dan mengatur style dari widget
  - Row : Digunakan untuk mengatur widget secara horizontal
  - Column : digunakan untuk mengatur widget secara vertikal 
  - Stack : Digunakan untuk menumpuk widget di atas widget lain
  - ListView : Digunakan untuk menampilkan daftar item yang banyaknya melebihi apa yang bisa ditampilkan pada layar dan membolehkan kita untuk melakukan scrolling terhadap daftar item tersebut.
  - Expanded : Digunakan apabila kita ingin agar sebuah child widget mencakup seluruh luas layar pada sumbu tertentu 
  

 - Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!
  Elemen input yang saya gunakan pada tugas kali ini adalah TextFormField. Elemen input ini saya gunakan karena TextFormField menyediakan beberapa fitur bawaan seperti validasi input dan styling sehingga memudahkan dalam membangun aplikasi.

 - Bagaimana penerapan clean architecture pada aplikasi Flutter?
 Penerapan clean architecture pada aplikasi Flutter dapat dilakukan dengan membagi aplikasi menjadi 3 layer, diantaranya:
  <p>
  - Presentation layer yang mengurusi tampilan yang dilihat oleh pengguna
  - Domain layer yang mengurusi business logic dari aplikasi sendiri
  - Data layer yang mengurusi penyimpanan dan pengiriman data pada aplikasi</p>Dengan menerapkan hal tersebut, kita memperoleh beberapa manfaat, diantaranya: 
     - Separation of concerns dimana masing-masing modul hanya mengurusi urusannya masing-masing sehingga aplikasi menjadi lebih modular dan lebih mudah dimaintain
	 - Testability dimana kita menjadi lebih mudah membuat unit test karena masing-masing modul dites secara independen
	 - Scalability dan maintainability dimana aplikasi yang kita buat menjadi lebih mudah untuk dikembangkan lebih lanjut dan untuk dimaintain karena masing-masing layer terpisah

 - Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial)
 Untuk membuat halaman formulir pada aplikasi sekaligus validasinya, pertama-tama saya menambahkan kode berikut untuk mengimpor fungsi yang diperlukan:
 ```dart
import 'package:flutter/material.dart';
import 'package:enkom_kw_mobile/widgets/left_drawer.dart';
```
Lalu, untuk membuat halaman formulir beserta validasi untuk formulir tersebut, saya menambahkan kode berikut:
```dart
class ShopFormPage extends StatefulWidget {
  		const ShopFormPage({super.key});
  		@override
  		State<ShopFormPage> createState() => _ShopFormPageState();
}
```
```dart
class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  int _price = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Center(
            child: Text(
              'Form Tambah Produk',
            ),
          ),
          backgroundColor: Colors.indigo,
          foregroundColor: Colors.white,
        ),
        drawer: const LeftDrawer(),
        body: Form(
          key: _formKey,
          child: SingleChildScrollView(
            child:
                Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Nama Produk",
                    labelText: "Nama Produk",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _name = value!;
                    });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Nama tidak boleh kosong!";
                    }
                    return null;
                  },
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Jumlah",
                    labelText: "Jumlah",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _price = int.parse(value!);
                    });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Jumlah tidak boleh kosong!";
                    }
                    if (int.tryParse(value) == null) {
                      return "Jumlah harus berupa angka!";
                    }
                    return null;
                  },
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Harga",
                    labelText: "Harga",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _price = int.parse(value!);
                    });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Harga tidak boleh kosong!";
                    }
                    if (int.tryParse(value) == null) {
                      return "Harga harus berupa angka!";
                    }
                    return null;
                  },
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: TextFormField(
                  decoration: InputDecoration(
                    hintText: "Deskripsi",
                    labelText: "Deskripsi",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    ),
                  ),
                  onChanged: (String? value) {
                    setState(() {
                      _description = value!;
                    });
                  },
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return "Deskripsi tidak boleh kosong!";
                    }
                    return null;
                  },
                ),
              ),
              Align(
                alignment: Alignment.bottomCenter,
                child: Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: ElevatedButton(
                    style: ButtonStyle(
                      backgroundColor: MaterialStateProperty.all(Colors.indigo),
                    ),
                    onPressed: () {
                      if (_formKey.currentState!.validate()) {
                        showDialog(
                          context: context,
                          builder: (context) {
                            return AlertDialog(
                              title: const Text('Produk berhasil tersimpan'),
                              content: SingleChildScrollView(
                                child: Column(
                                  crossAxisAlignment: CrossAxisAlignment.start,
                                  children: [
                                    Text('Nama: $_name'),
                                    Text('Jumlah: $_amount'),
                                    Text('Harga: $_price'),
                                    Text('Deskripsi: $_description'),
                                  ],
                                ),
                              ),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            );
                          },
                        );
                        _formKey.currentState!.reset();
                      }
                    },
                    child: const Text(
                      "Save",
                      style: TextStyle(color: Colors.white),
                    ),
                  ),
                ),
              ),
            ]),
          ),
        ));
  }
}
```
Pada kode tersebut, saya membuat widget TextFormField yang dibungkus oleh Padding sebagai salah satu children dari widget Column. Setelah itu, saya menambahkan atribut crossAxisAlignment untuk mengatur alignment children dari Column.
Di dalam masing-masing widget TextFormField, saya menambahkan validasi-validasi yang sekiranya diperlukan untuk mencegah input yang invalid. Contohnya adalah validator berikut yang bertujuan untuk mengecek apakah deskripsi yang dimasukkan oleh user kosong atau tidak.
```dart
 validator: (String? value) {
		if (value == null || value.isEmpty) {
		  return "Deskripsi tidak boleh kosong!";
		}
		return null;
},
```
Tombol save diimplementasikan dengan menambahkan kode berikut:
```dart
child: const Text(
	  "Save",
	  style: TextStyle(color: Colors.white),
	),
```
Lalu, data dimunculkan dengan menambahkan kode berikut:
```dart
Align(
	alignment: Alignment.bottomCenter,
	child: Padding(
	  padding: const EdgeInsets.all(8.0),
	  child: ElevatedButton(
		style: ButtonStyle(
		  backgroundColor: MaterialStateProperty.all(Colors.indigo),
		),
		onPressed: () {
		  if (_formKey.currentState!.validate()) {
			showDialog(
			  context: context,
			  builder: (context) {
				return AlertDialog(
				  title: const Text('Produk berhasil tersimpan'),
				  content: SingleChildScrollView(
					child: Column(
					  crossAxisAlignment: CrossAxisAlignment.start,
					  children: [
						Text('Nama: $_name'),
						Text('Jumlah: $_amount'),
						Text('Harga: $_price'),
						Text('Deskripsi: $_description'),
					  ],
					),
				  ),
				  actions: [
					TextButton(
					  child: const Text('OK'),
					  onPressed: () {
						Navigator.pop(context);
					  },
					),
				  ],
				);
			  },
			);
			_formKey.currentState!.reset();
		  }
		},
		child: const Text(
		  "Save",
		  style: TextStyle(color: Colors.white),
		),
	  ),
	),
  ),
```
Pengguna akan diarahkan ke dalam form tambah item baru dengan menambahkan kode sebagai berikut:
```dart
  ListTile(
	leading: const Icon(Icons.add_shopping_cart),
	title: const Text('Tambah Item'),
	// Bagian redirection ke ShopFormPage
	onTap: () {
	  Navigator.push(
		  context,
		  MaterialPageRoute(
			  builder: (context) => const ShopFormPage()));
	},
  ),
```
Lalu, kita akan membuat drawer dimana drawer tersebut memiliki 2 tombol, yaitu halaman utam dan tambah item, dimana masing-masing tombol akan merouting pengguna ke tujuan yang diinginkan dengan menambahkan kode berikut:

```dart
import 'package:flutter/material.dart';
import 'package:enkom_kw_mobile/screens/menu.dart';
import 'package:enkom_kw_mobile/screens/shoplist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'EnKomKWSuper',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text(
                  "Toko Laptop terpercayamu!",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    fontWeight: FontWeight.normal,
                    color: Colors.white, // Set the text color to white
                  ),
                ),
              ],
            ),
          ),
          // TODO: Bagian routing
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Item'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              Navigator.push(
                  context,
                  MaterialPageRoute(
                      builder: (context) => const ShopFormPage()));
            },
          ),
        ],
      ),
    );
  }
}
```