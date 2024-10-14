# Minpro-DPP
![Untitled Diagram drawio](https://github.com/user-attachments/assets/c41551fe-c216-4db3-a0a3-d523c100c039)

# penjelasan baris kode

```markdown

**Baris 1-2 :**
from prettytable import PrettyTable
from datetime import datetime

from prettytable import PrettyTable: Mengimpor kelas PrettyTable dari modul prettytable. Kelas ini digunakan untuk membuat tabel yang dapat dengan mudah dibaca dan ditampilkan dalam terminal.
from datetime import datetime      : Mengimpor kelas datetime dari modul datetime, yang memungkinkan kita untuk menangani operasi terkait tanggal dan waktu, seperti mendapatkan tanggal saat ini.

**Baris 3-10:**

pengguna = {
    'guru': {'kata_sandi': 'tes', 'peran': 'guru'},
    'faris': {'kata_sandi': '2409116055', 'peran': 'siswa'} 
}

daftar_tugas = []
daftar_kehadiran = []

pengguna        : Sebuah kamus (dictionary) yang menyimpan informasi login untuk dua jenis pengguna:
  Guru          : Memiliki kata sandi tes dan peran guru.
  Faris         : Merupakan siswa dengan kata sandi 2409116055.
daftar_tugas    : Sebuah list kosong yang akan digunakan untuk menyimpan tugas yang dibuat oleh guru.
daftar_kehadiran: Sebuah list kosong yang akan digunakan untuk menyimpan catatan kehadiran siswa.

**Baris 12-20:**

def login():
    nama_pengguna = input("Nama Pengguna: ")
    kata_sandi = input("Kata Sandi: ")
    if nama_pengguna in pengguna and pengguna[nama_pengguna]['kata_sandi'] == kata_sandi:
        print(f"\nLogin berhasil sebagai {pengguna[nama_pengguna]['peran']}\n")
        return pengguna[nama_pengguna]['peran'], nama_pengguna
    else:
        print("\nKredensial tidak valid\n")
        return None, None

login()       : Fungsi ini digunakan untuk mengautentikasi pengguna berdasarkan nama pengguna dan kata sandi yang dimasukkan.
Input pengguna: Mengambil nama pengguna dan kata sandi menggunakan fungsi input().
Validasi      : Memeriksa apakah nama_pengguna ada dalam kamus pengguna dan apakah kata sandi yang dimasukkan cocok. Jika keduanya benar, maka login berhasil.
Output        : Menampilkan pesan bahwa login berhasil dan mengembalikan peran serta nama pengguna.
Error Handling: Jika kredensial tidak valid, akan menampilkan pesan kesalahan dan mengembalikan None.

**Baris 22-33:**

def lihat_kehadiran():
    if not daftar_kehadiran:
        print("\nBelum ada data kehadiran yang dicatat.\n")
        return

    tabel = PrettyTable()
    tabel.field_names = ["Nama", "Tanggal", "Kehadiran"]
    for record in daftar_kehadiran:
        tabel.add_row([record["nama"], record["tanggal"], record["status"].capitalize()])
    print(f"\n{tabel}\n")

lihat_kehadiran(): Fungsi ini digunakan untuk menampilkan catatan kehadiran.
Cek Data         : Memeriksa apakah ada data kehadiran yang dicatat. Jika tidak ada, memberikan pesan yang sesuai.
Tabel Kehadiran  : Menggunakan PrettyTable untuk membuat tabel yang menampilkan nama, tanggal, dan status kehadiran.
Menampilkan Tabel: Mencetak tabel ke layar.
