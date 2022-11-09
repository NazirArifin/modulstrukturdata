# Modul 6 - Linked List -- Dobly & Circular Linked List

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan konsep Dolby & Circular Linked List dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- Jika dosen praktikum sedang menjelaskan, harap diam karena diam adalah cara untuk tidak ngomong apalagi ngomong hal yang tidak bermanfaat

## Materi

### Doubly Linked List

![Doubly Linked List](https://media.geeksforgeeks.org/wp-content/uploads/Circular-doubly-linked-list.png)

- Doubly Linked List adalah linked list yang memiliki pointer ke node selanjutnya dan node sebelumnya. Sedangkan circular linked list memiliki pointer ke node selanjutnya dan node sebelumnya. Pointer pada node terakhir akan menunjuk ke node pertama.

- Kelebihan dari double linked list adalah data dapat dicari kedua arah, baik dari depan maupun belakang. Sedangkan kelemahan dari double linked list adalah membutuhkan memori lebih banyak karena harus menyimpan pointer ke node sebelumnya.

### Circular Linked List

- Hampir sama dengan doubly linked list, hanya saja pointer pada node terakhir akan menunjuk ke node pertama sehingga membentuk lingkaran.
- Kelebihan dari circular linked list adalah kita dalam mencari data dari belakang ke node pertama, karena pointer pada node terakhir akan menunjuk ke node pertama. Selain itu kita tidak perlu menggunakan NULL sebagai penanda akhir dari linked list.
- Sedangkan kelemahan dari circular linked list adalah kita tidak dapat mengetahui apakah node terakhir atau tidak, karena pointer pada node terakhir akan menunjuk ke node pertama. Hal ini seringkali mengakibatkan perulangan tanpa henti.

## Praktikum

- Buat file __"Node.php"__ dan kemudian ketikkan kode berikut:

```php
<?php
class Node {
  private mixed $data;
  private ? Node $previous;
  private ? Node $next;

  public function __construct(mixed $data) {
    $this->data = $data;
    $this->next = null;
    $this->previous = null;
  }

  public function getData(): mixed {
    return $this->data;
  }

  public function getNext(): ? Node {
    if ($this->next == null) {
      return null;
    } else {
      return $this->next;
    }
  }

  public function setNext(? Node $next): void {
    $this->next = $next;
  }

  public function getPrevious(): ? Node {
    if ($this->previous == null) {
      return null;
    } else {
      return $this->previous;
    }
  }

  public function setPrevious(? Node $previous): void {
    $this->previous = $previous;
  }
}
```

- Buat file __"LinkedList.php"__ dan kemudian ketikkan kode berikut:

```php
<?php
class LinkedList {
  private ? Node $head;
  private ? Node $tail;
  private int $size;

  public function __construct() {
    $this->head = null;
    $this->tail = null;
    $this->size = 0;
  }

  public function add(Node $node): void {
    if ($this->head == null) {
      $this->head = $node;
      $this->tail = $node;
    } else {
      // tambahkan node baru ke belakang
      $this->tail->setNext($node);
      $node->setPrevious($this->tail);
      $this->tail = $node;
    }
    $this->size = $this->size + 1;
  }

  public function addFirst(Node $node): void {
    if ($this->head == null) {
      $this->head = $node;
      $this->tail = $node;
    } else {
      $node->setNext($this->head);
      $this->head->setPrevious($node);
      $this->head = $node;
    }
    $this->size = $this->size + 1;
  }

  public function addLast(Node $node): void {
    $this->add($node);
  }

  public function addAt(int $index, Node $node): void {
    if ($index < 0 || $index > $this->size) {
      throw new Exception("Index out of bounds");
    }
    if ($index == 0) {
      $this->addFirst($node);
    } else if ($index == $this->size) {
      $this->addLast($node);
    } else {
      $current = $this->head;
      for ($i = 0; $i < $index - 1; $i++) {
        $current = $current->getNext();
      }
      $node->setNext($current->getNext());
      $current->getNext()->setPrevious($node);
      $current->setNext($node);
      $node->setPrevious($current);
      $this->size++;
    }
  }

  public function removeFirst(): void {
    if ($this->head == null) {
      throw new Exception("List is empty");
    }
    if ($this->head == $this->tail) {
      $this->head = null;
      $this->tail = null;
    } else {
      $this->head = $this->head->getNext();
      $this->head->setPrevious(null);
    }
    $this->size--;
  }

  // cetak isi circle linked list
  public function print(): void {
    $current = $this->head;
    while ($current != null) {
      echo $current->getData() . " ";
      $current = $current->getNext();
    }
    echo PHP_EOL;
  }
}
```

- Untuk mencoba kode yang telah kita buat, buat file __"index.php"__ dan kemudian ketikkan kode berikut:

```php
<?php
<?php
spl_autoload_register(function ($class_name) {
  include $class_name . '.php';
});

try {
  $linkedlist = new LinkedList();
  $linkedlist->add(new Node("A"));
  $linkedlist->add(new Node("B"));
  $linkedlist->add(new Node("C"));

  $linkedlist->addFirst(new Node("D"));
  $linkedlist->addLast(new Node("E"));
  $linkedlist->addAt(2, new Node("F"));

  $linkedlist->print();
} catch (Exception $e) {
  echo $e->getMessage();
}
```

## Tugas

- Tambahkan turunan dari class __"LinkedList.php"__ yang bernama __"CircularLinkedList.php"__ dan kemudian tambahkan method __"removeLast()"__ untuk menghapus node terakhir dari linked list).
- Tambahkan method __"removeAt(int $index)"__ (untuk menghapus node pada index tertentu).
- Tambahkan method __"remove(Node $node)"__ (untuk menghapus node tertentu).
- Tambahkan method __"removeAll(Node $node)"__ (untuk menghapus semua node yang memiliki data yang sama dengan node yang diberikan).

- Pastikan setelah penghapusan node, pointer pada node sebelum dan sesudah node yang dihapus masih benar.