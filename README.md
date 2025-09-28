# DDP-Mini-Project-2
Mini Project dengan Tema Sistem Manajemen Event atau Acara

Nama  : Noor Hamsyah Pratama
NIM  : 2509116046
Kelas : B 2025


<img width="1458" height="2303" alt="FL MinPro 2" src="https://github.com/user-attachments/assets/a8563296-388d-4daf-9dc0-c564ead17e3c" />

Flowchart di atas menunjukkan proses sistem login dan pengelolaan acara dalam aplikasi, dimulai dari langkah masuk hingga manajemen data acara. Setiap keadaan dijelaskan di bawah ini mengikuti urutan dan logika yang ada dalam diagram.

Alur Inti
Pengguna mulai dari "Start" dan diarahkan untuk melakukan "Login" terlebih dahulu.
Setelah masuk, sistem memeriksa kebenaran username dan password. Jika benar, pengguna melanjutkan ke menu utama. Jika tidak, akan ada kesempatan untuk login kembali hingga habis, setelah itu akses akan ditolak dan proses login selesai.

Lanjut, apabila login sukses, pengguna ditampilakan lima opsi menu:
1. Tambah Event
2. Daftar Event
3. Update Event
4. Hapus Event
5. Keluar.

Jika memilih opsi 1 "Tambah Event"
Pengguna menginput informasi nama, tempat, tanggal, dan waktu event.
Acara kemudian ditambahkan dan kembali ke menu.

Jika memilih opsi 2 "Daftar Event"
Jika sudah ada event, semua acara akan ditampilkan. lalu kembali ke menu.
Jika belum terdapat event, pengguna akan kembali diarahkan ke menu.

Jika memilih opsi 3 "Update Event"
Hanya dapat dilaksanakan oleh posisi "Manager". Apabila karyawan, akses tidak diberikan. lalu kembali ke menu.
Jika jabatan sesuai dan event sudah terdaftar, masukkan nomor event yang ingin diperbarui, kemudian masukkan nama, lokasi, tanggal, dan waktu baru sebelum event berhasil diperbarui.
Jika event belum tersedia, kembali ke menu utama.

Jika memilih opsi 4 "Hapus Event"
Hanya dapat dilakukan oleh posisi "Manager". Apabila karyawan, akses tidak diberikan. lalu kembali ke menu.
Jika event sudah terdaftar, masukkan nomor event yang ingin dihapus dan event tersebut akan dihapus.
Jika tidak ada event, kembali ke menu utama.

Jika memilih opsi 5 "Keluar"
Sistem menunjukkan pesan "Terima Kasih".

Apabila pilihan menu tidak valid, sistem akan mengarahkan pengguna kembali ke menu.

Jika login gagal sampai kesempatan habis, akses ditolak dan proses selesai.



[MinPro 2 DDP.txt](https://github.com/user-attachments/files/22583206/MinPro.2.DDP.txt)
users = {
    "tama" : {"password" : 123, "jabatan" : "manager"},
    "amat" : {"password" : 321, "jabatan" : "karyawan"}
}

def login():
    print("===LOGIN===")
    kesempatan = 3
    while kesempatan > 0 :
        try:
            username = input("Masukkan Username: ")
            password = int(input("Masukkan Password: "))
        except ValueError:
            print("Password Berupa Angka")
            continue
        except KeyboardInterrupt:
            print("\nJangan Pencet CTRL C")
            continue
        except EOFError:
            print("\nJangan Pencet CTRL Z")
            continue
        if username in users and users[username]['password'] == password:
            print("Login Berhasil")
            jabatan = users[username]["jabatan"]
            print(f"Selamat datang, {username}! Jabatan: {jabatan}")
            return jabatan
        else:
            kesempatan -= 1
            print("Login Gagal")
            if kesempatan == 0:
                print("Maaf, Coba Di ingat ingat lagi")
    return None



def menu(jabatan):
    print("Menu:")
    print("1. Tambah Event")
    print("2. Daftar Event")
    print("3. Update Event")
    print("4. Hapus Event")
    print("5. Keluar")  

def tambah(Event):
    nama = input("Masukkan Nama Event: ")
    lokasi = input("Masukkan Lokasi Event: ")
    tanggal = input("Masukkan Tanggal Event(DD-MM-YYYY): ")
    waktu = input("Masukkan Waktu Event (00:00): ")
    Event.append([nama, lokasi, waktu, tanggal])
    print("Anda Berhasil Menambahkan Event")

def tampilan(Event):
    if not Event:
        print("Belum Ada Event")

    else:
        nomor = 1
        for event in Event:
            print(f"{nomor}. {event[0]} | {event[1]} | {event[2]} | {event[3]}")
            nomor += 1

def update(Event):
    if not Event:
        print("Belum Ada Event")
    
    try:
        nomor = int(input("Masukkan Nomor Event: "))  
        index = nomor - 1  

        
        nama = input("Masukkan Nama Event Baru: ")
        lokasi = input("Masukkan Lokasi Event Baru: ")
        tanggal = input("Masukkan Tanggal Event Baru (DD-MM-YYYY): ")
        waktu = input("Masukkan Waktu Event (00:00): ")
        Event[index] = [nama, lokasi, tanggal, waktu]  
        print("Anda Berhasil Update Event")
    except ValueError:
        print("Tolong Masukkan Angka!")
    except IndexError:
        print("Nomor Event Tidak Ada")
    except KeyboardInterrupt:
        print("\nJangan Pencet CTRL C")
    except EOFError:
            print("\nJangan Pencet CTRL Z")


def hapus(Event):
    if not Event:
        print("Belum Ada Event")
    try:
        nomor = int(input("Masukkan Nomor Event: "))  
        index = nomor - 1  
        del Event[index]
        print("Anda Berhasil Menghapus Event")
    except ValueError:
        print("Tolong Masukkan Angka!")
    except IndexError:
        print("Nomor Event Tidak Ada")
    except KeyboardInterrupt:
        print("\nJangan Pencet CTRL C")
    except EOFError:
            print("\nJangan Pencet CTRL Z")

def pilih_menu():
    jabatan = login()

    Event = []
    while True:
        menu(jabatan)
        try:
            pilihan = int(input("Pilih Menu: "))
            if pilihan == 1:
                tambah(Event)
            elif pilihan == 2:
                tampilan(Event)
            elif pilihan == 3:
                if jabatan == 'manager':
                    update(Event)
                else:
                    print("AKSES DITOLAK!")
            elif pilihan == 4:
                if jabatan == 'manager':
                    hapus(Event)
                else:
                    print("AKSES DITOLAK!")
            elif pilihan == 5 :
                print("Terima Kasih")
                break
            else:
                print("Pilihan Tidak Valid")
        except ValueError:
            print("Tolong Masukkan Angka")
        except KeyboardInterrupt:
            print("\nJangan Pencet CTRL C")
        except EOFError:
            print("\nJangan Pencet CTRL Z")


pilih_menu()


