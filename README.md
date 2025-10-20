# <h1 align="center">Laporan Praktikum Struktur Data<br> Modul 5 SINGLY LINKED LIST (BAGIAN KEDUA) </h1>
<p align="center">Osha Alfida Valyana / 103112430202</p>

## Dasar Teori

Single Linked List adalah sebuah field pointer-nya hanya satu buah saja dan satu arah serta pada akhir node yang nodenya saling terhubung satu sama lain. Jadi Setiap node pada linked list mempunyai field yang berisi pointer ke node berikutnya, dan juga memiliki field yang berisi data. Node terakhir akan menunjuk ke NULL yang akan digunakan sebagai kondisi berhenti pada saat pembacaan isi linked list.

## Guided

### Soal 1

```cpp
#include <iostream>
using namespace std;

struct Buku {
    string isbn;
    string judul;
    string penulis;
    Buku* next;
};

class LinkedList {
private:
    Buku* head;

public:
    LinkedList() {
        head = nullptr;
    }

    void tambahBuku(string isbn, string judul, string penulis) {
        Buku* bukuBaru = new Buku();
        bukuBaru->isbn = isbn;
        bukuBaru->judul = judul;
        bukuBaru->penulis = penulis;
        bukuBaru->next = nullptr;

        if (head == nullptr) {
            head = bukuBaru;
        } else {
            Buku* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = bukuBaru;
        }
        cout << "\n Buku \"" << judul << "\" berhasil ditambahkan.\n";
    }

    void lihatBuku() {
        if (head == nullptr) {
            cout << "\n Tidak ada data buku.\n";
            return;
        }

        cout << "\n=== Daftar Buku ===\n";
        Buku* temp = head;
        while (temp != nullptr) {
            cout << "ISBN   : " << temp->isbn << endl;
            cout << "Judul  : " << temp->judul << endl;
            cout << "Penulis: " << temp->penulis << endl;
            cout << "---------------------------\n";
            temp = temp->next;
        }
    }

    void hapusBuku(string isbn) {
        if (head == nullptr) {
            cout << "\n Tidak ada buku untuk dihapus.\n";
            return;
        }

        Buku* temp = head;
        Buku* prev = nullptr;

        if (temp != nullptr && temp->isbn == isbn) {
            head = temp->next;
            delete temp;
            cout << "\n Buku dengan ISBN " << isbn << " berhasil dihapus.\n";
            return;
        }

        while (temp != nullptr && temp->isbn != isbn) {
            prev = temp;
            temp = temp->next;
        }

        if (temp == nullptr) {
            cout << "\n Buku dengan ISBN " << isbn << " tidak ditemukan.\n";
            return;
        }

        prev->next = temp->next;
        delete temp;
        cout << "\n🗑️ Buku dengan ISBN " << isbn << " berhasil dihapus.\n";
    }

    void perbaruiBuku(string isbn, string judulBaru, string penulisBaru) {
        Buku* temp = head;
        while (temp != nullptr) {
            if (temp->isbn == isbn) {
                temp->judul = judulBaru;
                temp->penulis = penulisBaru;
                cout << "\n Data buku dengan ISBN " << isbn << " berhasil diperbarui.\n";
                return;
            }
            temp = temp->next;
        }
        cout << "\n Buku dengan ISBN " << isbn << " tidak ditemukan.\n";
    }
};

int main() {
    LinkedList daftarBuku;
    int pilihan;
    string isbn, judul, penulis;

    do {
        cout << "\n==============================";
        cout << "\n     MENU BUKU";
        cout << "\n==============================";
        cout << "\n1. Tambah Buku";
        cout << "\n2. Hapus Buku";
        cout << "\n3. Perbarui Buku";
        cout << "\n4. Lihat Buku";
        cout << "\n5. Keluar";
        cout << "\n==============================";
        cout << "\nMasukkan pilihan: ";
        cin >> pilihan;
        cin.ignore(); 

        switch (pilihan) {
        case 1:
            cout << "\nMasukkan ISBN    : ";
            getline(cin, isbn);
            cout << "Masukkan Judul   : ";
            getline(cin, judul);
            cout << "Masukkan Penulis : ";
            getline(cin, penulis);
            daftarBuku.tambahBuku(isbn, judul, penulis);
            break;

        case 2:
            daftarBuku.lihatBuku();
            break;

        case 3:
            cout << "\nMasukkan ISBN buku yang ingin dihapus: ";
            getline(cin, isbn);
            daftarBuku.hapusBuku(isbn);
            break;

        case 4:
            cout << "\nMasukkan ISBN buku yang ingin diperbarui: ";
            getline(cin, isbn);
            cout << "Masukkan Judul baru   : ";
            getline(cin, judul);
            cout << "Masukkan Penulis baru : ";
            getline(cin, penulis);
            daftarBuku.perbaruiBuku(isbn, judul, penulis);
            break;

        case 5:
            cout << "\n Keluar dari program.\n";
            break;

        default:
            cout << "\n Pilihan tidak valid.\n";
        }
    } while (pilihan != 5);

    return 0;
}

```
 ⁠
