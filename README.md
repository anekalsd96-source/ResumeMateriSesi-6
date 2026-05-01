## 📘 TUGAS – GENERIC (RESUME SESI 6)

## Nama: Aneka Lisda
## NIM: 25141013P
## Kelas: SI2KR

## 🧠 1. Pengertian Generic
### Generic adalah fitur dalam bahasa pemrograman Dart yang memungkinkan kita membuat kode yang dapat digunakan untuk berbagai tipe data dengan tetap menjaga keamanan tipe (type-safe).
### Dengan generic, kita tidak perlu membuat class atau fungsi yang sama untuk tipe data yang berbeda, sehingga kode menjadi lebih efisien dan reusable.
---

## 🧠 2. Tujuan Penggunaan Generic
### Menghindari penggunaan tipe data dynamic
### Meningkatkan keamanan tipe data (type safety)
### Membuat kode lebih fleksibel dan reusable
### Mengurangi duplikasi kode
---
## 💻 3. Contoh Kode
---
❌ Tanpa Generic
```dart
class Box {
  dynamic data;

  Box(this.data);
}
void main() {
  var box1 = Box(10);        // int
  var box2 = Box("Hello");   // String
  print(box1.data);
  print(box2.data);
}
```
### Output :
### 10
### Hello
---
 ✅ Dengan Generic
```dart
class Box<T> {
  T data;

  Box(this.data);
}

void main() {

  // Box dengan tipe int
  var box1 = Box<int>(10);
  print("Nilai box1: ${box1.data}");

  // Box dengan tipe String
  var box2 = Box<String>("Hello");
  print("Nilai box2: ${box2.data}");

  // Box dengan tipe double
  var box3 = Box<double>(3.14);
  print("Nilai box3: ${box3.data}");
}
```
### Output :
### Nilai box1: 10
### Nilai box2: Hello
### Nilai box3: 3.14
---
✅ Contoh Sintaks Generic pada Class dan Function
```dart
T myFunc<T>(T value) {
  return value;
}

void main() {
 
  // Contoh dengan int
  var angka = myFunc<int>(100);
  print("Nilai int: $angka");

  // Contoh dengan String
  var teks = myFunc<String>("Hello");
  print("Nilai string: $teks");

  // Contoh dengan double
  var desimal = myFunc<double>(3.14);
  print("Nilai double: $desimal");
}
```
### Output :
### Nilai int: 100
### Nilai string: Hello
### Nilai double: 3.14
---
✅ Multiple Type Parameter
```dart
class Pair<K, V> {
  K key;
  V value;

  Pair(this.key, this.value);
}

void main() {

  // Contoh 1: String dan int
  var pair1 = Pair<String, int>("age", 20);
  print("Key: ${pair1.key}, Value: ${pair1.value}");

  // Contoh 2: String dan String
  var pair2 = Pair<String, String>("name", "Aneka");
  print("Key: ${pair2.key}, Value: ${pair2.value}");

  // Contoh 3: int dan double
  var pair3 = Pair<int, double>(1, 3.14);
  print("Key: ${pair3.key}, Value: ${pair3.value}");
}
```
### Output :
### Key: age, Value: 20
### Key: name, Value: Aneka
### Key: 1, Value: 3.14
---
### Penjelasan Singkat :
### <K, V> → dua tipe data (Key & Value)
### Bisa digunakan untuk menyimpan pasangan data seperti:
nama–nilai
id–harga
### Lebih fleksibel dan type-safe
---
✅ Menggabungkan 2 Nilai dengan Tipe Data yang Berbeda
```dart
String combine<T, U>(T a, U b) {
  return "$a, $b";
}

void main() {

  // Contoh 1
  var hasil1 = combine<String, int>("Umur", 20);
  print(hasil1);

  // Contoh 2
  var hasil2 = combine<int, double>(10, 3.14);
  print(hasil2);

  // Contoh 3 (tanpa tipe eksplisit / type inference)
  var hasil3 = combine("Nama", "Aneka");
  print(hasil3);
}
```
### Output :
### Umur, 20
### 10, 3.14
### Nama, Aneka
---
✅ Generic dengan extends
```dart
class NumberBox<T extends num> {
  T value;

  NumberBox(this.value);

  T getValue() {
    return value;
  }
}

void main() {
  print("Program berjalan");

  // Contoh dengan int
  var intBox = NumberBox<int>(10);
  print("Nilai int: ${intBox.getValue()}");

  // Contoh dengan double
  var doubleBox = NumberBox<double>(3.14);
  print("Nilai double: ${doubleBox.getValue()}");

  // ❌ Ini akan error (karena String bukan turunan dari num)
  // var stringBox = NumberBox<String>("Hello");
}
```
### Output :
### Umur, 20
### 10, 3.14
### Nama, Aneka
---
✅ Type Inference
```dart
T myFunc<T>(T value) {
  return value;
}

void main() {

  // Type Inference (tidak perlu menulis <int>)
  var data = myFunc(10);        // otomatis int
  var text = myFunc("Hello");  // otomatis String

  print("Nilai data: $data");
  print("Tipe data: ${data.runtimeType}");

  print("Nilai text: $text");
  print("Tipe text: ${text.runtimeType}");
}
```
### Output :
### Nilai data: 10
### Tipe data: int
### Nilai text: Hello
### Tipe text: String
---
✅ Pembatasan Tipe pada Interface dan Class
```dart
void printData<T extends Iterable>(T data) {
  for (var item in data) {
    print(item);
  }
}

void main() {
  print("Contoh Interface:");

  printData([1, 2, 3]);        // List
  printData({"A", "B"});       // Set

  // ❌ Error:
  // printData(10);
}
```
### Output :
### Contoh Interface:
### 1
### 2
### 3
### A
### B
---
✅ Pembatasan Type dengan Class Abstract
---
### Pembatasan tipe dengan abstract class (T extends Animal) digunakan untuk memastikan bahwa tipe generic hanya boleh berupa turunan dari class Animal, sehingga method seperti sound() bisa dipanggil dengan aman.
---
```dart
abstract class Animal {
  void sound();
}

class Dog implements Animal {
  @override
  void sound() => print("Woof");
}

class Cat implements Animal {
  @override
  void sound() => print("Meow");
}

// Generic dengan pembatasan abstract class
class Cage<T extends Animal> {
  T animal;

  Cage(this.animal);

  void makeSound() {
    animal.sound();
  }
}

void main() {
  var dogCage = Cage(Dog());
  dogCage.makeSound();

  var catCage = Cage(Cat());
  catCage.makeSound();

  // ❌ Error jika bukan turunan Animal
  // var wrong = Cage<String>("Hello");
}
```
### Output :
### Woof
### Meow
---

## Sintaks Generic pada Class dan Function

### Generic adalah fitur yang memungkinkan kita membuat class dan function yang dapat bekerja dengan berbagai tipe data menggunakan parameter tipe seperti <T>.
### Pada class generic, tipe data ditentukan saat objek dibuat, sehingga class dapat digunakan untuk berbagai tipe tanpa menulis ulang kode.
### Pada function generic, tipe data ditentukan saat fungsi dipanggil, sehingga fungsi dapat menerima dan mengembalikan berbagai tipe data dengan aman (type-safe).
---
## 🎯 Tujuan:
### Membuat kode fleksibel dan reusable
### Menjaga keamanan tipe (type safety)
### Mengurangi duplikasi kode
---
