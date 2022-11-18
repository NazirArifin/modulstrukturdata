# Modul 9 - Struktur Data Graph

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep dasar struktur data graph, dan mampu mengimplementasikannya dengan baik.

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- __Struktur data bukan merupakan materi yang mudah, jadi jangan terlalu cepat putus asa jika tidak mengerti materi ini. Kesukaran materi ini akan membantu kita dalam memahami materi-materi yang lebih sulit di kemudian hari. Jadi, jangan putus asa dan teruslah belajar. Semangat!!!__

## Materi

### Struktur Data Graph

- Graph adalah struktur data yang terdiri dari node / vertice (simpul) dan edge (sisi). Node adalah titik yang terhubung dengan edge. Edge adalah garis yang menghubungkan dua node. Graph dapat berbentuk apapun, tetapi biasanya graph berbentuk seperti gambar di bawah ini. Lebih formalnya, graph disusun dari kumpulan vertice (V) dan kumpulan edge (E) yang dinyatakan dalam notasi matematika sebagai berikut:

$$G = (V, E)$$

![Graph](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5b/6n-graf.svg/220px-6n-graf.svg.png)

- Graph dapat digunakan untuk merepresentasikan jaringan, misalnya jaringan komputer, jaringan listrik, jaringan telepon, jaringan jalan, dan lain-lain. Graph juga dapat digunakan untuk merepresentasikan hubungan antar objek, misalnya hubungan antar negara, hubungan antar orang, hubungan antar hewan, dan lain-lain.

- Beberapa istilah yang sering digunakan dalam graph adalah sebagai berikut:
  
  * Node / Vertice (simpul)

    Node adalah titik yang terhubung dengan edge. Node bisa memiliki label, misalnya nama negara, nama orang, nama hewan, dan lain-lain.

  * Edge (sisi)

    Edge adalah garis yang menghubungkan dua node. Edge bisa menunjukkan pasangan node yang berurutan atau tidak berurutan. 

  * Weight

    Weight adalah nilai yang menunjukkan kekuatan hubungan antara dua node. Misalnya, weight dari edge yang menghubungkan node A dan node B adalah 5, maka hubungan antara node A dan node B memiliki kekuatan 5. Weight juga bisa digunakan untuk menunjukkan jarak antara dua node. Misalnya, weight dari edge yang menghubungkan node A dan node B adalah 5, maka jarak antara node A dan node B adalah 5.

  * Directed Graph

    Directed Graph adalah graph yang memiliki arah. Misalnya, edge yang menghubungkan node A dan node B hanya bisa bergerak dari node A ke node B, tetapi tidak bisa bergerak dari node B ke node A.

  * Undirected Graph

    Undirected Graph adalah graph yang tidak memiliki arah. Misalnya, edge yang menghubungkan node A dan node B bisa bergerak dari node A ke node B atau dari node B ke node A.

  * Self Loop
  
    Self Loop adalah edge yang menghubungkan node dengan dirinya sendiri. Misalnya, edge yang menghubungkan node A dengan dirinya sendiri.

  * Parallel Edge
  
    Parallel Edge adalah edge yang menghubungkan dua node yang sama lebih dari satu kali. Misalnya, edge yang menghubungkan node A dan node B lebih dari satu kali.




