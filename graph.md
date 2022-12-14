# Modul 9 - Struktur Data Graph

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep dasar struktur data graph, dan mampu mengimplementasikannya dengan baik.

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- __Struktur data bukan merupakan materi yang mudah, jadi jangan terlalu cepat putus asa jika tidak mengerti materi ini. Kesukaran materi ini akan membantu kita dalam memahami materi-materi yang lebih sulit di kemudian hari. Jadi, jangan putus asa dan teruslah belajar. Semangat!!!__

## Materi

### Struktur Data Graph

- Graph adalah struktur data yang terdiri dari node / vertice (simpul) dan edge (sisi). Node adalah titik yang terhubung dengan edge. Edge adalah garis yang menghubungkan dua node. Graph dapat berbentuk apapun, tetapi biasanya graph berbentuk seperti gambar di bawah ini.

![Graph](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5b/6n-graf.svg/220px-6n-graf.svg.png)

- Lebih formalnya, graph disusun dari kumpulan vertice (V) dan kumpulan edge (E) yang dinyatakan dalam notasi matematika sebagai berikut:

$$G = (V, E)$$

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

### Jenis Graph

- Finite Graph

  Finite Graph adalah graph yang jumlah node dan edge-nya terbatas. Misalnya, graph yang terdiri dari 10 node dan 20 edge.

- Infinite Graph
  
  Infinite Graph adalah graph yang jumlah node dan edge-nya tidak terbatas.

- Trivial Graph

  Trivial Graph adalah graph yang hanya terdiri dari satu node. Misalnya, graph yang terdiri dari node A saja.

- Simple Graph
  
  Simple Graph adalah graph yang tidak memiliki self loop dan parallel edge. Misalnya, jalur kereta api yang menghubungkan kota-kota yang berbeda-beda.

- Multigraph

  Multigraph adalah graph yang memiliki beberapa parallel edge tapi tidak memiliki self loop. 

- Null Graph

  Null Graph adalah ketika terdapat beberapa vertice yang tidak terhubung dengan edge sama sekali. Misalnya, graph yang terdiri dari node A, node B, node C, dan node D, tetapi tidak ada edge yang menghubungkan node A dengan node B, node A dengan node C, node A dengan node D, node B dengan node C, node B dengan node D, node C dengan node D.

- Complete Graph

  Complete Graph adalah graph yang setiap node terhubung dengan semua node lainnya. Misalnya, graph yang terdiri dari node A, node B, node C, dan node D, dan setiap node terhubung dengan semua node lainnya.

- Pseudograph

  Pseudograph adalah graph yang memiliki self loop dan parallel edge. Misalnya, graph yang terdiri dari node A, node B, node C, dan node D, dan setiap node terhubung dengan semua node lainnya, tetapi terdapat self loop dan parallel edge.

- Regular Graph

  Regular Graph adalah graph yang setiap node memiliki derajat yang sama. Misalnya, graph yang terdiri dari node A, node B, node C, dan node D, dan setiap node memiliki derajat 3.

- Bipartite Graph
  
  Bipartite Graph adalah graph yang dapat dibagi menjadi dua bagian yang tidak memiliki edge yang menghubungkan dua bagian tersebut. Misalnya, graph yang terdiri dari node A, node B, node C, dan node D, dan setiap node memiliki derajat 3, tetapi tidak ada edge yang menghubungkan node A dengan node B, node A dengan node C, node A dengan node D, node B dengan node C, node B dengan node D, node C dengan node D.

![Graph](https://media.geeksforgeeks.org/wp-content/uploads/bipartite.png)

- Labeled Graph

  Labeled Graph adalah graph yang memiliki label pada node dan edge. Misalnya, graph yang terdiri dari node A, node B, node C, dan node D, dan setiap node memiliki derajat 3, tetapi tidak ada edge yang menghubungkan node A dengan node B, node A dengan node C, node A dengan node D, node B dengan node C, node B dengan node D, node C dengan node D, dan setiap node memiliki label nama negara, setiap edge memiliki label jarak antara dua negara.

- Directed Graph

  Directed Graph adalah graph yang memiliki arah. Misalnya, edge yang menghubungkan node A dan node B hanya bisa bergerak dari node A ke node B, tetapi tidak bisa bergerak dari node B ke node A.

- Cyclic Graph

  Cyclic Graph adalah graph yang memiliki cycle.

### Perbedaan Tree dan Graph

| Perbandingan    | Graph                                                    | Tree                                        |
|-----------------|----------------------------------------------------------|---------------------------------------------|
| Definisi        | Struktur data non-liniear                                | Struktur data non-linier                    |
| Struktur        | Kumpulan node dan edge                                   | Kumpulan node dan edge                      |
| Edge            | Tiap node boleh memiliki sebanyak apapun edge            | Jika ada n node, maka jumlah edge pasti n-1 |
| Jenis Edge      | Boleh directed atau undirected                           | Selalu directed                             |
| Node Root       | Tidak ada node khusus yang menjadi Root                  | Ada node khusus yang menjadi root           |
| Bentuk Loop     | Bisa saja terbentuk sebuah loop                          | Tidak ada loop                              |
| Traversal       | Breadth-First Search (BFS), dan Depth-First Search (DFS) | In-order, Pre-order, atau Post-order        |
| Contoh aplikasi | Menemukan jalur terpendek dalam graph jaringan           | Decision tree                               |


## Praktikum

- Untuk penerapan graph, akan digunakan 