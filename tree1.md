# Modul 7 - Tree -- Operasi Dasar Tree

Tujuan Pembelajaran: Mahasiswa dapat memahami operasi-operasi dasar yang ada dalam tree serta dapat menggunakannya dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan

## Materi

### Tree (Pohon)

- Tree adalah struktur data yang non-linear dan memiliki hirarki yang terdiri dari node-node yang saling berhubungan. Tree disusun dari node pusat, node struktural, dan subnode yang dihubungkan dengan garis lurus.

- Kita dapat menyatakan bahwa struktur data tree memiliki __root__ (akar), __brances__ (ranting), dan __leaves__ (daun). Root adalah node yang tidak memiliki parent, branches adalah node yang memiliki parent dan subnode, dan leaves adalah node yang memiliki parent dan tidak memiliki subnode.

![Tree](https://res.cloudinary.com/practicaldev/image/fetch/s--GLixMccZ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lolxr50mxeeh4uor8kpa.jpg)

- Beberapa istilah dalam struktur data Tree adalah:

  - __Parent__: Node yang menjadi induk dari node lain
  - __Child__: Node yang menjadi anak dari node lain
  - __Root__: Node paling atas yang tidak memiliki parent
  - __Leaf / Eksternal__: Node paling bawah yang tidak memiliki child
  - __Ancestor (Leluhur)__: Node yang merupakan parent dari node lain
  - __Descendant (Turunan)__: Node yang merupakan child dari node lain
  - __Sibling / Neighbour__: Node yang memiliki parent yang sama
  - __Internal__: Node yang memiliki child minimal satu
  - __Degree__: Jumlah child dari node
  - __Level__: Tingkat dari node dari root ke node tersebut. Level root adalah 0
  - __Subtree__: Tree yang merupakan bagian dari tree lain

- Beberapa operasi dasar dari struktur data Tree antara lain

  - __Create__: Membuat tree baru
  - __Insert__: Menambahkan node baru ke dalam tree
  - __Delete__: Menghapus node dari tree
  - __Search__: Mencari node dalam tree
  - __Preorder__: Melakukan traversal tree dengan cara root, left, right
  - __Inorder__: Melakukan traversal tree dengan cara left, root, right
  - __Postorder__: Melakukan traversal tree dengan cara left, right, root

- Beberapa jenis struktur data Tree adalah:
  - __Binary Tree__: Tree yang setiap node hanya memiliki maksimal 2 child
  - __General Tree__: Tree yang setiap node memiliki jumlah child yang tidak terbatas
  - __Balanced Tree__: Tree yang memiliki tinggi yang sama untuk setiap node
  - __Binary Search Tree__: Tree yang setiap node memiliki child yang lebih kecil dari parentnya di sebelah kiri dan lebih besar dari parentnya di sebelah kanan

- Contoh struktur data Tree

  ![Contoh Tree](https://media.geeksforgeeks.org/wp-content/uploads/20211127152300/imi-300x258.png)

- Pada gambar diatas, Node A adalah node root. Node B adalah parent dari D dan E. D dan E adalah sibling. D, E, F dan G adalah node leaf. A dan B adalah ancestor dari E. E dan G adalah descendant dari A. Level dari node E adalah 2.

### Aplikasi yang menggunakan Tree

- Tree digunakan dalam banyak aplikasi seperti:

  - Menyimpan data dalam bentuk hierarki
  - Spanning Tree: Tree yang digunakan untuk menghubungkan semua node dalam jaringan
  - Binary Search Tree: digunakan untuk pencarian data
  - Huffman Tree: digunakan untuk kompresi data
  - Expression Tree: digunakan untuk menyimpan ekspresi matematika
  - Syntax Tree: digunakan untuk menyimpan struktur data dari suatu program
  - Decision Tree: digunakan untuk membuat keputusan
  - B-Tree: digunakan untuk menyimpan data dalam bentuk index

### Praktikum

- Kita akan membuat program untuk menghitung jumlah node, jumlah leaf, dan jumlah tinggi dari tree. Pertama kali kita buat class __"Node"__ di file __"Node.php"__ yang berisi property __"data"__ dan __"children"__ yang merupakan array yang berisi node-node yang merupakan child dari node tersebut.

```php
<?php
class Node {
  private mixed $data;
  private array $children;
  private ?Node $parent;

  public function __construct(mixed $data) {
    $this->data = $data;
    $this->children = [];
    $this->parent = null;
  }

  public function addChild(Node $child): void {
    $this->children[] = $child;
  }

  public function removeChild(Node $child): void {
    $this->children = array_filter($this->children, function ($c) use ($child) {
      return $c !== $child;
    });
  }

  public function getData(): mixed {
    return $this->data;
  }

  public function getChildren(): array {
    return $this->children;
  }

  public function hasChildren(): bool {
    return count($this->children) > 0;
  }

  public function setParent(Node $parent): void {
    $this->parent = $parent;
  }

  public function getParent(): ?Node {
    return $this->parent;
  }
}
```

- Kemudian kita buat class __"Tree"__ di file __"Tree.php"__ yang berisi property __"root"__ yang merupakan node root dari tree.

```php
<?php
class Tree {
  protected Node $root;

  public function __construct(Node $root) {
    $this->root = $root;
  }

  public function getRoot(): Node {
    return $this->root;
  }
  
  // insert
  public function insert(Node $node, Node $parent): void {
    $parent->addChild($node);
  }

  // delete
  public function delete(Node $node): void {
    $node->getParent()->removeChild($node);
  }

  // search
  public function search(Node $node, mixed $data): ?Node {
    if ($node->getData() === $data) {
      return $node;
    }

    foreach ($node->getChildren() as $child) {
      $found = $this->search($child, $data);
      if ($found) {
        return $found;
      }
    }

    return null;
  }

  // traverse
  public function traverse(Node $node, callable $callback): void {
    $callback($node);

    foreach ($node->getChildren() as $child) {
      $this->traverse($child, $callback);
    }
  }
}
```

- Pada file __"Tree.php"__ terdapat beberapa method untuk melakukan operasi dasar dalam tree yaitu:
  
    - __insert__: untuk menambahkan node baru ke dalam tree
    - __delete__: untuk menghapus node dari tree
    - __search__: untuk mencari node dalam tree
    - __traverse__: untuk melakukan traversal tree

- Kemudian kita buat file __"index.php"__ untuk menjalankan program yang memanfaatkan class __"Tree"__ dan __"Node"__.

```php
<?php
spl_autoload_register(function ($class) {
  require_once $class . '.php';
});

$a = new Node('A');
$tree = new Tree($a);

$b = new Node('B');
$c = new Node('C');
$d = new Node('D');
$e = new Node('E');
$f = new Node('F');
$g = new Node('G');

$tree->insert($b, $a);
$tree->insert($c, $a);

$tree->insert($d, $b);
$tree->insert($e, $b);

$tree->insert($f, $c);
$tree->insert($g, $c);

echo 'Parent tiap node adalah: ' . PHP_EOL;
$tree->traverse($tree->getRoot(), function ($node) {
  if ($node->getParent()) {
    echo $node->getData() . ' -> ' . $node->getParent()->getData() . PHP_EOL;
  }
});
echo PHP_EOL;

echo 'Children setiap node adalah: ' . PHP_EOL;
$tree->traverse($tree->getRoot(), function ($node) {
  if ($node->hasChildren()) {
    echo $node->getData() . ' -> ' . implode(', ', array_map(function ($child) {
      return $child->getData();
    }, $node->getChildren())) . PHP_EOL;
  }
});
echo PHP_EOL;

echo 'Mencari parent node dengan data E: ' . PHP_EOL;
$found = $tree->search($tree->getRoot(), 'E');
if ($found) {
  echo $found->getData() . ' -> ' . $found->getParent()->getData() . PHP_EOL;
}
```

- Pada file __"index.php"__ diatas, kita membuat node __"A"__ sebagai root dari tree. Kemudian kita membuat node __"B"__, __"C"__, __"D"__, __"E"__, __"F"__, dan __"G"__. Kemudian kita memasukkan node-node tersebut ke dalam tree dengan memanggil method __"insert"__ yang ada di class __"Tree"__.

- Kemudian kita melakukan traversal tree dengan memanggil method __"traverse"__ yang ada di class __"Tree"__.

- Jika semua berjalan dengan baik, maka Anda akan melihat isi dari tree yang telah buat.

## Tugas

- Buatlah class turunan dari __"Tree"__ dan tambahkan method untuk menghitung jumlah node, jumlah leaf, dan jumlah tinggi dari tree.