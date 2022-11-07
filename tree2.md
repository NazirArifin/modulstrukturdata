# Modul 8 - Binary Search Tree (BST) & Heap

Tujuan Pembelajaran: Mahasiswa dapat memahami konsep dan implementasi struktur data Heap dengan baik

## Persiapan

- Berdoa agar lancar dalam belajar, bagi yang membawa hp harap hp nya di _silence_ atau sekalian dimatikan
- __Struktur data bukan merupakan materi yang mudah, jadi jangan terlalu cepat putus asa jika tidak mengerti materi ini. Kesukaran materi ini akan membantu kita dalam memahami materi-materi yang lebih sulit di kemudian hari. Jadi, jangan putus asa dan teruslah belajar. Semangat!!!__

## Materi

### Binary Tree
- Binary Tree adalah struktur data yang terdiri dari node-node yang saling terhubung dengan relasi parent-child. Setiap node memiliki 2 buah child, yaitu left child dan right child.
- Binary Tree memiliki 3 macam jenis, yaitu:
  - Full Binary Tree: Binary Tree yang setiap node memiliki 2 buah child atau tidak memiliki child sama sekali
  - Complete Binary Tree: Binary Tree yang setiap level terisi secara penuh, kecuali level terakhir. Level terakhir terisi dari kiri ke kanan.
  - Perfect Binary Tree: Binary Tree yang setiap level terisi secara penuh, dan setiap node memiliki 2 buah child.
  - Balanced Binary Tree: Binary Tree yang memiliki tinggi yang sama di setiap levelnya. Jika tinggi dari setiap levelnya berbeda, maka Binary Tree tersebut tidak disebut Balanced Binary Tree.

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
- Preorder Traversal: Proses traversal dimulai dari node induk, kemudian dilanjutkan ke node paling kiri, dan terakhir ke node paling kanan. Proses traversal ini akan menghasilkan data yang terurut secara descending.
- Postorder Traversal: Proses traversal dimulai dari node paling kiri, kemudian dilanjutkan ke node paling kanan, dan terakhir ke node induknya. Proses traversal ini akan menghasilkan data yang terurut secara descending.

![Traversal](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Preorder-from-Inorder-and-Postorder-traversals.jpg)

### Heap

- Heap adalah struktur data yang mirip dengan tree, namun memiliki sifat yang berbeda. Heap adalah struktur data yang mempunyai sifat _Complete Binary Tree_ , artinya setiap level dari tree tersebut terisi secara penuh, kecuali level terakhir. Level terakhir dari tree tersebut terisi dari kiri ke kanan. 
- Heap mempunyai dua jenis, yaitu _max heap_ dan _min heap_. _Max heap_ adalah tree yang mempunyai sifat dimana setiap node mempunyai nilai yang lebih besar dari node-node anaknya. _Min heap_ adalah tree yang mempunyai sifat dimana setiap node mempunyai nilai yang lebih kecil dari node-node anaknya. 
- Heap mempunyai dua operasi dasar, yaitu _insert_ dan _delete_. Operasi _insert_ digunakan untuk memasukkan data ke dalam tree. Operasi _delete_ digunakan untuk menghapus data dari tree. Operasi _delete_ mempunyai dua jenis, yaitu _delete max_ dan _delete min_. Operasi _delete max_ digunakan untuk menghapus node dengan nilai tertinggi dari tree. Operasi _delete min_ digunakan untuk menghapus node dengan nilai terendah dari tree.

![Heap](https://www.geeksforgeeks.org/wp-content/uploads/MinHeapAndMaxHeap.png)

## Praktikum

### Binary Search Tree

