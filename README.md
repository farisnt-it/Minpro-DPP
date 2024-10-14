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

def catat_kehadiran(nama_pengguna):
    tanggal_hari_ini = datetime.now().strftime("%d-%m-%Y")
    
    if nama_pengguna == 'faris': 
        hadir = input("Apakah hadir (ya/tidak): ").strip().lower()
        if hadir in ['ya', 'tidak']:
            daftar_kehadiran.append({"nama": "Faris", "tanggal": tanggal_hari_ini, "status": hadir})
            print("\nKehadiran telah dicatat.\n")
        else:
            print("\nInput tidak valid. Harap masukkan 'ya' atau 'tidak'.\n")
    else:
        print("\nHanya Faris yang bisa mencatat kehadiran.\n")

catat_kehadiran(nama_pengguna): Fungsi ini digunakan untuk mencatat kehadiran siswa.
Tanggal Hari Ini              : Mengambil tanggal hari ini menggunakan datetime.now() dan mengubah formatnya menjadi dd-mm-yyyy.
Validasi Pengguna             : Memastikan bahwa hanya Faris yang dapat mencatat kehadiran.
Input Kehadiran               : Mengambil input apakah Faris hadir atau tidak.
Simpan Data                   : Menambahkan catatan kehadiran ke dalam daftar_kehadiran jika input valid.


**Baris 35-44:**

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

**Baris 46-56:**

def buat_tugas():
    nama_tugas = input("Masukkan nama tugas baru: ")
    while True:
        tenggat_waktu = input("Masukkan tenggat waktu (dd-mm-yyyy): ")
        try:
            datetime.strptime(tenggat_waktu, "%d-%m-%Y")
            break
        except ValueError:
            print("Format tanggal salah. Silakan masukkan kembali.")
    daftar_tugas.append({"tugas": nama_tugas, "tenggat_waktu": tenggat_waktu})
    print(f"\nTugas '{nama_tugas}' dengan tenggat waktu '{tenggat_waktu}' telah ditambahkan.\n")

buat_tugas()        : Fungsi ini digunakan untuk membuat tugas baru.
Input Nama Tugas    : Mengambil nama tugas dari input pengguna.
Input Tenggat Waktu : Meminta pengguna untuk memasukkan tenggat waktu dan memvalidasi format tanggal.
Error Handling      : Jika format tanggal salah, akan mengulangi permintaan hingga input valid.
Simpan Tugas        : Menambahkan tugas ke dalam daftar_tugas jika valid.

**Baris 58-66:**

def lihat_tugas():
    if not daftar_tugas:
        print("\nTidak ada tugas yang tersedia.\n")
        return
    tabel = PrettyTable()
    tabel.field_names = ["No", "Tugas", "Tenggat Waktu"]
    for i, task in enumerate(daftar_tugas, start=1):
        tabel.add_row([i, task["tugas"], task["tenggat_waktu"]])
    print(f"\n{tabel}\n")

lihat_tugas(): Fungsi ini digunakan untuk menampilkan daftar tugas yang telah dibuat.
Cek Tugas: Memeriksa apakah ada tugas yang tersedia. Jika tidak, memberikan pesan yang sesuai.
Tabel Tugas: Menggunakan PrettyTable untuk membuat tabel yang menampilkan nomor, nama tugas, dan tenggat waktu.
Menampilkan Tabel: Mencetak tabel ke layar.

**Baris 68-87:**

kelola_tugas(peran): Fungsi ini digunakan untuk mengelola tugas berdasarkan peran pengguna.
Menu untuk Guru: Jika pengguna adalah guru, menyediakan opsi untuk menambah atau melihat tugas.
Menu untuk Siswa: Jika pengguna adalah siswa, hanya dapat melihat tugas.

**Baris 89-106:**

def tampilkan_menu_guru():
    menu_guru = PrettyTable()
    menu_guru.field_names = ["No", "Opsi"]
    menu_guru.add_row(["1", "Mengelola Tugas"])
    menu_guru.add_row(["2", "Melihat Kehadiran"])
    menu_guru.add_row(["3", "Logout"])
    print("=== Menu Guru ===")
    print(menu_guru)

def tampilkan_menu_faris():
    menu_faris = PrettyTable()
    menu_faris.field_names = ["No", "Opsi"]
    menu_faris.add_row(["1", "Melihat dan Mengumpulkan Tugas"])
    menu_faris.add_row(["2", "Mencatat Kehadiran"])
    menu_faris.add_row(["3", "Memeriksa Kehadiran Hari Ini"])
    menu_faris.add_row(["4", "Logout"])
    print("=== Menu Faris ===")
    print(menu_faris)


pada kode baris ini bertujuan untuk membuat tempat user memilih opsi yang sudah di sediakan di prettytable baik role guru ataupun role siswa

**Baris 108-160:**

