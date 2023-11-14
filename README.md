# Inventory App Using Flutter 
Nama   : Hilmy Ammar Darmawan  
NPM    : 2206081736  
Kelas  : PBP - E  
## Assignment 7

### Perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi flutter?
Stateless Widget  : Widget yang statis yang berarti tidak dapat berubah setelah dibuat  
Stateful Widget   : Widget yang dinamis yang berarti widget dapat merespons perubahan data dan interaksi user

### Widget yang digunakan dalam tugas 7
1. ShopCard: Menerima data dari ShopItem dan menampilkannya dalam bentuk card
2. Scaffodld: Berperan sebagai kerangka dasar untuk tampilan aplikasi
3. AppBar: Menampilkan judul aplikasi
4. Text: Menampilkan teks di layar
5. InkWell: Memberikan area responsif terhadap sentuhan user
6. Icon: Menampilkan icon
7. Container: Mengelompokkan ikon dan teks ke dalam card
   
### Implementasi Checklist Tugas
#### Membuat sebuah program flutter baru

Melalui terminal pada direktori tempat saya menyimpan proyek, saya generate proyek flutter baru bernama inventory_app dengan kode berikut  
```bash
flutter create inventory_app
cd inventory_app
```
Lalu saya menjalankan 'flutter run' pada terminal untuk melihat apakah proyek sudah berhasil dibuat

#### Merapikan struktur proyek
Dalam menerapkan *best practice.* dalam pengembangan aplikasi, saya membuat file baru bernama menu.dart pada direktory inventory_app/lib. Pada baris pertama saya menambahkan kode berikut:
```bash
import 'package:flutter/material.dart';
```
Lalu, dari file main.dart, saya melakukan *cut.* dari baris ke 39 sampai akhir kode yang berisi class 'MyHomePage' dan 'MyHomePageState' ke menu.dart. Terakhir saya menambahkan kode berikut agar tidak ada bagian kode yang error
```bash
import 'package:inventory_app/menu.dart';
```

#### Membuat Widget Sederhana pada Flutter
Pada main.dart, saya mengubah warna tema aplikasi menjadi indingo dengan melakukan perubahan pada bagian berikut:
```bash
colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
```
Setelah itu, saya mengubah sifat widget halaman dari stateful menjadi stateless
1. Saya menghapus 'MyHomePage(title: 'Flutter Demo Home Page')' menjadi MyHomePage() saja
2. Saya mengubah mengubah sifat widget halaman dari stateful menjadi stateless dengan menambahkan beberapa baris kode dan menghapus final String title sampai bawah sehingga kode berubah menjadi seperti ini
```bash
class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            ...
        );
    }
}
```
Selanjutnya, saya menambahkan teks dan card untuk memperlihatkan item yang dijual. Beda dengan tutorial, pada class ShopItem saya juga menambahkan warna card untuk mengimplementasi bonus sehingga kode akan menjadi seperti ini
```bash
class ShopItem {
  final String name;
  final IconData icon;
  final Color color;
  ShopItem(this.name, this.icon, this.color);
}
```
Lalu, dibawah kode 'MyHomePage({Key? key}) : super(key: key);', saya menambahkan item-item yang dijual dengan kode berikut. Karena saya mengubah class, ada bagian kode yang saya tambahkan menjadi seperti ini
```bash
final List<ShopItem> items = [
    ShopItem("Lihat Produk", Icons.checklist),
    ShopItem("Tambah Produk", Icons.add_shopping_cart),
    ShopItem("Logout", Icons.logout),
];
```
Selanjutnya, saya menambahkan kode dibawah ini didalam widget build
```bash
return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Inventory App',
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
```
Terakhir, saya membuat widget stateless untuk menampilkan card
```bash
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
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
```
#### Finishing
Setelah semua kode saya edit sesuai dengan panduan pada tutorial dan checklist pada tugas, saya menjalankan 'flutter run' dan hasilnya memang seperti yang saya harapkan. Terdapat 3 card, yaitu Lihat Item, Tambah Item, dan Logout dengan setiap cardnya memiliki warna yang berbeda. Terakhir, saya melakukan git add, commit, dan push ke dalam repository ini

