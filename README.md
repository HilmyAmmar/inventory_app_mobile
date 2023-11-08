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
import 'package:shopping_list/menu.dart';
```

#### Membuat Widget Sederhana pada Flutter
Pada main.dart, saya mengubah warna tema aplikasi menjadi indingo dengan melakukan perubahan pada bagian berikut:
```bash
colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
```

