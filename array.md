# Modul 1 - Array -- Pengenalan Array di PHP

Tujuan Pembelajaran: Mahasiswa dapat mengetahui dan memahami penggunaan array di PHP dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan

## Materi

### Array (Larik)

- Array merupakan kumpulan data yang memiliki nama yang sama dan memiliki tipe data yang sama atau berbeda. Array adalah salah satu tipe data yang paling sering digunakan dalam bahasa pemrograman untuk menyimpan data, mengatur dan mengolah data.
- Array dapat dibuat dengan menggunakan tanda kurung siku `[]` atau dengan menggunakan fungsi `array()`. Pada bahasa pemrograman lain seperti Java atau C++, isi dan key array biasanya memiliki tipe data yang sama, namun di PHP kita dapat menggunakan string untuk key dan mencampur beragam tipe data dalam isi array. 
- Untuk inisialisasi array dapat menggunakan key maupun tidak, jika tidak menggunakan key maka array akan dianggap sebagai array numerik secara berurutan yang dimulai dari 0. Contoh:
```php
<?php
// array numerik
$angka = [1, 2, 3, 4, 5];
```
- Jika menggunakan key, maka digunakan tanda __=>__ untuk memisahkan key dan value. Contoh:
```php
<?php
$angka = [
  0 => 1,
  1 => 2,
  2 => 3,
  3 => 4,
  'lima' => 5
];
```
- Jika ada key array yang sama maka hanya yang terakhir yang akan digunakan. Untuk mengakses isi array dapat menggunakan tanda kurung siku `[]` dengan key yang diinginkan. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
echo $angka[0]; // 1
// mengubah isi array
$angka[0] = 10;
echo $angka[0]; // 10
echo $angka['lima']; // 5
```

- Fungsi __`count()`__ digunakan untuk menghitung jumlah elemen array. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
echo count($angka); // 5
```

### Operasi Dasar Array

- Untuk menambahkan elemen baru pada array dapat menggunakan fungsi __`array_push()`__ atau menggunakan notasi singkat __```$array[] = $data```__. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
array_push($angka, 6);
$angka[] = 7;
echo count($angka); // 7
```

- Untuk menghapus elemen array dapat menggunakan fungsi __`unset()`__ dengan key yang diinginkan atau menggunakan fungsi __```array_splice```__. Sedangkan untuk mengosongkan array dapat dilakukan dengan mengisi array dengan array kosong `[]` Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
unset($angka[0]);
array_splice($angka, 1, 1);
echo count($angka); // 3
$angka = []; // kosongkan array
```

- Perbedaan dari fungsi ```unset``` dan ```array_splice``` adalah fungsi ```unset``` hanya menghapus elemen array dengan key yang diinginkan, sedangkan fungsi ```array_splice``` menghapus elemen array dengan key yang diinginkan dan kemudian mengurutkan key array.

- Untuk menggabungkan dua buah array dapat menggunakan fungsi __`array_merge()`__. Contoh:
```php
<?php
$angka1 = [1, 2, 3, 4, 5];
$angka2 = [6, 7, 8, 9, 10];
$angka3 = array_merge($angka1, $angka2);
echo count($angka3); // 10
```

- Untuk mengecek apakah suatu elemen ada dalam array dapat menggunakan fungsi __`in_array()`__ atau __`array_search()`__. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
if (in_array(3, $angka)) {
  echo "3 ada dalam array";
}
if (array_search(3, $angka) !== false) {
  echo "3 ada dalam array";
}
```

- Untuk mengecek apakah suatu key ada dalam array dapat menggunakan fungsi __`array_key_exists()`__. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
echo array_key_exists(0, $angka); // 1
echo array_key_exists(6, $angka); // 
```

- Untuk memecah (_unpack_) array dapat menggunakan fungsi __`list()`__ atau menggunakan __```...$array```__ untuk mengekstrak array. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
list($a, $b, $c, $d, $e) = $angka;
echo $a; // 1
echo $b; // 2

