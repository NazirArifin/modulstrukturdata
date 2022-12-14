# Modul 8 - Binary Search Tree (BST)

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep dan implementasi struktur data Binary Search Tree (BST) dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- _Tidak penting apa yang orang lain pikirkan tentang kita, yang penting adalah apa yang kita pikirkan tentang diri kita sendiri_

## Materi

### Binary Tree
- Binary Tree adalah struktur data yang terdiri dari node-node yang saling terhubung dengan relasi parent-child. Setiap node memiliki 2 buah child, yaitu left child dan right child.
- Binary Tree memiliki 3 macam jenis, yaitu:
  - Full Binary Tree: Binary Tree yang setiap node memiliki 2 buah child atau tidak memiliki child sama sekali
  - Complete Binary Tree: Binary Tree yang setiap level terisi secara penuh, kecuali level terakhir. Level terakhir terisi dari kiri ke kanan.
  - Perfect Binary Tree: Binary Tree yang setiap level terisi secara penuh, dan setiap node memiliki 2 buah child.
  - Balanced Binary Tree: Binary Tree yang memiliki tinggi yang sama di setiap levelnya. Jika tinggi dari setiap levelnya berbeda, maka Binary Tree tersebut tidak disebut Balanced Binary Tree.

![Binary Tree](https://pics.me.me/tevits-331t-ttt-go-studying-data-structures-binary-tree-on-58744783.png)

### Binary Search Tree
- Binary Search Tree (BST) adalah struktur data tree yang berbasis node biner yang mana memiliki properti berikut:
  - Semua node di sub-tree kiri memiliki nilai yang lebih kecil dari node induknya
  - Semua node di sub-tree kanan memiliki nilai yang lebih besar dari node induknya
  - Sub-tree kiri dan sub-tree kanan juga merupakan BST

![BST](https://media.geeksforgeeks.org/wp-content/uploads/BSTSearch.png)

- Pada BST, kita dapat melakukan operasi berikut:
  - Insert
  - Delete
  - Search
  - Traversal (Inorder, Preorder, Postorder)

- Inorder Traversal: Proses traversal dimulai dari node paling kiri, kemudian dilanjutkan ke node induknya, dan terakhir ke node paling kanan. Proses traversal ini akan menghasilkan data yang terurut secara ascending.
- Preorder Traversal: Proses traversal dimulai dari node induk, kemudian dilanjutkan ke node paling kiri, dan terakhir ke node paling kanan. Proses ini digunakan untuk membuat _copy_ dari BST.
- Postorder Traversal: Proses traversal dimulai dari node paling kiri, kemudian dilanjutkan ke node paling kanan, dan terakhir ke node induknya. Proses ini digunakan untuk menghapus node pada BST.

![Traversal](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Preorder-from-Inorder-and-Postorder-traversals.jpg)


## Praktikum 

### Binary Search Tree

- Pertama kita akan membuat class __"Node"__ dalam file __"Node.php"__ untuk menampung data yang akan dimasukkan ke dalam tree. Class __"Node"__ memiliki property __"data"__ untuk menampung data, dan property __"left"__ dan __"right"__ untuk menampung node-node anak dari node tersebut. Class __"Node"__ memiliki method __"__construct"__ untuk menginisialisasi data dan node-node anak dari node tersebut.

```php
<?php
class Node {
  private mixed $data;
  private ?Node $left;
  private ?Node $right;
  private ?Node $parent;
  private array $children;

  public function __construct(mixed $data) {
    $this->data = $data;
    $this->left = null;
    $this->right = null;
    $this->parent = null;
    $this->children = [];
  }

  public function setParent(Node $parent): void {
    $this->parent = $parent;
  }

  public function getParent(): ?Node {
    return $this->parent;
  }

  public function getData(): mixed {
    return $this->data;
  }

  public function setData(mixed $data): void {
    $this->data = $data;
  }

  public function getLeft(): ?Node {
    return $this->children[0] ?? null;
  }

  public function getRight(): ?Node {
    return $this->children[1] ?? null;
  }

  public function setLeft(?Node $node): void {
    $this->children[0] = $node;
  }

  public function setRight(?Node $node): void {
    $this->children[1] = $node;
  }

  public function getChildren(): array {
    return $this->children;
  }
}
```

- Selanjutnya kita akan membuat class __"BinarySearchTree"__ dalam file __"BinarySearchTree.php"__ untuk mengimplementasikan Binary Search Tree. Ketikkan kode berikut:

```php
<?php
class BinarySearchTree {
  protected ?Node $root;

  public function __construct() {
    $this->root = null;
  }

  public function getRoot(): ?Node {
    return $this->root;
  }

  // fungsi untuk menambahkan node baru pada BST
  // jika BST masih kosong, maka node baru akan menjadi root
  // jika BST tidak kosong, maka lakukan langkah berikut:
  // 1. cari node yang akan menjadi parent dari node baru
  // 2. jika data pada node baru lebih kecil dari data pada node parent, maka node baru akan menjadi left child dari node parent
  // 3. jika data pada node baru lebih besar dari data pada node parent, maka node baru akan menjadi right child dari node parent
  public function insert(int $data): void {
    $node = new Node($data);
    if ($this->root === null) {
      $this->root = $node;
      return;
    }
    // cari node yang akan menjadi parent dari node baru
    $current = $this->root;
    while (true) {
      if ($data < $current->getData()) {
        if ($current->getLeft() === null) {
          $current->setLeft($node);
          break;
        }
        $current = $current->getLeft();
      } else {
        if ($current->getRight() === null) {
          $current->setRight($node);
          break;
        }
        $current = $current->getRight();
      }
    }
  }

  public function find(int $data): ?Node {
    $current = $this->root;
    while ($current !== null) {
      if ($data === $current->getData()) {
        return $current;
      }
      if ($data < $current->getData()) {
        $current = $current->getLeft();
      } else {
        $current = $current->getRight();
      }
    }
    return null;
  }

  public function remove(int $data): void {
    $node = $this->find($data);
    if ($node === null) {
      return;
    }
    $parent = $node->getParent();
    if ($node->getLeft() === null && $node->getRight() === null) {
      if ($parent === null) {
        $this->root = null;
      } else {
        if ($parent->getLeft() === $node) {
          $parent->setLeft(null);
        } else {
          $parent->setRight(null);
        }
      }
    } elseif ($node->getLeft() === null) {
      if ($parent === null) {
        $this->root = $node->getRight();
      } else {
        if ($parent->getLeft() === $node) {
          $parent->setLeft($node->getRight());
        } else {
          $parent->setRight($node->getRight());
        }
      }
    } elseif ($node->getRight() === null) {
      if ($parent === null) {
        $this->root = $node->getLeft();
      } else {
        if ($parent->getLeft() === $node) {
          $parent->setLeft($node->getLeft());
        } else {
          $parent->setRight($node->getLeft());
        }
      }
    } else {
      $min = $node->getRight();
      while ($min->getLeft() !== null) {
        $min = $min->getLeft();
      }
      $this->remove($min->getData());
      $node->setData($min->getData());
    }
  }

  // traverse BST dengan preorder
  // visit root, traverse left subtree, traverse right subtree
  public function preorder(?Node $node): void {
    if ($node === null) {
      return;
    }
    echo $node->getData() . ' ';
    $this->preorder($node->getLeft());
    $this->preorder($node->getRight());
  }

  // traverse BST dengan inorder
  // traverse left subtree, visit root, traverse right subtree
  public function inorder(?Node $node): void {
    if ($node === null) {
      return;
    }
    $this->inorder($node->getLeft());
    echo $node->getData() . " ";
    $this->inorder($node->getRight());
  }

  // traverse BST dengan postorder
  // traverse left subtree, traverse right subtree, visit root
  public function postorder(?Node $node): void {
    if ($node === null) {
      return;
    }
    $this->postorder($node->getLeft());
    $this->postorder($node->getRight());
    echo $node->getData() . " ";
  }

  public function traverse(Node $node, int $level = 0): void {
    // hanya jika node tidak null
    if ($node !== null) {
      // traverse ke kanan hanya jika node memiliki right child
      if ($node->getRight() !== null) {
        $this->traverse($node->getRight(), $level + 1);
      }
      // tampilkan node
      for ($i = 0; $i < $level; $i++) {
        echo "   ";
      }
      echo $node->getData() . PHP_EOL;
      // traverse ke kiri hanya jika node memiliki left child
      if ($node->getLeft() !== null) {
        $this->traverse($node->getLeft(), $level + 1);
      }
    }
  }
}
```

- Pada class __"BinarySearchTree"__ terdapat property __"root"__ untuk menampung node root dari tree. Class __"BinarySearchTree"__ memiliki beberapa method antara lain:

  - __"getRoot"__ untuk mengembalikan nilai dari property __"root"__. 
  - __"insert"__ untuk memasukkan data ke dalam tree. 
  - __"find"__ untuk mencari data pada tree. 
  - __"remove"__ untuk menghapus data pada tree. 
  - __"preorder"__ untuk melakukan traverse tree dengan preorder.
  - __"inorder"__ untuk melakukan traverse tree dengan inorder.
  - __"postorder"__ untuk melakukan traverse tree dengan postorder.
  - __"traverse"__ untuk menampilkan data pada tree.

- Selanjutnya kita buat file __"index.php"__ untuk menjalankan program. Ketikkan kode berikut:

```php
<?php
spl_autoload_register(function ($class) {
  require_once $class . '.php';
});

$bst = new BinarySearchTree();
foreach ([10, 5, 15, 3, 7, 12, 18, 1, 4, 6, 8, 11, 13, 16, 19] as $a) {
  $bst->insert($a);
}
$bst->traverse($bst->getRoot());

echo PHP_EOL;
echo 'Preorder: ' . PHP_EOL;
$bst->preorder($bst->getRoot());
echo PHP_EOL;
echo 'Inorder: ' . PHP_EOL;
$bst->inorder($bst->getRoot());
echo PHP_EOL;
echo 'Postorder: ' . PHP_EOL;
$bst->postorder($bst->getRoot());
```

- Pada kode di atas, kita membuat object dari class __"BinarySearchTree"__ dan memasukkan beberapa data ke dalam tree. Kemudian kita menampilkan isi dari tree dengan memanggil method __"traverse"__.

- Jika kita jalankan program dengan perintah __"php index.php"__ maka akan muncul output seperti berikut:

```bash
        19
      18
         16
   15
         13
      12
         11
10
         8
      7
         6
   5
         4
      3
         1
```

- Pada output di atas, kita dapat melihat bahwa data pada tree telah terurut secara ascending. Dimulai dari data terkecil hingga data terbesar. Node 10 merupakan node root dari tree. Node 5 dan 15 merupakan node anak dari node 10. Node 3 dan 7 merupakan node anak dari node 5. Node 12 dan 18 merupakan node anak dari node 15. 
- Node 1 dan 4 merupakan node anak dari node 3. Node 6 dan 8 merupakan node anak dari node 7. Node 11 dan 13 merupakan node anak dari node 12. Node 16 dan 19 merupakan node anak dari node 18.

## Tugas

- Buat class turunan dari class __"BinarySearchTree"__ dengan penambahan method:
  
    - __"getMin"__ untuk mengembalikan nilai data terkecil dari tree. 
    - __"getMax"__ untuk mengembalikan nilai data terbesar dari tree.
    - __"countBetween"__ untuk mengembalikan jumlah node yang berada diantara 10 -15.
    - __"countLeaf"__ untuk mengembalikan jumlah node yang tidak memiliki child.
