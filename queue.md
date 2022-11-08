# Modul 4 - Queue (Antrian)

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan konsep queue dalam pemrograman dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- Jika ada pertanyaan silahkan tanyakan kepada dosen praktikum, tapi sebelumnya pastikan sudah membaca materi yang ada di modul ini, jangan dikit-dikit tanya karena berarti: "ente kadang-kadang ente, wrrr.."

## Materi

### Queue (baca: kyu)

- Queue adalah struktur data yang berfungsi untuk menyimpan data secara berurutan, dimana data yang pertama kali masuk akan pertama kali keluar (__FIFO__) misalnya antrian di bank, antrian di toko, antrian di klinik, dll.

- Bagian antrian yang paling depan disebut dengan __front__ / __head__ dan bagian antrian yang paling belakang disebut dengan __rear__ / __tail__.

![Queue](https://media.geeksforgeeks.org/wp-content/uploads/20220816162225/Queue.png)

- Seperti _stack_, queue dapat direpresentasikan dengan array, namun untuk queue, elemen yang baru masuk akan diletakkan di bagian belakang array, sedangkan elemen yang keluar akan diletakkan di bagian depan array.

- Untuk mengimplementasikan queue, kita perlu mengetahui dua buah variabel, yaitu __front__ dan __rear__. Variabel __front__ akan menunjuk ke elemen pertama yang ada di dalam queue, sedangkan variabel __rear__ akan menunjuk ke elemen terakhir yang ada di dalam queue.

## Praktikum

- Buat file baru dengan file __"Queue.php"__ dan kemudian ketikkan kode berikut:

```php
<?php
class Queue {
  protected array $queue = [];
  protected int $limit;
  // front adalah index pertama queue dalam array
  protected int $front = 0;
  // rear adalah index elemen terakhir queue dalam array
  protected int $rear = 0;

  public function __construct($limit = 10)  {
    $this->limit = $limit;
  }

  public function isFull(): bool {
    return count($this->queue) == $this->limit;
  }

  public function isEmpty(): bool {
    return $this->rear == $this->front;
  }

  public function enqueue(mixed $item): void {
    if (! $this->isFull()) {
      $this->queue[$this->rear] = $item;
      // rear bergerak mundur ke belakang
      $this->rear = $this->rear + 1;
    }
  }

  // ketika menghapus elemen dari queue terdapat dua pendekatan:
  // pendekatan pertama: kita hapus elemen di head dan geser semua elemen ke kiri satu persatu
  // - ini tidak efisien karena kita harus menggeser elemen sebanyak jumlah elemen yang ada
  // pendekatan kedua: kita hapus elemen di head dan pindah head ke elemen berikutnya
  // - ini lebih efisien karena kita hanya perlu menggeser head ke elemen berikutnya
  // - namun, index elemen yang dihapus tidak dapat digunakan lagi
  //
  // disini kita akan menggunakan pendekatan kedua
  public function dequeue(): mixed {
    if ($this->isEmpty()) {
      throw new RunTimeException('Queue is empty!');
    } else {
      $item = $this->queue[$this->front];
      unset($this->queue[$this->front]);
      $this->front = $this->front + 1;
      return $item;
    }
  }

  public function printQueue(): string {
    return implode(', ', $this->queue);
  }
}
```

- Dengan kode diatas kita membuat enqueue yang dapat diisi sembarang tipe data dan memiliki beberapa method seperti __isFull()__, __isEmpty()__, __enqueue()__, __dequeue()__, dan __printQueue()__.

  - ```enqueue()``` berfungsi untuk menambahkan elemen ke dalam queue, jika queue penuh maka elemen tidak akan ditambahkan ke dalam queue.
  - ```dequeue()``` berfungsi untuk menghapus elemen dari queue, jika queue kosong maka akan muncul pesan error.
  - ```printQueue()``` berfungsi untuk mencetak isi dari queue.
  - ```isFull()``` berfungsi untuk mengecek apakah queue penuh atau tidak.
  - ```isEmpty()``` berfungsi untuk mengecek apakah queue kosong atau tidak.

- Beberapa contoh menggunakan queue diatas adalah ketikkan kode berikut di file __"index.php"__:

```php
<?php
spl_autoload_register(function ($class_name) {
  include $class_name . '.php';
});

try {
  $queue = new Queue();
  $queue->enqueue('First');
  $queue->enqueue('Second');
  $queue->enqueue('Third');

  echo 'Isi Enqueue: ' . $queue->printQueue() . PHP_EOL;

  $queue->dequeue() . PHP_EOL;
  $queue->dequeue() . PHP_EOL;

  echo 'Isi Enqueue: ' . $queue->printQueue() . PHP_EOL;

  $queue->dequeue() . PHP_EOL;

  $queue->dequeue() . PHP_EOL;
} catch (RunTimeException $e) {
  echo $e->getMessage() . PHP_EOL;
}
```

- Eksekusi file __"index.php"__ dan Anda akan dapat melihat hasil dari penggunaan queue yang telah kita buat bersama.

## Tugas

- Buat class turunan dari class __Queue__ yang memodifikasi method __dequeue()__ sehingga __head__ tidak bergeser ke elemen berikutnya, namun elemen lain dan __tail__ yang menggeser ke kiri.
- Buat class __Queque__ yang mengimplementasikan __enqueue()__ dan __dequeue()__ menggunakan class __Stack__ yang ada pada modul sebelumnya dimana terdapat dua buah stack, yaitu __stack1__ dan __stack2__, dan __enqueue()__ dan __dequeue()__ menggunakan dua buah stack tersebut.
