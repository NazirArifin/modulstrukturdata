# Modul 5 - Linked List -- Linear

Tujuan Pembelajaran: Mahasiswa dapat memahami operasi-operasi dasar yang ada dalam linked list serta dapat menggunakannya dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- Shaft-shaft yang ada di depan harap diisi terlebih dahulu

## Materi

### Linked List

- Linked list merupakan kumpulan data yang terdiri dari node-node yang saling terhubung. Setiap node memiliki data dan pointer yang menunjuk ke node selanjutnya. Linked list memiliki dua jenis, yaitu __linear__ dan __circular__.

- Dengan array kita dapat menyimpan data secara linear, tapi array memiliki keterbatasan yang tidak dapat diubah ukurannya. Sedangkan linked list dapat menyimpan data secara linear dan dapat diubah ukurannya.

- Selain itu penghapusan dan penambahan data pada linked list lebih mudah dibandingkan dengan array. Untuk menghapus data pada array kita harus menggeser data yang ada setelah data yang akan dihapus. Sedangkan untuk menghapus data pada linked list cukup menghapus node yang akan dihapus dan mengubah pointer node sebelumnya.

- Kekurangan linked list adalah tidak dapat mengakses data secara langsung, karena data disimpan secara non-linear (lokasi di memori yang tidak berurutan). Untuk mengakses data pada linked list kita harus mengakses data dari node pertama dan mengakses data pada node selanjutnya sampai data yang dicari ditemukan. Memori ekstra juga diperlukan untuk menyimpan pointer pada setiap node.

### Jenis Linked List

- __Simple LInked List__: Linked list yang hanya memiliki pointer ke node selanjutnya.
- __Doubly Linked List__: Linked list yang memiliki pointer ke node selanjutnya dan node sebelumnya.
- __Circular Linked List__: Linked list yang memiliki pointer ke node selanjutnya dan node sebelumnya. Pointer pada node terakhir akan menunjuk ke node pertama.

### Representasi Linked List

- Linked list dapat direpresentasikan dengan menggunakan pointer. Pointer pada linked list dapat berupa pointer ke node pertama, node terakhir, atau node yang akan dihapus. Node pertama disebut dengan head, node terakhir disebut dengan tail, dan node yang akan dihapus disebut dengan current. Jika linked list kosong maka head dan tail akan menunjuk ke null.

- Setiap node terdiri minimal terdiri dari dua bagian yaitu data dan pointer. Pointer pada linked list dapat berupa pointer ke node selanjutnya atau node sebelumnya. Pointer ke node selanjutnya disebut dengan next, dan pointer ke node sebelumnya disebut dengan prev.

## Praktikum