$array = [1, 2, 3];
$array2 = [...$array, 4, 5]; // [1, 2, 3, 4, 5]
$array3 = [0, ...$array2, 101, 102]; // [0, 1, 2, 3, 4, 5, 101, 102]
```

### Mencacah Array

- Untuk mencacah array dapat menggunakan perulangan __`for`__ atau __`foreach`__. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
for ($i = 0; $i < count($angka); $i++) {
  echo $angka[$i] . " ";
}
echo PHP_EOL;
foreach ($angka as $a) {
  echo $a . " ";
}
```

- Untuk mencacah array dengan key dapat menggunakan perulangan __`foreach`__ dengan menggunakan notasi __`$key => $value`__. Contoh:
```php
<?php
$angka = [
  0 => 1,
  1 => 2,
  2 => 3,
  3 => 4,
  'lima' => 5
];
foreach ($angka as $key => $value) {
  echo $key . " => " . $value . PHP_EOL;
}
```

### Array Multi Dimensi

- Array multi dimensi adalah array yang berisi array lainnya. Contoh:
```php
<?php
$angka = [
  [1, 2, 3, 4, 5],
  [6, 7, 8, 9, 10],
  [11, 12, 13, 14, 15]
];
echo $angka[0][0]; // 1
```

### Fungsi Array di PHP

- Fungsi __`array_map()`__ digunakan untuk mengubah setiap elemen array dengan fungsi yang diberikan. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
$angka2 = array_map(function ($a) {
  return $a * 2;
}, $angka);
print_r($angka2); // Array ( [0] => 2 [1] => 4 [2] => 6 [3] => 8 [4] => 10 )
```

- Fungsi __`array_filter()`__ digunakan untuk menghapus elemen array yang tidak memenuhi kondisi. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
$angka2 = array_filter($angka, function ($a) {
  return $a % 2 == 0;
});
print_r($angka2); // Array ( [1] => 2 [3] => 4 )
```

