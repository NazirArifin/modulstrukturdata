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

- __Simple Linked List__: Linked list yang hanya memiliki pointer ke node selanjutnya.
- __Doubly Linked List__: Linked list yang memiliki pointer ke node selanjutnya dan node sebelumnya.
- __Circular Linked List__: Linked list yang memiliki pointer ke node selanjutnya dan node sebelumnya. Pointer pada node terakhir akan menunjuk ke node pertama.

### Representasi Linked List

- Linked list dapat direpresentasikan dengan menggunakan pointer. Pointer pada linked list dapat berupa pointer ke node pertama, node terakhir, atau node yang akan dihapus. Node pertama disebut dengan head, node terakhir disebut dengan tail, dan node yang akan dihapus disebut dengan current. Jika linked list kosong maka head dan tail akan menunjuk ke null.

- Setiap node terdiri minimal terdiri dari dua bagian yaitu data dan pointer. Pointer pada linked list dapat berupa pointer ke node selanjutnya atau node sebelumnya. Pointer ke node selanjutnya disebut dengan next, dan pointer ke node sebelumnya disebut dengan prev.

## Praktikum

- Buat file __"Node.php"__ dan ketikkan kode berikut:

```php
<?php
class Node {
  private ? Node $next;
  private mixed $data;

  public function __construct(mixed $data) {
    $this->data = $data;
    $this->next = null;
  }

  public function getNext() {
    return $this->next;
  }

  public function setNext(?Node $next) {
    $this->next = $next;
  }

  public function getData() {
    return $this->data;
  }
}
```

- Kemudian buat file __"LinkedList.php"__ dan ketikkan kode berikut:

```php
<?php
class LinkedList {
  // head adalah node pertama dari linked list, bisa null
  private ? Node $head;
  // size adalah jumlah node yang ada di linked list
  private int $length;

  public function __construct() {
    $this->head = null;
    $this->length = 0;
  }

  public function getHead(): ? Node {
    if ($this->head == null) {
      return null;
    } else {
      return $this->head;
    }
  }

  public function getLength(): int {
    return $this->length;
  }

  public function isEmpty(): bool {
    return $this->length == 0;
  }

  public function insertFirst(Node $node): void {
    if ($this->head == null) {
      $this->head = $node;
    } else {
      // kita akan menghubungkan node baru dengan node yang ada
      $node->setNext($this->head);
      // kemudian kita akan mengubah head menjadi node baru
      $this->head = $node;
    }
    $this->length = $this->length + 1;
  }

  public function insertLast(Node $node): void {
    if ($this->head == null) {
      $this->head = $node;
    } else {
      // kita akan mencari node terakhir
      $current = $this->head;
      while ($current->getNext() != null) {
        $current = $current->getNext();
      }
      // setelah menemukan node terakhir, kita akan menghubungkan node baru dengan node terakhir
      $current->setNext($node);
    }
    $this->length = $this->length + 1;
  }

  public function deleleFirst(): void {
    if ($this->head != null) {
      $current = $this->head;
      // kita akan menghapus node pertama
      $this->head = $this->head->getNext();
      // menghapus node pertama tidak berarti menghapus node dari memori
      // karena node pertama masih bisa diakses melalui variabel current
      // kita akan menghapus node dari memori dengan menghapus variabel current
      unset($current);
      $this->length = $this->length - 1;
    }
  }

  public function deleteLast(): void {
    if ($this->head != null) {
      $current = $this->head;
      // cari node terakhir dimana node terakhir adalah node yang tidak memiliki next
      while ($current->getNext() != null) {
        $previous = $current;
        $current = $current->getNext();
      }
      // setelah menemukan node terakhir, kita akan menghapus node terakhir
      $previous->setNext(null);
      // kita akan menghapus node dari memori dengan menghapus variabel current
      unset($current);
      $this->length = $this->length - 1;
    }
  }

  public function insertAt(Node $node, int $index = 0): void {
    if ($index == 0) {
      $this->insertFirst($node);
    } else if ($index == $this->length) {
      $this->insertLast($node);
    } else if ($index > 0 && $index < $this->length) {
      $current = $this->head;
      $i = 0;
      // kita akan mencari node yang berada di index sebelum index yang diinginkan
      while ($i < $index - 1) {
        $current = $current->getNext();
        $i = $i + 1;
      }
      // setelah menemukan node yang berada di index sebelum index yang diinginkan
      // kita akan menghubungkan node baru dengan node yang berada di index sebelum index yang diinginkan
      $node->setNext($current->getNext());
      // kemudian kita akan menghubungkan node yang berada di index sebelum index yang diinginkan dengan node baru
      $current->setNext($node);
      $this->length = $this->length + 1;
    }
  }

  public function deleteAt(int $index): void {
    if ($index == 0) {
      $this->deleleFirst();
    } else if ($index == $this->length - 1) {
      $this->deleteLast();
    } else if ($index > 0 && $index < $this->length - 1) {
      $current = $this->head;
      $i = 0;
      // kita akan mencari node yang berada di index sebelum index yang diinginkan
      while ($i < $index - 1) {
        $current = $current->getNext();
        $i = $i + 1;
      }
      // setelah menemukan node yang berada di index sebelum index yang diinginkan, 
      // kita akan menghapus node yang berada di index yang diinginkan
      $current->setNext($current->getNext()->getNext());
      $next = $current->getNext();
      // kita akan menghapus node dari memori dengan menghapus variabel next
      unset($next);
      $this->length = $this->length - 1;
    }
  }

  public function print(): void {
    if ($this->head != null) {
      $current = $this->head;
      while ($current != null) {
        echo $current->getData() . " ";
        $current = $current->getNext();
      }
      echo PHP_EOL;
    }
  }
}
```

- Untuk mencoba kode yang telah kita buat, buat file __"index.php"__ dan ketikkan kode berikut:

```php
<?php
spl_autoload_register(function ($class_name) {
  include $class_name . '.php';
});

$linkedlist = new LinkedList();
$linkedlist->insertFirst(new Node("A"));
$linkedlist->insertFirst(new Node("B"));
$linkedlist->insertFirst(new Node("C"));

$linkedlist->insertLast(new Node("D"));
$linkedlist->print();

$linkedlist->deleteLast();
$linkedlist->deleteAt(2);
$linkedlist->print();
```

- Jalankan kode di atas dengan perintah __"php index.php"__ dan jika berhasil maka Anda akan melihat hasil operasi linked list yang sudah kita kerjakan.

## Tugas

- Buat class __Stack__ yang memiliki method __push()__, __pop()__, dan __print()__ yang menggunakan linked list sebagai struktur data dasarnya.
- Buat class __Queue__ yang memiliki method __enqueue()__, __dequeue()__, dan __print()__ yang menggunakan linked list sebagai struktur data dasarnya.





