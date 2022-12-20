# Modul 4a - Circular Queue

Tujuan Pembelajaran: Mahasiswa dapat memahami dan menerapkan konsep circular queue dalam pemrograman dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- Hidup sehat, jaga jarak, pakai masker, cuci tangan, dan jangan lupa berdoa

## Materi

### Circular Queue

![Circular Queue](https://media.geeksforgeeks.org/wp-content/uploads/Circular-queue.png)

- Circular queue adalah queue yang menggunakan array untuk menyimpan elemen-elemen yang ada di dalamnya, namun circular queue memiliki kelebihan dibandingkan dengan queue biasa, dimana elemen terakhir dari queue dihubungkan dengan elemen pertama dari queue.

- Operasi yang digunakan pada circular queue sama seperti queue biasa, yaitu enqueue dan dequeue dengan prinsip FIFO (First In First Out). Circular queue disebut juga "Ring Buffer" (buffer berputar)

- Circular queue memiliki dua buah variabel tambahan, yaitu __front__ dan __rear__. Variabel __front__ akan menunjuk ke elemen pertama yang ada di dalam queue, sedangkan variabel __rear__ akan menunjuk ke elemen terakhir yang ada di dalam queue.

- Pseudocode untuk circular queue adalah sebagai berikut:

```text
- createQueue(Q)
- enqueue(Q, x)
- dequeue(Q)
- isEmpty(Q)
- isFull(Q)
```

- Pseudocode untuk createQueue adalah sebagai berikut:

```text
- Q.front = 0
- Q.rear = 0
```

- Pseudocode untuk enqueue adalah sebagai berikut:

```text
- if isFull(Q)
- then error "Queue is full"
- else
- Q.rear = (Q.rear + 1) mod Q.maxSize
- Q.data[Q.rear] = x
```

- Pseudocode untuk dequeue adalah sebagai berikut:

```text
- if isEmpty(Q)
- then error "Queue is empty"
- else
- Q.front = (Q.front + 1) mod Q.maxSize
- return Q.data[Q.front]
```

- Pseudocode untuk isEmpty adalah sebagai berikut:

```text
- if Q.front == Q.rear
- then return true
- else return false
```

- Pseudocode untuk isFull adalah sebagai berikut:

```text
- if (Q.rear + 1) mod Q.maxSize == Q.front
- then return true
- else return false
```

- Pseudocode untuk printQueue adalah sebagai berikut:

```text
- if isEmpty(Q)
- then error "Queue is empty"
- else
- i = Q.front
- while i != Q.rear
- do i = (i + 1) mod Q.maxSize
- print Q.data[i]
```

## Praktikum

- Buat file baru dengan file __"CircularQueue.php"__ dan kemudian ketikkan kode berikut:

```php
<?php
class CircularQueue {
  protected int $maxSize;
  protected int $front;
  protected int $rear;
  protected array $data;

  public function __construct($maxSize) {
    $this->maxSize = $maxSize;
    $this->front = 0;
    $this->rear = 0;
    $this->data = [];
  }

  public function enqueue($x) {
    if ($this->isFull()) {
      echo "Queue is full";
    } else {
      // ketika rear sudah mencapai batas maksimal, maka rear akan kembali ke 0, karena itu kita gunakan modulus
      $this->rear = ($this->rear + 1) % $this->maxSize;
      $this->data[$this->rear] = $x;
    }
  }

  public function dequeue() {
    if ($this->isEmpty()) {
      echo "Queue is empty";
    } else {
      $this->front = ($this->front + 1) % $this->maxSize;
      return $this->data[$this->front];
    }
  }

  public function isEmpty() {
    return $this->front == $this->rear;
  }

  public function isFull() {
    // penuh ketika rear sudah mencapai batas maksimal dan front sudah berada di depannya
    if (($this->rear + 1) % $this->maxSize == $this->front) {
      return true;
    }
    return false;
  }

  public function printQueue() {
    if ($this->isEmpty()) {
      echo "Queue is empty";
    } else {
      $i = $this->front;
      while ($i != $this->rear) {
        $i = ($i + 1) % $this->maxSize;
        echo $this->data[$i] . " ";
      }
    }
  }
}
```

- Kemudian buat file baru dengan nama __"index.php"__ dan ketikkan kode berikut:

```php
<?php
spl_autoload_register(function ($class_name) {
  include $class_name . '.php';
});

$queue = new CircularQueue(5);
$queue->enqueue(1);
$queue->enqueue(2);
$queue->enqueue(3);
$queue->enqueue(4);
$queue->enqueue(5);
$queue->printQueue();
echo PHP_EOL;

$queue->dequeue();
$queue->dequeue();
$queue->printQueue();
echo PHP_EOL;
```

## Tugas

- Buatlah class CircularQueue dengan ketentuan menggunakan pseudocode berikut:

```text
- enqueue(Q, x)
- dequeue(Q)
- isEmpty(Q)
- isFull(Q)
- printQueue(Q)
```

- Pseudocode untuk enqueue adalah sebagai berikut:

```text
- if isFull(Q)
- then error "Queue is full"
- else if
- if front == -1
- then front = rear = 0
- Q.data[rear] = x
- else if rear == Q.maxSize - 1 and front != 0
- then rear = 0
- Q.data[rear] = x
- else
- rear = rear + 1
- Q.data[rear] = x
```

- Pseudocode untuk dequeue adalah sebagai berikut:

```text
- if isEmpty(Q)
- then error "Queue is empty"
- else data = Q.data[front]
- Q.data[front] = -1
- if front == rear
- then front = rear = -1
- else if front == Q.maxSize - 1
- then front = 0
- else
- front = front + 1
- return data
```

- Pseudocode untuk isEmpty adalah sebagai berikut:

```text
- if front == -1
- then return true
- else return false
```

- Pseudocode untuk isFull adalah sebagai berikut:

```text
- if front == 0 and rear == Q.maxSize - 1
- then return true
- else if front == rear + 1
- then return true
- else return false
```

- Pseudocode untuk printQueue adalah sebagai berikut:

```text
- if isEmpty(Q)
- then error "Queue is empty"
- else if rear >= front
- then for i = front to rear
- print Q.data[i]
- else
- for i = front to Q.maxSize - 1
- print Q.data[i]
- for i = 0 to rear
- print Q.data[i]
```


