# 📘 TUGAS – GENERIC (RESUME SESI 6)

# Nama: Aneka Lisda
# NIM: 25141013P
# Kelas: SI2KR

# 🧠 1. Ringkasan Materi Generic

Generic adalah fitur yang memungkinkan kita membuat kode yang dapat digunakan untuk berbagai tipe data dengan tetap aman (type-safe). Dengan generic, kesalahan tipe bisa dicegah sejak compile-time, berbeda dengan penggunaan dynamic yang baru diketahui saat runtime. Generic dapat digunakan pada class, function, dan collection. Selain itu, terdapat konsep seperti multiple type parameters, type inference, serta pembatasan tipe menggunakan extends untuk memastikan hanya tipe tertentu yang diperbolehkan. Generic juga lebih aman dan efisien dibanding dynamic dan Object karena tidak memerlukan casting dan memiliki performa lebih baik.
---

# 💻 2. Contoh Kode
---
'''dart
❌ Tanpa Generic
class Box {
  dynamic data;
  Box(this.data);
}
```
```dart
✅ Dengan Generic
class Box<T> {
  T data;
  Box(this.data);
}
✅ Generic Function
T myFunc<T>(T value) {
  return value;
}
✅ Multiple Type Parameter
class Pair<K, V> {
  K key;
  V value;
  Pair(this.key, this.value);
}
```
```dart
✅ Menggabungkan 2 Tipe Berbeda
String combine<T, U>(T a, U b) {
  return "$a, $b";
}
✅ Generic dengan extends
class NumberBox<T extends num> {
  T value;
  NumberBox(this.value);
}
✅ Type Inference
var data = myFunc(10); // otomatis int
✅ Pembatasan Tipe Interface
void printData<T extends Iterable>(T data) {
  for (var item in data) {
    print(item);
  }
}
```
```dart
✅ Pembatasan dengan Abstract Class
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