## Assigment 8

### Perbedaan antara Navigator.push() dan Navigator.pushReplacement(), beserta contoh
1. 'Navigator.push()' digunakan untuk menambahkan halaman baru ke *navigation stack*. Halaman baru ditambahkan di atas halaman sebelumnya sehingga pengguna dapat kembali ke halaman tersebut dengan mudah. Contoh penggunaannya adalah ketika meng-click suatu card yang menampilkan suatu produk maka akan berpindah ke halaman yang mengandung informasi produk tersebut dan akan kembali ke halaman card saat pengguna meng-click tombol back.
2. 'Navigator.pushReplacement()' digunakan untuk menambahkan halaman baru ke *navigation stack* disertai dengan menggantikan halaman saat ini dalam tumpukan dengan halaman baru. Contoh penggunaannya adalah ketika meng-click tombol log in pada halaman login, maka akan berpindah ke beranda utama dan tidak bisa kembali ke halaman login lagi.

### Widget pada Flutter
1. Container: Digunakan untuk mengatur properti seperti padding, margin, dan decoration
2. Row: Digunakan untuk menyusun elemen secara horizontal
3. Column: Digunakan untuk menyusun elemen secara vertikal
4. ListView: Digunakan untuk menampilkan daftar elemen
5. Stack: Digunakan untuk menumpukkan elemen-elemen di atas satu sama lain

### Elemen input pada Tugas 7 beserta alasan penggunaannya
1. TextFormField: Digunakan pada setiap kolom input pada form, termasuk kolom nama, harga, dan deskripsi. Elemen ini dapat juga digunakan untuk menentukan berbagai properti pada form, seperti label, teks, dsb. Selain itu, elemen ini juga menyediakan validasi input untuk memastikan bahwa pengguna memasukkan data yang valid dan sesuai apa yang diharapkan.
2. ElevatedButton: Digunakan untuk mengirimkan data. Ketika user menekan tombol, Flutter akan mengirimkan data yang telah dimasukkan melalui TextFormField ke fungsi onPressed(). Fungsi ini kemudian digunakan untuk melakukan pemrosesan data dan mengambil tindakan sesuai yang diinginkan, seperti menyimpan data atau melakukan perubahan pada data yang telah ada.
   
### Penerapan *clean architecture* pada Flutter
*Clean Architecture* merupakan sebuah pola arsitektur dalam pengembangan software yang memisahkan domain dari infrastruktur. Hal ini membuat aplikasi menjadi lebih mudah untuk dipahami, diuji, dan diperbarui. Penerapa *clean architecture* pada flutter dapat dibagi menjadi beberapa layer, yaitu:
1. Presentation layer: Bertanggung jawab dalam menampilkan data kepada pengguna. Layer ini menggunakan widget Flutter untuk membangun *user interface* aplikasinya
2. Domain layer: Bertanggung jawab dalam memproses logika bisnis aplikasi. 
3. Data layer: Bertanggung jawab dalam mengambil dan menyimpan data. Layer ini dapat menggunakan berbagai sumber data, seperti API, database, atau file lokal.

