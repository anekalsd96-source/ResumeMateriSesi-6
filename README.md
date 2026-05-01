# 📘 TUGAS – GENERIC (RESUME SESI 6)

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
✅ Generic Function
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
### ✅ Menggabungkan 2 Tipe Berbeda
```dart
String combine<T, U>(T a, U b) {
  return "$a, $b";
}
```
---
✅ Generic dengan extends
```dart
class NumberBox<T extends num> {
  T value;
  NumberBox(this.value);
}
```
---
✅ Type Inference
```dart
var data = myFunc(10); // otomatis int
✅ Pembatasan Tipe Interface
void printData<T extends Iterable>(T data) {
  for (var item in data) {
    print(item);
  }
}
```
---
✅ Pembatasan dengan Abstract Class
```dart
abstract class Animal {
  void sound();
}

class Dog implements Animal {
  void sound() => print("Woof");
}

class Cage<T extends Animal> {
  T animal;
  Cage(this.animal);
}
```
---
