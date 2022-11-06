# Modul 3 - Stack -- Evaluasi Ekspresi Aritmatika

Tujuan Pembelajaran: Mahasiswa dapat memahami penggunaan stack dalam evaluasi ekspresi aritmatika dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- Pahami teori dulu baru praktek, jangan kebalik, semua butuh proses, harus sabar
- Kalau kurang jelas, nyalakan lampu (takut lupa) atau pakai kaca matanya

## Materi
### Ekspresi Aritmatika

- Stack adalah struktur data yang sangat efektif untuk melakukan evaluasi aritmatika dalam bahasa pemrograman. Ekspresi aritmatika terdiri dari __Operand__ dan __Operator__. Selain itu ekspresi aritmatika juga bisa melibatkan tanda kurung seperti kurang buka dan kurung tutup.

- Contoh ekspresi aritmatika: __```A+(B-C)```__

- Untuk dapat melakukan evaluasi, Anda harus tahu tentang aturan urutan dalam ekspresi aritmatika. Aturan hak dari _operator_ aritmatika adalah:

| **Operator** | **Asosiasi**  | **Hak urutan**                     |
|--------------|---------------|------------------------------------|
| ^            | Kanan ke kiri | Paling tinggi diikuti oleh * dan / |
| *, /         | Kiri ke kanan | Paling tinggi diikuti oleh + dan - |
| +, -         | Kiri ke kanan | Paling rendah                      |

### Notasi Ekspresi Aritmatika

- Terdapat tiga notasi untuk merepresentasikan ekspresi aritmatika yaitu:
  
  - Notasi Infix
    
    Notasi Infix adalah penulisan ekspresi yang nyaman dimana setiap _operator_ diletakkan diantara _operand_. Contohnya: __```A+B```__, __```(C-D)```__ 

  - Notasi Prefix

    Notasi Prefix adalah penulisan ekspresi dimana _operator_ diletakkan sebelum _operand_. Notasi ini dikenalkan oleh seorang ahli matematika asal Polandia (_Polish_) sehingga sering dikenal sebagai __polish notation__. Contohnya: __```+AB```__, __```-CD```__

  - Notasi Postfix
    
    Notasi Postfix meletakkan _operator_ setelah _operand_ yang merupakan kebalikan dari _polish notation_ dan sering dikenal sebagai _reverse polish notation_. Contohnya: __```AB+```__, __```CD+```__

### Konversi Ekspresi Aritmatika ke Notasi Lainnya

- Contoh Konversi Notasi Aritmatika dari Notasi Infix ke notasi Prefix dan Postfix

| Notasi Infix | Notasi Prefix | Notasi Postfix |
|--------------|---------------|----------------|
| A*B          | *AB           | AB*            |
| (A+B)/C      | /+ABC         | AB+C/          |
| (A*B)+(D-C)  | +*AB-DC       | AB*DC-+        |

## Praktikum

- Buat file __"Stack.php"__ dan ketikkan kode berikut:

```php
<?php
class Stack {
  private array $stack = [];
  private int $limit;

  public function __construct($limit = 10) {
    $this->limit = $limit;
  }

  public function push($item) {
    if ($this->height < $this->limit) {
      $this->stack[$this->height] = $item;
      $this->height = $this->height + 1;
    } else {
      // STACK OVERFLOW
      throw new RunTimeException('Stack is full!');
    }
  }

  public function pop() {
    if ($this->isEmpty()) {
      // STACK UNDERFLOW
      throw new RunTimeException('Stack is empty!');
    } else {
      $item = $this->top();
      unset($this->stack[$this->height]);
      $this->height = $this->height - 1;
      return $item;
    }
  }

  public function top() {
    return $this->stack[$this->height];
  }

  public function isEmpty() {
    return empty($this->stack);
  }
}
```

- Buat file __"Converter.php"__ lalu ketikkan kode berikut:

