# Merah Putih Nusantara

## Soal Utama

Perhatikan potongan kode program berikut!

```cpp
int MERAH(int A, int B){
    if (B == 0){
        return A;
    }
    else{
        return MERAH(B,A%B);
    }
}

int PUTIH(int A, int B, int C){
    if(C == 0){
        return 0;
    }
    else if(MERAH(A,C) == B){
        return 1 + PUTIH(A,B,C-1);
    }
    else{
        return PUTIH(A,B,C-1);
    }
}

int NUSANTARA(int A,int B){
    return PUTIH(A,B,A);
}
```

### Soal (1/3)

Dari 5 pemanggilan berikut manakah yang hasil kembaliannya paling besar?

- [ ] `MERAH(24,4)`
- [ ] `MERAH(24,9)`
- [ ] `MERAH(24,17)`
- [ ] `MERAH(24,18)`
- [ ] `MERAH(24,34)`

### Soal (2/3)

Berapakah hasil kembalian dari pemanggilan `NUSANTARA(12,3)` ?

### Soal (3/3)

Berapakah hasil kembalian dari pemanggilan `NUSANTARA(12,3)` ?

## Penjelasan

Pada potongan program dapat diketahui bahwa, fungsi `MERAH` adalah salah satu fungsi umum yang dikenal sebagai fungsi euclidean. Fungsi tersebut digunakan untuk menentukan hasil *Greatest Common Divisor (GCD)* atau biasa dikenal sebagai Faktor Pembagi terBesar (FPB) dari 2 angka integer.

maka, agar lebih mempermudah kita dapat langsung merubah fungsi `MERAH` menjadi `FPB`

Maka, kode menjadi

```cpp
int FPB(int A, int B){
    if (B == 0){
        return A;
    }
    else{
        return FPB(B,A%B);
    }
}

int PUTIH(int A, int B, int C){
    if(C == 0){
        return 0;
    }
    else if(FPB(A,C) == B){
        return 1 + PUTIH(A,B,C-1);
    }
    else{
        return PUTIH(A,B,C-1);
    }
}

int NUSANTARA(int A,int B){
    return PUTIH(A,B,A);
}
```

Sehingga, kita dapat mulai menyelesaikan soal dengan mudah.

### Solusi (1/3)

Dari 5 opsi pilihan pada soal:

- [ ] `MERAH(24,4)`
- [ ] `MERAH(24,9)`
- [ ] `MERAH(24,17)`
- [ ] `MERAH(24,18)`
- [ ] `MERAH(24,34)`

Dapat kita kerjakan dengan mengetahui faktor dari angka 24, dimana:

$$24 = 2^3 \times 3 $$

Kemudian, observasi pasangan argumennya

$4 = 2^2$, maka hasil $\text{FPB}(24,4)=4$,
$9 = 3^2$, maka hasil $\text{FPB}(24,9)=3$,
$17 = 17$, maka hasil $\text{FPB}(24,17)=1$,
$18 = 2 \times 3 ^2$, maka hasil $\text{FPB}(24,18)=6$,
$34 = 17 \times 2$, maka hasil $\text{FPB}(24,34)=2$.

Maka kembalian terbesar:

- [ ] `MERAH(24,4)`
- [ ] `MERAH(24,9)`
- [ ] `MERAH(24,17)`
- [X] `MERAH(24,18)`
- [ ] `MERAH(24,34)`

## Solusi (2/3)

Sekarang kita akan mengobservasi fungsi `PUTIH`

```cpp
int PUTIH(int A, int B, int C){
    if(C == 0){
        return 0; 
    }
    else if(FPB(A,C) == B){
        return 1 + PUTIH(A,B,C-1);
    }
    else{
        return PUTIH(A,B,C-1);
    }
}
```

Mari pecah tiap *logic condition* yang ada.

```cpp
if(C == 0){
    return 0; 
}
```

Diketahui, saat kondisi logika ini penuhi maka program akan berhenti rekursi dan mengembalikan nilai dari *heap memory*.

```cpp
else if(FPB(A,C) == B){
    return 1 + PUTIH(A,B,C-1);
}
```

Diketahui, bahwa ketika hasil `FPB(A,C)` sama dengan `B` maka, *heap memory* akan bertambah 1.


```cpp
else if(FPB(A,C) == B){
    return 1 + PUTIH(A,B,C-1);
}
```

Diketahui, bahwa ketika kondisi logika dipenuhi yaitu hasil `FPB(A,C)` sama dengan `B` maka, *heap memory* akan bertambah 1, dan nilai C akan dikurangi 1.

```cpp
else{
    return PUTIH(A,B,C-1);
}
```

Diketahui, bahwa ketika tidak ada kondisi logika dipenuhi nilai C akan dikurangi 1.

Maka, dari observasi tersebut dapat dipastikan fungsi putih adalah fungsi untuk mencari berapa hasil $\text{FPB}$ yang sama dengan `B` untuk tiap `A` dari `0` hingga `A`.

Maka, karena $0 \rightarrow 12$ hanya memiliki 2 hasil $\text{FPB}$ yang bernilai 3. Maka kembalian akan menghasilkan $2$.

$$\therefore{\text{NUSANTARA}(24,3)=2}$$
## Solusi (3/3)

Maka, dengan penjelasan [solusi (2/3)](#solusi-23) 

$$2025 = 5^2 \times 3^4$$
$$135 = 5 \times 3^3 $$

Diperlukan untuk mencari kelipatan dari 135 yang memenuhi syarat tersebut. Maka, bisa dilakukan

$\text{FPB}(2025,135k)$, dimana $1 \geq k \leq \frac{2025}{135}$, menghasilkan $1 \geq k \leq 15$.

Maka, dapat mencari angka prima dan kelipatannya selain 3 dan 5 dari $1\rightarrow15$, termasuk 1.

Maka ditemukan 8 angka:

$$k={1,2,4,7,8,11,13,14}$$

Maka, hasil pengembalian adalah 8

$$\therefore{\text{NUSANTARA}(2025,135)=8}$$