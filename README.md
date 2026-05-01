# 📘 TUGAS – GENERIC (RESUME SESI 6)

# Nama: Aneka Lisda
# NIM: 25141013P
# Kelas: SI2KR

# 🧠 1. Pengertian Generic
Generic adalah fitur dalam bahasa pemrograman Dart yang memungkinkan kita membuat kode yang dapat digunakan untuk berbagai tipe data dengan tetap menjaga keamanan tipe (type-safe).
Dengan generic, kita tidak perlu membuat class atau fungsi yang sama untuk tipe data yang berbeda, sehingga kode menjadi lebih efisien dan reusable.
---

# 🧠 2. Tujuan Penggunaan Generic
Menghindari penggunaan tipe data dynamic
Meningkatkan keamanan tipe data (type safety)
Membuat kode lebih fleksibel dan reusable
Mengurangi duplikasi kode
---
# 💻 3. Contoh Kode
---
❌ Tanpa Generic
---
'''dart
class Box {
  dynamic data;
  Box(this.data);
}
```
---
 ✅ Dengan Generic
```dart
class Box<T> {
  T data;
  Box(this.data);
}
```
# ✅ Generic Function
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
### ✅ Menggabungkan 2 Tipe Berbeda
'''dart
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