```php
<?php
class Converter {
  private string $infix;
  private array $precedence = [
    '^' => 3,
    '*' => 2,
    '/' => 2,
    '+' => 1,
    '-' => 1,
    '(' => 0,
    ')' => 0
  ];

  public function __construct($infix) {
    $this->infix = $infix;
  }

  // operand = [0-9], atau [a-z]
  private function isOperand($char) {
    $char = strtolower($char);
    // ord adalah fungsi untuk mengubah karakter menjadi kode ASCII
    // 97-122 adalah kode ASCII untuk huruf a-z
    // 48-57 adalah kode ASCII untuk angka 0-9
    return (ord($char) >= 97 && ord($char) <= 122) || (ord($char) >= 48 && ord($char) <= 57);
  }

  private function isOperator($char) {
    return ($char == '+' || $char == '-' || $char == '*' || $char == '/' || $char == '^' || $char == '(' || $char == ')');
  }

  private function hasHigherPrecedence($operator1, $operator2) {
    return ($this->precedence[$operator1] > $this->precedence[$operator2]);
  }

  public function toPostfix() {
    $postfix = '';

    $operatorStack = new Stack(30);
    $outputStack = new Stack(30);

    try {
      for ($i = 0; $i < strlen($this->infix); $i++) {
        $char = $this->infix[$i];

        if ($this->isOperand($char)) {
          // jika char adalah operand, maka masukkan ke output stack
          $outputStack->push($char);
        } else if ($this->isOperator($char)) {
          // jika char adalah operator, maka lakukan operasi berikut:
          // 1. jika operator stack kosong, maka masukkan ke operator stack
          // 2. jika operator stack tidak kosong, maka lakukan operasi berikut:
          //    a. jika char adalah '(', maka masukkan ke operator stack
          //    b. jika char adalah ')', maka pop operator stack sampai ketemu '('
          //    c. jika char adalah operator, maka lakukan operasi berikut:
          //       i. jika char memiliki precedence lebih tinggi dari operator stack top, maka masukkan ke operator stack
          //       ii. jika char memiliki precedence lebih rendah dari operator stack top, maka pop operator stack dan masukkan ke output stack
          //       iii. jika char memiliki precedence sama dengan operator stack top, maka pop operator stack dan masukkan ke output stack          
          if ($operatorStack->isEmpty()) {
            $operatorStack->push($char);
          } else {
            if ($char == '(') {
              $operatorStack->push($char);
            } else if ($char == ')') {
              while (!$operatorStack->isEmpty() && $operatorStack->top() != '(') {
                $outputStack->push($operatorStack->pop());
              }
              if (!$operatorStack->isEmpty()) {
                $operatorStack->pop();
              }
            } else {
              if ($this->hasHigherPrecedence($char, $operatorStack->top())) {
                $operatorStack->push($char);
              } else {
                while (!$operatorStack->isEmpty() && !$this->hasHigherPrecedence($char, $operatorStack->top())) {
                  $outputStack->push($operatorStack->pop());
                }
                $operatorStack->push($char);
              }
            }
          }
        }
      }
      
      // pop semua operator stack dan masukkan ke output stack jika operator stack tidak kosong
      while (! $operatorStack->isEmpty()) {
        $outputStack->push($operatorStack->pop());
      }
    } catch (RunTimeException $e) {
      echo $e->getMessage() . PHP_EOL;
    }
    return $outputStack->toString();
  }

  private function reverseInfix() {
    // reverse infix, lalu ganti '(' dengan ')' dan sebaliknya
    $reverse = '';
    for ($i = strlen($this->infix) - 1; $i >= 0; $i--) {
      $char = $this->infix[$i];
      if ($char == '(') {
        $reverse .= ')';
      } else if ($char == ')') {
        $reverse .= '(';
      } else {
        $reverse .= $char;
      }
    }
    return $reverse;
  }

  public function toPrefix() {
    $prefix = '';
    // reverse infix
    $this->infix = $this->reverseInfix($this->infix);
    // convert infix to postfix
    $prefix = $this->toPostfix();
    // reverse postfix
    return strrev($prefix);
  }
}
```

- Kemudian untuk menggunakan class "Converter", buat file __"index.php"__ dengan isi seperti berikut:

```php
<?php
spl_autoload_register(function ($class) {
  include $class . '.php';
});


$infix = '2+3/4+5*(6-7)^8';
echo 'Infix: ' . $infix . PHP_EOL;
$converterPostfix = new Converter($infix);
echo 'Postfix: ' . $converterPostfix->toPostfix() . PHP_EOL;

$converterInfix = new Converter($infix);
echo 'Prefix: ' . $converterInfix->toPrefix() . PHP_EOL;
```

- Eksekusi file __"index.php"__, jika semua berjalan dengan baik maka akan muncul hasil dari proses postfix dan prefix dari infix yang dimasukkan.

## Tugas

- Buatlah class "Calculator" untuk menghitung hasil dari postfix dan prefix yang sudah dikonversi menggunakan struktur data "Stack" yang sudah dibuat sebelumnya.