### Implementasi Checklist Tugas
#### Menambahkan drawer menu untuk navigasi
Pertama, saya membuat berkas baru dalam direktori baru `widgets` dengan nama `left_drawer.dart`. Pada berkas tersebut, saya menambahkan kode berikut:
```
import 'package:flutter/material.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            // TODO: Bagian drawer header
          ),
          // TODO: Bagian routing
        ],
      ),
    );
  }
}
```
Selanjutnya, saya mengimpor halaman-halaman yang ingin kita masukkan ke dalam navigasi pada drawer menu. Setelah berhasil import, saya memasukkan routing untuk halaman-halaman yang telah diimpor ke bagian `TODO: Bagian routing` dengan kode berikut:
```
...
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
  title: const Text('Tambah Produk'),
  // Bagian redirection ke ShopFormPage
  onTap: () {
    /*
    TODO: Buatlah routing ke ShopFormPage di sini,
    setelah halaman ShopFormPage sudah dibuat.
    */
  },
),
...
```
Lanjut, saya akan menghias header dengan memasukkan drawer header di `TODO: Bagian drawer header` dengan kode berikut:
```
...
const DrawerHeader(
  decoration: BoxDecoration(
    color: Colors.indigo,
  ),
  child: Column(
    children: [
      Text(
        'Shopping List',
        textAlign: TextAlign.center,
        style: TextStyle(
          fontSize: 30,
          fontWeight: FontWeight.bold,
          color: Colors.white,
        ),
      ),
      Padding(padding: EdgeInsets.all(10)),
      Text("Catat seluruh keperluan belanjamu di sini!",
          // TODO: Tambahkan gaya teks dengan center alignment, font ukuran 15, warna putih, dan weight biasa
          ),
    ],
  ),
),
...
```
Terakhir, setelah berhasil membuat drawer menu. Saya memasukkan drawer menu yang telah dibuat tersebut ke dalam halaman `menu.dart` dengan kode `drawer: const LeftDrawer()` setelah melakukan impor. Tidak lupa, saya mengerjakan setiap TODO yang masih ada pada kode agar program dapat berjalan lancar

#### Menambahkan Form dan Elemen Input 
Pertama, saya akan membuat berkas baru pada `lib` dengan nama `shoplist_form.dart`/ Lalu, saya menambahkan sejumlah kode ke dalam berkas tersebut.
```
import 'package:flutter/material.dart';
// TODO: Impor drawer yang sudah dibuat sebelumnya

class ShopFormPage extends StatefulWidget {
    const ShopFormPage({super.key});

    @override
    State<ShopFormPage> createState() => _ShopFormPageState();
}

class _ShopFormPageState extends State<ShopFormPage> {
    @override
    Widget build(BuildContext context) {
        return Placeholder();
    }
}
```
Selanjutnya, saya mengubah widget `Placeholder()' dengan kode berikut:
```
Scaffold(
  appBar: AppBar(
    title: const Center(
      child: Text(
        'Form Tambah Produk',
      ),
    ),
    backgroundColor: Colors.indigo,
    foregroundColor: Colors.white,
  ),
  // TODO: Tambahkan drawer yang sudah dibuat di sini
  body: Form(
    child: SingleChildScrollView(),
  ),
);
```
Setelah mengubah widget, saya membuat variabel baru bernama `_formKey` lalu menambahkan `_formKey` tersebut ke dalam atribut `key` milik widget `form`. Selanjutnya saya mengisi widget `form` dengan field. Beberapa variable dibuat untuk menyimpan input dari masing-masing field yang akan dibuat. Setelah itu, saya membuat widget `Column` sebagai child dari `SingleChildScrollView` serta membuat widget `TextFormField` yang dibungkus oleh `Padding` sebagai salah satu children dari widget `Column`. Lalu, saya menambahkan atribut `crossAxisAlignment` untuk mengatur alignment children dari `Column`. Selanjutnya, saya membuat dua `TextFormField` yang dibungkus dengan `Padding` sebagai child selanjutnya dari `Column` seperti sebelumnya untuk sisa field. Terakhir, saya membuat tombol sebagai child selanjutnya dari `Column`. Tombol akan dibungkus dengan widget `Padding` dan `Align`. Kode akhir akan terlihat seperti ini.
```
class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _price = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Form Tambah Item',
          ),
        ),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Form(
        key: _formKey,
        child: SingleChildScrollView(
            child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Nama Item",
                  labelText: "Nama Item",
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
                            title: const Text('Item berhasil tersimpan'),
                            content: SingleChildScrollView(
                              child: Column(
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                  Text('Nama: $_name'),
                                  Text('Price: $_price'),
                                  Text('Description: $_description'),
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
                    }
                    _formKey.currentState!.reset();
                  },
                  child: const Text(
                    "Save",
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              ),
            ),
          ],
        )),
      ),
    );
  }
}
```

#### Memunculkan Data
