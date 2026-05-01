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
### ❌ Tanpa Generic
---
### Penggunaan dynamic pada class Box membuat program sangat fleksibel karena dapat menyimpan berbagai tipe data seperti int ### dan String. Namun, pendekatan ini tidak memiliki keamanan tipe (type safety) karena tidak ada pengecekan saat compile-### time. Akibatnya, kesalahan tipe baru akan muncul saat program dijalankan (runtime error). Oleh karena itu, meskipun ###  ### mudah digunakan, penggunaan tanpa generic kurang disarankan untuk program yang membutuhkan keamanan dan keandalan data.
---
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
### ✅ Contoh Sintaks Generic pada Class dan Function
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
### ✅ Multiple Type Parameter
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
### nama–nilai
### id–harga
### Lebih fleksibel dan type-safe
---
### ✅ Menggabungkan 2 Nilai dengan Tipe Data yang Berbeda
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
### ✅ Generic dengan extends
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
### ✅ Type Inference
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
### ✅ Pembatasan Tipe pada Interface dan Class
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
### ✅ Pembatasan Type dengan Class Abstract
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

## Generic Class dan Fungsi

### Sintaks generic pada class dan function memungkinkan kode digunakan untuk berbagai tipe data secara aman, sehingga lebih efisien, fleksibel, dan mudah dipelihara.

### Repository<T> → menyimpan data berbagai tipe
### swap<T> → menukar posisi data dalam list
### Triple<A, B, C> → menyimpan 3 tipe data berbeda
---
```dart
// 1. Class Repository
class Repository<T> {
  List<T> _data = [];

  void save(T item) {
    _data.add(item);
  }

  T getById(int id) {
    return _data[id];
  }

  List<T> getAll() {
    return _data;
  }
}

// 2. Fungsi generic swap
void swap<T>(List<T> list, int i, int j) {
  T temp = list[i];
  list[i] = list[j];
  list[j] = temp;
}

// 3. Class Triple
class Triple<A, B, C> {
  A first;
  B second;
  C third;

  Triple(this.first, this.second, this.third);
}

void main() {
  // 🔹 Test Repository
  var repo = Repository<String>();
  repo.save("Data 1");
  repo.save("Data 2");

  print("Data pertama: ${repo.getById(0)}");
  print("Semua data: ${repo.getAll()}");

  // 🔹 Test swap
  var list = [1, 2, 3];
  swap(list, 0, 2);
  print("Hasil swap: $list");

  // 🔹 Test Triple
  var triple = Triple<String, int, double>("Aneka", 20, 3.5);
  print("Triple: ${triple.first}, ${triple.second}, ${triple.third}");
}
```
### Output :
### Data pertama: Data 1
### Semua data: [Data 1, Data 2]
### Hasil swap: [3, 2, 1]
### Triple: Aneka, 20, 3.5
---
## 🧠 Teori: Generic vs Dynamic vs Object
---
### Dalam Dart, terdapat tiga cara menangani tipe data:
---
### 1. Generic (<T>)
---
### Generic digunakan untuk menentukan tipe data secara spesifik saat compile-time.
### ✔️ Aman (type-safe)
### ✔️ Tidak perlu casting
### ✔️ Performa lebih baik
---
### 2. Dynamic
---
### dynamic memungkinkan variabel menyimpan semua tipe data tanpa pengecekan saat compile-time.
### ✔️ Fleksibel
### ❌ Tidak aman (error muncul saat runtime)
---
### 3. Object
---
### Object adalah tipe dasar semua tipe data di Dart.
### ✔️ Lebih aman dari dynamic
### ❌ Harus casting saat digunakan
---
### Contoh Kode penggunaan Generic vs Dynamic vs Object
```dart
// Generic
class Box<T> {
  T data;
  Box(this.data);
}

// Dynamic
class BoxDynamic {
  dynamic data;
  BoxDynamic(this.data);
}

// Object
class BoxObject {
  Object data;
  BoxObject(this.data);
}

void main() {
  // ✅ Generic (aman)
  var box1 = Box<int>(10);
  print("Generic: ${box1.data}");

  // ❌ Dynamic (berisiko)
  var box2 = BoxDynamic("Hello");
  print("Dynamic: ${box2.data}");

  // ⚠️ Object (perlu casting)
  var box3 = BoxObject(100);
  int nilai = box3.data as int;
  print("Object: $nilai");

  // ❌ Contoh error dynamic (runtime)
  var boxError = BoxDynamic("Text");
  // int salah = boxError.data; // error saat runtime
}
```
### Output :
### Generic: 10
### Dynamic: Hello
### Object: 100
---
## Cache Generic
### Cache Generic adalah struktur penyimpanan data sementara yang menggunakan Generic <T> sehingga dapat menyimpan berbagai tipe data dengan aman (type-safe).
---
Cache biasanya digunakan untuk:
---
### Menyimpan data sementara
### Mempercepat akses data
### Mengurangi pengambilan data berulang
---
Dengan Generic, kita bisa membuat satu class cache yang bisa digunakan untuk berbagai tipe data tanpa membuat ulang class.
---
### Contohnya :
```dart
class Cache<T> {
  final Map<String, T> _storage = {};

  void set(String key, T value) {
    _storage[key] = value;
  }

  T? get(String key) {
    return _storage[key];
  }

  void remove(String key) {
    _storage.remove(key);
  }
}

void main() {
  print("Program berjalan");

  // Cache untuk String
  var userCache = Cache<String>();
  userCache.set("name", "Aneka");
  print("User: ${userCache.get("name")}");

  // Cache untuk int
  var numberCache = Cache<int>();
  numberCache.set("age", 20);
  print("Age: ${numberCache.get("age")}");

  // Cache untuk object
  var listCache = Cache<List<int>>();
  listCache.set("numbers", [1, 2, 3]);
  print("Numbers: ${listCache.get("numbers")}");
}
```
### Output :
### Program berjalan
### User: Aneka
### Age: 20
### Numbers: [1, 2, 3]
