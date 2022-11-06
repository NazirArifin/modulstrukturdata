# Modul 1 - Stack -- Operasi Dasar Stack

Tujuan Pembelajaran: Mahasiswa dapat memahami operasi-operasi dasar yang ada dalam stack serta dapat menggunakannya dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan

## Materi

### Stack

- Stack merupakan kumpulan data yang diatas data yang lain seperti sebuah tumpukan. Dengan demikian stack merupakan struktur data yang menerapkan prinsip __LIFO__ (_Last In First Out_) atau data yang masuk terakhir akan dikeluarkan pertama kali.

- Untuk menambahkan data pada bagian atas tumpukan dilakukan operasi __push__, sedangkan untuk menghapus atau memindahkan data dari tempat atas maka dilakukan operasi __pop__.

### Praktikum

- Buat file baru dengan file __"Stack.php"__ dan kemudian ketikkan kode berikut:

```php
<?php
class Stack {
  private array $stack = [];
  private int $limit;
  private int $height = 0;

  public function __construct($limit = 10) {
    // set batas stack
    $this->limit = $limit;
  }

  public function push($item) {
    if ($this->height < $this->limit) {
      // set tinggi stack
      $this->height++;
      // masukkan item ke dalam stack
      $this->stack[$this->height] = $item;
    } else {
      throw new RunTimeException('Stack is full!');
    }
  }

  public function pop() {
    if ($this->isEmpty()) {
      // jika stack kosong
      throw new RunTimeException('Stack is empty!');
    } else {
      // jika stack tidak kosong
      // dapatkan item teratas yang akan dihapus
      $item = $this->top();
      // hapus item dari stack
      unset($this->stack[$this->height]);
      // set tinggi stack baru
      $this->height = $this->height - 1;
      return $item;
    }
  }

  public function top() {
    // dapatkan item teratas
    return $this->stack[$this->height];
  }

  public function getHeight() {
    // dapatkan tinggi stack
    return $this->height;
  }

  public function isEmpty() {
    // cek apakah stack kosong
    return empty($this->stack);
  }

  public function isFull() {
    // cek apakah stack penuh
    return $this->height === $this->limit;
  }

  public function clear() {
    // hapus semua item dari stack
    $this->stack = [];
    $this->height = 0;
  }
}
```

- Dengan kode diatas kita membuat stack yang dapat diisi sembarang tipe data (int, string, object, dsb) dan memiliki beberapa fungsi dasar antara lain:

  - ```push()```: menambah data baru
  - ```pop()```: menghapus data paling atas
  - ```top()```: mendapatkan data paling atas (tanpa menghapus data)
  - ```getHeigth()```: mendapatkan tinggi stack saat ini
  - ```isEmpty()```: mengecek apakah stack kosong
  - ```isFull()```: mengecek apakah stack penuh
  - ```clear()```: membersihkan / menghapus semua isi stack

- Beberapa contoh menggunakan stack diatas adalah ketikkan kode berikut di file __"index.php"__

```php
<?php
spl_autoload_register(function ($class) {
  include $class . '.php';
});

try {
  $stack = new Stack();
  $stack->push('one');
  $stack->push('two');

  echo $stack->top() . PHP_EOL;
  echo $stack->getHeight() . PHP_EOL;

  $stack->pop();

  echo $stack->top() . PHP_EOL;
  echo $stack->getHeight() . PHP_EOL;

  $stack->pop();
  $stack->pop();
} catch (RunTimeException $e) {
  echo $e->getMessage() . PHP_EOL;
}
```

- Eksekusi file __index.php__ dan Anda akan dapat melihat hasil dari penggunaan stack yang telah kita buat

## Tugas

- Buat method yang dapat memasukkan data lebih dari satu (__multiPush()__) dan mengeluarkan data lebih dari satu (__multiPop__)
- Buat aplikasi yang dapat menampilkan kalimat terbalik menggunakan stack diatas. Contoh: "__Saya beli mobil__" menjadi "__libom ileb ayaS__"
- Buat aplikasi yang mengubah desimal menjadi biner menggunakan stack diatas. Contoh: angka desimal __14__ diubah menjadi __1110__

