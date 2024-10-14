from prettytable import PrettyTable
from datetime import datetime

# Informasi login pengguna (guru atau siswa Faris)
pengguna = {
    'guru': {'kata_sandi': 'tes', 'peran': 'guru'},
    'faris': {'kata_sandi': '2409116055', 'peran': 'siswa'}
}

# Data untuk tugas dan kehadiran
daftar_tugas = []
daftar_kehadiran = []

def login():
    nama_pengguna = input("Nama Pengguna: ")
    kata_sandi = input("Kata Sandi: ")
    if nama_pengguna in pengguna and pengguna[nama_pengguna]['kata_sandi'] == kata_sandi:
        print(f"\nLogin berhasil sebagai {pengguna[nama_pengguna]['peran']}\n")
        return pengguna[nama_pengguna]['peran'], nama_pengguna
    else:
        print("\nKredensial tidak valid\n")
        return None, None

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

def lihat_kehadiran():
    if not daftar_kehadiran:
        print("\nBelum ada data kehadiran yang dicatat.\n")
        return

    tabel = PrettyTable()
    tabel.field_names = ["Nama", "Tanggal", "Kehadiran"]
    for record in daftar_kehadiran:
        tabel.add_row([record["nama"], record["tanggal"], record["status"].capitalize()])
    print(f"\n{tabel}\n")

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

def lihat_tugas():
    if not daftar_tugas:
        print("\nTidak ada tugas yang tersedia.\n")
        return
    tabel = PrettyTable()
    tabel.field_names = ["No", "Tugas", "Tenggat Waktu"]
    for i, task in enumerate(daftar_tugas, start=1):
        tabel.add_row([i, task["tugas"], task["tenggat_waktu"]])
    print(f"\n{tabel}\n")

def perbarui_tugas():
    if not daftar_tugas:
        print("\nTidak ada tugas yang tersedia untuk diperbarui.\n")
        return

    lihat_tugas()
    no_tugas = int(input("Masukkan nomor tugas yang ingin diperbarui: "))
    
    if 1 <= no_tugas <= len(daftar_tugas):
        tugas_baru = input("Masukkan nama tugas baru: ")
        while True:
            tenggat_waktu = input("Masukkan tenggat waktu baru (dd-mm-yyyy): ")
            try:
                datetime.strptime(tenggat_waktu, "%d-%m-%Y")
                break
            except ValueError:
                print("Format tanggal salah. Silakan masukkan kembali.")
        
        daftar_tugas[no_tugas - 1] = {"tugas": tugas_baru, "tenggat_waktu": tenggat_waktu}
        print(f"\nTugas telah diperbarui menjadi '{tugas_baru}' dengan tenggat waktu '{tenggat_waktu}'.\n")
    else:
        print("\nNomor tugas tidak valid.\n")

def hapus_tugas():
    if not daftar_tugas:
        print("\nTidak ada tugas yang tersedia untuk dihapus.\n")
        return

    lihat_tugas()
    no_tugas = int(input("Masukkan nomor tugas yang ingin dihapus: "))
    
    if 1 <= no_tugas <= len(daftar_tugas):
        removed_task = daftar_tugas.pop(no_tugas - 1)
        print(f"\nTugas '{removed_task['tugas']}' telah dihapus.\n")
    else:
        print("\nNomor tugas tidak valid.\n")

def kelola_tugas(peran):
    if peran == 'guru':
        while True:
            print("\n=== Menu Tugas Guru ===")
            print("1. Tambah Tugas")
            print("2. Lihat Tugas")
            print("3. Perbarui Tugas")
            print("4. Hapus Tugas")
            print("5. Kembali")
            pilihan = input("Pilih opsi: ")

            if pilihan == '1':
                buat_tugas()
            elif pilihan == '2':
                lihat_tugas()
            elif pilihan == '3':
                perbarui_tugas()
            elif pilihan == '4':
                hapus_tugas()
            elif pilihan == '5':
                break
            else:
                print("\nOpsi tidak valid. Silakan coba lagi.\n")

    elif peran == 'siswa': 
        lihat_tugas()

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
    menu_faris.add_row(["1", "Melihat Tugas"])
    menu_faris.add_row(["2", "Mencatat Kehadiran"])
    menu_faris.add_row(["3", "Memeriksa Kehadiran Hari Ini"])
    menu_faris.add_row(["4", "Logout"])
    print("=== Menu Faris ===")
    print(menu_faris)

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

if __name__ == "__main__":
    main()