- Fungsi __`array_reduce()`__ digunakan untuk mengurangi array menjadi satu nilai. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5];
$angka2 = array_reduce($angka, function ($a, $b) {
  return $a + $b;
});
echo $angka2; // 15
```

- Fungsi __`array_column()`__ digunakan untuk mengambil kolom dari array multi dimensi. Contoh:
```php
<?php
$angka = [
  ['nama' => 'Andi', 'umur' => 20],
  ['nama' => 'Budi', 'umur' => 21],
  ['nama' => 'Caca', 'umur' => 22],
];
$nama = array_column($angka, 'nama');
print_r($nama); // Array ( [0] => Andi [1] => Budi [2] => Caca )
```

- Fungsi __`array_flip()`__ digunakan untuk menukar key dan value dari array. Contoh:
```php
<?php
$angka = [
  'satu' => 1,
  'dua' => 2,
  'tiga' => 3,
];
$angka2 = array_flip($angka);
print_r($angka2); // Array ( [1] => satu [2] => dua [3] => tiga )
```

- Fungsi __`array_unique()`__ digunakan untuk menghapus elemen array yang duplikat. Contoh:
```php
<?php
$angka = [1, 2, 3, 4, 5, 1, 2, 3, 4, 5];
$angka2 = array_unique($angka);
print_r($angka2); // Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 )
```

## Praktikum

- Program untuk menghitung jumlah huruf vokal dan konsonan dari sebuah kalimat
```php
<?php
$kalimat = "Saya sedang belajar PHP";
$jumlahVokal = 0;
$jumlahKonsonan = 0;
for ($i = 0; $i < strlen($kalimat); $i++) {
  if (in_array($kalimat[$i], ['a', 'i', 'u', 'e', 'o'])) {
    $jumlahVokal++;
  } else if ($kalimat[$i] != ' ') {
    $jumlahKonsonan++;
  }
}
echo "Jumlah huruf vokal: " . $jumlahVokal . PHP_EOL;
echo "Jumlah huruf konsonan: " . $jumlahKonsonan . PHP_EOL;
```

- Program untuk menghitung jumlah huruf vokal dan konsonan dari sebuah kalimat dengan menggunakan fungsi __`array_count_values()`__
```php
<?php
$kalimat = "Saya sedang belajar PHP";
$jumlahVokal = 0;
$jumlahKonsonan = 0;
$jumlahHuruf = array_count_values(str_split($kalimat));
foreach ($jumlahHuruf as $key => $value) {
  if (in_array($key, ['a', 'i', 'u', 'e', 'o'])) {
    $jumlahVokal += $value;
  } else if ($key != ' ') {
    $jumlahKonsonan += $value;
  }
}
echo "Jumlah huruf vokal: " . $jumlahVokal . PHP_EOL;
echo "Jumlah huruf konsonan: " . $jumlahKonsonan . PHP_EOL;
```

- Program untuk menghitung jumlah huruf vokal dan konsonan dari sebuah kalimat dengan menggunakan fungsi __`str_split()`__ dan __`array_filter()`__ dan __`array_reduce()`__
```php
<?php
$kalimat = "Saya sedang belajar PHP";
$jumlahVokal = 0;
$jumlahKonsonan = 0;
$jumlahHuruf = str_split($kalimat);
$jumlahHuruf = array_filter($jumlahHuruf, function ($a) {
  return $a != ' ';
});
$jumlahVokal = array_reduce(array_filter($jumlahHuruf, function ($a) {
  return in_array($a, ['a', 'i', 'u', 'e', 'o']);
}), function ($a, $b) {
  return $a + 1;
});
$jumlahKonsonan = array_reduce(array_filter($jumlahHuruf, function ($a) {
  return !in_array($a, ['a', 'i', 'u', 'e', 'o']);
}), function ($a, $b) {
  return $a + 1;
});
echo "Jumlah huruf vokal: " . $jumlahVokal . PHP_EOL;
echo "Jumlah huruf konsonan: " . $jumlahKonsonan . PHP_EOL;
```

## Tugas 1

- Buat program yang menggunakan fungsi __`array_map()`__ untuk mengubah semua huruf pada sebuah kalimat menjadi huruf besar
- Buat program yang menggunakan fungsi __`array_filter()`__ untuk menghapus semua angka ganjil pada sebuah array
- Buat program yang menggunakan fungsi __`array_reduce()`__ untuk menghitung jumlah semua angka pada sebuah array
- Buat program yang menggunakan fungsi __`array_column()`__ untuk mengambil kolom nama dari array multi dimensi

## Tugas 2

- Terdapat data array seperti berikut:
```php
<?php
$data = [
  [
    'nama' => 'Andi',
    'umur' => 20,
    'hobi' => ['berenang', 'olahraga', 'main game'],
  ],
  [
    'nama' => 'Budi',
    'umur' => 21,
    'hobi' => ['nongkrong', 'makan', 'tidur'],
  ],
  [
    'nama' => 'Caca',
    'umur' => 22,
    'hobi' => ['hiking', 'berenang', 'bersepeda'],
  ],
  [
    'nama' => 'Deni',
    'umur' => 22,
    'hobi' => ['memancing', 'ngoding', 'menggambar'],
  ],
  [
    'nama' => 'Euis',
    'umur' => 24,
    'hobi' => ['membaca', 'menggambar', 'menonton film'],
  ],
];
```
- Tampilkan nama orang yang memiliki umur lebih dari 21 tahun menggunakan fungsi __`array_filter()`__
- Tampilkan nama orang yang memiliki hobi "Membaca" menggunakan fungsi __`array_column`__ dan __`array_filter()`__
- Tampilkan nama orang yang memiliki umur lebih dari 21 tahun dan memiliki hobi "Membaca" menggunakan fungsi __`array_filter()`__ dan __`array_column()`__
- Tampilkan hobi yang paling banyak diikuti oleh orang yang memiliki umur lebih dari 21 tahun menggunakan fungsi __`array_column()`__, __`array_filter()`__ dan __`array_reduce()`__
- Ubah semua nama menjadi huruf besar yang orang yang memiliki hobi memancing menggunakan fungsi __`array_column()`__, __`array_filter()`__ dan __`array_map()`__ kemudian tampilkan.











