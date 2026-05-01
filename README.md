# 📘 TUGAS – GENERIC (RESUME SESI 6)

# Nama: Aneka Lisda
# NIM: 25141013P
# Kelas: SI2KR

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
### Output:
Nilai box1: 10
Nilai box2: Hello
Nilai box3: 3.14
---
✅ Generic Function
```dart
T myFunc<T>(T value) {
  return value;
}
```
---
✅ Multiple Type Parameter
```dart
class Pair<K, V> {
  K key;
  V value;
  Pair(this.key, this.value);
}
```
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