⁠Output 
![output Soal 1](https://github.com/chafdv/Modul5/blob/main/output/guided.png)

Program ini bertujuan untuk mengelola data buku menggunakan Single Linked List. Setiap buku menyimpan data ISBN, judul, dan penulis dalam bentuk node yang saling terhubung. Melalui menu interaktif, pengguna dapat menambah, menampilkan, memperbarui, dan menghapus data buku. Program ini menunjukkan penerapan struktur data linked list dalam pengelolaan data yang lebih dinamis dan efisien.
---

## Unguided

### Soal 1

buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya

```cpp
#include <iostream>
using namespace std;

struct Node {
    string nama;
    string pesanan;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void tambahAntrian(string nama, string pesanan) {
    Node* newNode = new Node();
    newNode->nama = nama;
    newNode->pesanan = pesanan;
    newNode->next = nullptr;

    if (head == nullptr) {
        head = tail = newNode;
    } else {
        tail->next = newNode;
        tail = newNode;
    }

    cout << "Pembeli " << nama << " telah ditambahkan ke antrian.\n";
}

void layaniAntrian() {
    if (head == nullptr) {
        cout << "Antrian kosong, tidak ada yang bisa dilayani.\n";
        return;
    }

    Node* temp = head;
    cout << "Melayani pembeli: " << head->nama << " (Pesanan: " << head->pesanan << ")\n";
    head = head->next;
    delete temp;

    if (head == nullptr) {
        tail = nullptr;
    }
}

void tampilAntrian() {
    if (head == nullptr) {
        cout << "Antrian kosong.\n";
        return;
    }

    cout << "\nDaftar Antrian Pembeli:\n";
    Node* temp = head;
    while (temp != nullptr) {
        cout << "- " << temp->nama << " (" << temp->pesanan << ")\n";
        temp = temp->next;
    }
    cout << endl;
}

void cariPembeli(string namaDicari) {
    if (head == nullptr) {
        cout << "Antrian kosong.\n";
        return;
    }

    Node* temp = head;
    bool ditemukan = false;

    while (temp != nullptr) {
        if (temp->nama == namaDicari) {
            cout << "\nPembeli ditemukan!\n";
            cout << "Nama    : " << temp->nama << endl;
            cout << "Pesanan : " << temp->pesanan << endl;
            ditemukan = true;
            break; 
        }
        temp = temp->next;
    }

    if (!ditemukan)
        cout << "\nPembeli dengan nama \"" << namaDicari << "\" tidak ditemukan.\n";
}

int main() {
    int pilihan;
    string nama, pesanan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Cari Pembeli\n"; 
        cout << "5. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore(); 

        switch (pilihan) {
            case 1:
                cout << "Masukkan nama pembeli: ";
                getline(cin, nama);
                cout << "Masukkan pesanan: ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilAntrian();
                break;
            case 4:
                cout << "Masukkan nama pembeli yang ingin dicari: ";
                getline(cin, nama);
                cariPembeli(nama);
                break;
            case 5:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }
    } while (pilihan != 5);

    return 0;
}

```
 ⁠
⁠Output  
![output Soal 1](https://github.com/chafdv/Modul5/blob/main/output/unguided1.png)

Program di atas bertujuan untuk mengelola antrian pembeli menggunakan konsep Linked List. Setiap data pembeli terdiri dari nama dan pesanan. Program menyediakan menu untuk menambah pembeli ke antrian, melayani pembeli pertama, serta menampilkan seluruh antrian. Dengan struktur linked list, data dapat ditambah dan dihapus secara dinamis tanpa batasan jumlah antrian.
---

### Soal 2

Gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN
 
```cpp
#include <iostream>
using namespace std;

struct Node {
    string isbn;
    string judul;
    string penulis;
    Node* next;
};

class LinkedList {
private:
    Node* head;

public:
    LinkedList() {
        head = nullptr;
    }

    void tambahBuku(string isbn, string judul, string penulis) {
        Node* newNode = new Node;
        newNode->isbn = isbn;
        newNode->judul = judul;
        newNode->penulis = penulis;
        newNode->next = nullptr;

        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        cout << "Buku \"" << judul << "\" berhasil ditambahkan.\n";
    }

    void hapusBuku(string isbn) {
        Node* temp = head;
        Node* prev = nullptr;

        while (temp != nullptr && temp->isbn != isbn) {
            prev = temp;
            temp = temp->next;
        }

        if (temp == nullptr) {
            cout << "Buku dengan ISBN " << isbn << " tidak ditemukan.\n";
            return;
        }

        if (prev == nullptr) {
            head = temp->next;
        } else {
            prev->next = temp->next;
        }

        delete temp;
        cout << "Buku dengan ISBN " << isbn << " berhasil dihapus.\n";
    }

    void perbaruiBuku(string isbn) {
        Node* temp = head;

        while (temp != nullptr) {
            if (temp->isbn == isbn) {
                string judulBaru, penulisBaru;
                cout << "Masukkan judul baru (kosongkan jika tidak diubah): ";
                getline(cin, judulBaru);
                cout << "Masukkan penulis baru (kosongkan jika tidak diubah): ";
                getline(cin, penulisBaru);

                if (!judulBaru.empty())
                    temp->judul = judulBaru;
                if (!penulisBaru.empty())
                    temp->penulis = penulisBaru;

                cout << "Data buku berhasil diperbarui.\n";
                return;
            }
            temp = temp->next;
        }

        cout << "Buku dengan ISBN " << isbn << " tidak ditemukan.\n";
    }

    void lihatBuku() {
        if (head == nullptr) {
            cout << "Tidak ada buku dalam daftar.\n";
            return;
        }

        Node* temp = head;
        cout << "\n=== Daftar Buku ===\n";
        while (temp != nullptr) {
            cout << "ISBN     : " << temp->isbn << endl;
            cout << "Judul    : " << temp->judul << endl;
            cout << "Penulis  : " << temp->penulis << endl;
            cout << "-----------------------------\n";
            temp = temp->next;
        }
    }

    void cariBuku(string keyword) {
        if (head == nullptr) {
            cout << "Tidak ada buku dalam daftar.\n";
            return;
        }

        Node* temp = head;
        bool ditemukan = false;

        cout << "\nHasil pencarian untuk: \"" << keyword << "\"\n";
        cout << "-----------------------------\n";

        while (temp != nullptr) {
            if (temp->judul == keyword || temp->penulis == keyword || temp->isbn == keyword) {
                cout << "ISBN     : " << temp->isbn << endl;
                cout << "Judul    : " << temp->judul << endl;
                cout << "Penulis  : " << temp->penulis << endl;
                cout << "-----------------------------\n";
                ditemukan = true;
            }
            temp = temp->next;
        }

        if (!ditemukan) {
            cout << "Tidak ada buku yang cocok dengan \"" << keyword << "\".\n";
        }
    }
};

int main() {
    LinkedList daftarBuku;
    int pilihan;
    string isbn, judul, penulis, keyword;

    do {
        cout << "\n===== MENU BUKU =====\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku\n";
        cout << "3. Perbarui Buku\n";
        cout << "4. Lihat Semua Buku\n";
        cout << "5. Cari Buku\n"; 
        cout << "6. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore(); 

        switch (pilihan) {
        case 1:
            cout << "Masukkan ISBN: ";
            getline(cin, isbn);
            cout << "Masukkan Judul: ";
            getline(cin, judul);
            cout << "Masukkan Penulis: ";
            getline(cin, penulis);
            daftarBuku.tambahBuku(isbn, judul, penulis);
            break;

        case 2:
            cout << "Masukkan ISBN yang akan dihapus: ";
            getline(cin, isbn);
            daftarBuku.hapusBuku(isbn);
            break;

        case 3:
            cout << "Masukkan ISBN yang akan diperbarui: ";
            getline(cin, isbn);
            daftarBuku.perbaruiBuku(isbn);
            break;

        case 4:
            daftarBuku.lihatBuku();
            break;

        case 5: 
            cout << "Masukkan judul / penulis / ISBN yang dicari: ";
            getline(cin, keyword);
            daftarBuku.cariBuku(keyword);
            break;

        case 6:
            cout << "Terima kasih!\n";
            break;

        default:
            cout << "Pilihan tidak valid.\n";
        }
    } while (pilihan != 6);

    return 0;
}
```

⁠Output 
![output Soal 2](https://github.com/chafdv/Modul5/blob/main/output/unguided2.png)

Program ini bertujuan untuk mengelola data buku menggunakan Single Linked List. Setiap buku memiliki data ISBN, judul, dan penulis. Melalui menu, pengguna dapat menambah, menghapus, memperbarui, menampilkan, dan mencari buku berdasarkan judul, penulis, atau ISBN. Program ini menunjukkan cara penggunaan linked list untuk menyimpan dan mengelola data secara dinamis dan efisien.

## Referensi

1.⁠ (https://daismabali.com/artikel_detail/54/1/Mengenal-Single-Linked-List-dalam-Struktur-Data.html) (diakses 20-10-2025)
