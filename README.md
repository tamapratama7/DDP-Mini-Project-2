
Mini Project dengan Tema Sistem Manajemen Event atau Acara

Nama  : Noor Hamsyah Pratama
NIM  : 2509116046
Kelas : B 2025

#FLOWCHART
<img width="1458" height="2303" alt="FL MinPro 2" src="https://github.com/user-attachments/assets/a8563296-388d-4daf-9dc0-c564ead17e3c" />

Flowchart di atas menunjukkan proses sistem login dan pengelolaan acara dalam aplikasi, dimulai dari langkah masuk hingga manajemen data acara. Setiap keadaan dijelaskan di bawah ini mengikuti urutan dan logika yang ada dalam diagram.

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
Jika sudah ada event, semua acara akan ditampilkan, lalu kembali ke menu.
Jika belum terdapat event, pengguna akan kembali diarahkan ke menu.

Jika memilih opsi 3 "Update Event"
Hanya dapat dilaksanakan oleh posisi "Manager". Apabila karyawan, akses tidak diberikan, lalu kembali ke menu.
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



#KODE
[MinPro 2.txt](https://github.com/user-attachments/files/22583490/MinPro.2.txt)
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
    return None



def menu(jabatan):
    print("Menu:")
    print("1. Tambah Event")
    print("2. Daftar Event")
    print("3. Update Event")
    print("4. Hapus Event")
    print("5. Keluar")

def tambah(Event):
    try:
        nama = input("Masukkan Nama Event: ")
        lokasi = input("Masukkan Lokasi Event: ")
        tanggal = input("Masukkan Tanggal Event(DD-MM-YYYY): ")
        waktu = input("Masukkan Waktu Event (00:00): ")
        Event.append([nama, lokasi, waktu, tanggal])
        print("Anda Berhasil Menambahkan Event")
    except ValueError:
        print("Tolong Masukkan Angka!")
    except IndexError:
        print("Nomor Event Tidak Ada")
    except KeyboardInterrupt:
        print("\nJangan Pencet CTRL C")
    except EOFError:
            print("\nJangan Pencet CTRL Z")

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
        return
    
    try:
        nomor = int(input("Masukkan Nomor Event: "))  
        index = nomor - 1 
        
        nomor_event = Event[index]

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
        return
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

    if jabatan is None:
        print("Login gagal! Program dihentikan.")
        return 
    
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




#OUTPUT 

<img width="797" height="1004" alt="Screenshot 2025-09-28 222634" src="https://github.com/user-attachments/assets/1092885a-163b-40f8-9a0b-c162995f6aea" />

Lanjutan Foto Ouput di Atas

<img width="510" height="834" alt="Screenshot 2025-09-28 231807" src="https://github.com/user-attachments/assets/6e28344e-2838-411f-8db8-286ce635fee4" />


TAMPILAN JIKA LOGIN USERNAME & PASSWORD SALAH SAMPAI KESEMPATAN HABIS dan JUGA JIKA PASSWORD TIDAK BERUPA ANGKA
<img width="474" height="367" alt="Screenshot 2025-09-28 224937" src="https://github.com/user-attachments/assets/77028912-4afa-4112-8bd2-a934d8b61afc" />

TAMPILAN JIKA KARYAWAN INGIN MENGAKSES UPDATE DAN HAPUS EVENT

<img width="449" height="621" alt="Screenshot 2025-09-28 222951" src="https://github.com/user-attachments/assets/7f147f4e-c51c-4fdd-942d-b86f3a6c44b3" />


TAMPILAN JIKA MENGINPUT YANG TIDAK ADA DI MENU

<img width="261" height="184" alt="Screenshot 2025-09-28 225132" src="https://github.com/user-attachments/assets/e6f6277b-c702-453b-818e-b4e596b81fc3" />

TAMPILAN JIKA MEMILIH OPSI NO 2, 3, DAN 4, TAPI BELUM ADA EVENT TERDAFTAR

<img width="541" height="789" alt="Screenshot 2025-09-28 225743" src="https://github.com/user-attachments/assets/34c37f00-9e92-43de-b774-2c6acf8d42bc" />

TAMPILAN JIKA DI OPSI 3, 4 MENGINPUT NOMOR EVENT YANG TIDAK ADA

<img width="272" height="564" alt="Screenshot 2025-09-28 230229" src="https://github.com/user-attachments/assets/7a7859e9-01e3-4b3e-9ba9-28049d88c550" />

TAMPILAN JIKA TERJADI KESALAHAN INPUT YANG SEHARUSNYA ANGKA

<img width="437" height="723" alt="Screenshot 2025-09-28 230511" src="https://github.com/user-attachments/assets/38364b8c-91ad-478c-9d02-b68530b5a903" />

TAMPILAN JIKA TERJADI KESALAHAN JIKA MEMENCET CTRL C DAN CTRL Z
-Login

<img width="384" height="214" alt="Screenshot 2025-09-28 230953" src="https://github.com/user-attachments/assets/51b93bed-c4dd-4209-80ec-f112c355e8a3" />

-Menu

<img width="275" height="372" alt="Screenshot 2025-09-28 231036" src="https://github.com/user-attachments/assets/d55e5453-09be-4604-b4ed-f09883caff86" />

-Tambah event

<img width="285" height="416" alt="Screenshot 2025-09-28 231113" src="https://github.com/user-attachments/assets/636aa9c8-5408-4ad7-9670-f249184f5d94" />

-Update Event

<img width="421" height="420" alt="Screenshot 2025-09-28 231214" src="https://github.com/user-attachments/assets/8dd3e0b6-0602-4842-963e-88a5bc930337" />

-Hapus Event

<img width="341" height="413" alt="Screenshot 2025-09-28 231255" src="https://github.com/user-attachments/assets/987c8973-bc82-47f5-8b0a-de468ca5b80b" />




TERIMA KASIH, THANK YOU


