def main():
    while True:
        peran, nama_pengguna = login()

        if peran is None:
            continue

        while peran in ['guru', 'siswa']:
            if peran == 'guru':
                tampilkan_menu_guru()
                pilihan = input("Pilih opsi: ")

                if pilihan == '1':
                    kelola_tugas(peran)
                elif pilihan == '2':
                    lihat_kehadiran()  
                elif pilihan == '3':
                    print("\nLogging out...\n")
                    break
                else:
                    print("\nOpsi tidak valid. Silakan coba lagi.\n")

            elif peran == 'siswa' and nama_pengguna == 'faris':
                tampilkan_menu_faris()
                pilihan = input("Pilih opsi: ")

                if pilihan == '1':
                    kelola_tugas(peran)
                elif pilihan == '2':
                    catat_kehadiran(nama_pengguna) 
                elif pilihan == '3':
                    lihat_kehadiran()  
                elif pilihan == '4':
                    print("\nLogging out...\n")
                    break
                else:
                    print("\nOpsi tidak valid. Silakan coba lagi.\n")

        while True:
            lanjut_program = input("Ingin login lagi? (ya/tidak): ").strip().lower()
            if lanjut_program == "ya":
                print("")
                break
            elif lanjut_program == "tidak":
                print()
                print("Keluar dari program...")
                return
            else:
                print("Input tidak valid. Harap masukkan 'ya' atau 'tidak'.\n")
        print()

Deskripsi: Program ini merupakan implementasi sederhana untuk manajemen tugas dan kehadiran di lingkungan pendidikan.
Fungsi: Memungkinkan guru untuk mengelola tugas dan siswa untuk mencatat kehadiran dengan antarmuka berbasis teks.
Tujuan: Meningkatkan efisiensi dalam pengelolaan tugas dan kehadiran di sekolah atau lembaga pendidikan.

# Penjelasan flowchart

1. Start
Deskripsi: Titik awal dari alur program. Menandakan bahwa program dimulai.
2. Login
Deskripsi: Pengguna diminta untuk memasukkan nama pengguna dan kata sandi.
Keputusan: Apakah kredensial valid?
Ya: Lanjut ke langkah berikutnya.
Tidak: Kembali ke langkah login dan meminta pengguna untuk mencoba lagi.
3. Tentukan Peran Pengguna
Deskripsi: Setelah login berhasil, sistem menentukan apakah pengguna adalah guru atau siswa.
Keputusan:
Jika pengguna adalah guru, lanjut ke menu guru.
Jika pengguna adalah siswa, lanjut ke menu siswa.
4. Menu Guru
Deskripsi: Menampilkan opsi yang tersedia untuk guru.
Opsi:
Mengelola Tugas: Masuk ke proses pengelolaan tugas.
Melihat Kehadiran: Menampilkan data kehadiran siswa.
Logout: Mengakhiri sesi pengguna dan kembali ke langkah login.
5. Mengelola Tugas
Deskripsi: Guru dapat menambah atau melihat tugas.
Keputusan: Apakah guru ingin menambah tugas atau melihat tugas?
Menambah Tugas: Masuk ke langkah untuk membuat tugas baru.
Melihat Tugas: Menampilkan daftar tugas yang telah dibuat.
Kembali ke Menu: Kembali ke menu guru.
6. Menu Siswa
Deskripsi: Menampilkan opsi yang tersedia untuk siswa (Faris).
Opsi:
Melihat dan Mengumpulkan Tugas: Menampilkan daftar tugas yang diberikan.
Mencatat Kehadiran: Memungkinkan siswa untuk mencatat kehadiran.
Memeriksa Kehadiran Hari Ini: Menampilkan status kehadiran untuk hari tersebut.
Logout: Mengakhiri sesi pengguna dan kembali ke langkah login.
7. Mencatat Kehadiran
Deskripsi: Siswa (Faris) mencatat kehadiran dengan memberikan input tentang status kehadirannya (ya/tidak).
Keputusan: Apakah input valid?
Ya: Catat kehadiran dan kembali ke menu siswa.
Tidak: Berikan pesan kesalahan dan kembali ke langkah mencatat kehadiran.
8. Melihat Kehadiran
Deskripsi: Menampilkan data kehadiran yang telah dicatat.
Keputusan: Apakah ada data kehadiran?
Ya: Tampilkan tabel kehadiran.
Tidak: Tampilkan pesan bahwa belum ada data kehadiran yang dicatat.
9. Kembali ke Menu
Deskripsi: Setelah menyelesaikan tindakan (baik sebagai guru maupun siswa), sistem akan kembali ke menu yang sesuai.
Keputusan: Apakah pengguna ingin logout?
Ya: Kembali ke langkah login.
Tidak: Kembali ke menu sesuai peran.
10. End
Deskripsi: Titik akhir dari alur program. Menandakan bahwa program telah selesai dijalankan.

