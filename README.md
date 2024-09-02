---

## PES_FH_SW.fas Sourece Code Fungsi PES (Prefix/Suffix)

### Deskripsi
Fungsi `PES` adalah sebuah fungsi AutoLISP yang digunakan untuk menambahkan teks sebagai prefix (awalan) atau suffix (akhiran) pada objek teks yang dipilih di AutoCAD. Fungsi ini mendukung objek `TEXT` dan `MTEXT` dan memungkinkan pengguna untuk memilih apakah ingin menambahkan teks dengan atau tanpa spasi tambahan.

### Fitur Utama
- **Prefix**: Menambahkan teks di awal objek tanpa spasi tambahan.
- **Suffix**: Menambahkan teks di akhir objek tanpa spasi tambahan.
- **PrefixSpace**: Menambahkan teks di awal objek dengan spasi tambahan.
- **SuffixSpace**: Menambahkan teks di akhir objek dengan spasi tambahan.

### Penggunaan
1. **Memulai Fungsi**: Ketik `PES` di command line AutoCAD.
2. **Pilih Opsi**:
   - `Prefix`: Untuk menambahkan teks di awal tanpa spasi.
   - `Suffix`: Untuk menambahkan teks di akhir tanpa spasi.
   - `PrefixSpace`: Untuk menambahkan teks di awal dengan spasi.
   - `SuffixSpace`: Untuk menambahkan teks di akhir dengan spasi.
3. **Masukkan Teks**: Ketik teks yang ingin ditambahkan dan tekan `Enter`.
4. **Pilih Objek**: Seleksi objek `TEXT` atau `MTEXT` yang ingin diubah.
5. **Hasil**: Objek yang dipilih akan diperbarui dengan teks yang ditambahkan sesuai dengan opsi yang dipilih.

### Contoh Kode
```lisp
(defun c:PES ()
  (initget "Prefix Suffix PrefixSpace SuffixSpace")
  (setq pilihan (getkword "\nPilih opsi [Prefix/Suffix/PrefixSpace/SuffixSpace]: "))
  
  (if pilihan
    (progn
      (setq teks (getstring T (strcat "\nMasukkan " pilihan ": ")))
      (princ (strcat "\nInput pengguna: '" teks "'"))
      (if (> (strlen teks) 0)
        (progn
          (setq ss (ssget '((0 . "TEXT,MTEXT"))))
          (if ss
            (progn
              (setq i 0)
              (repeat (sslength ss)
                (setq obj (ssname ss i))
                (setq nilai (vla-get-TextString (vlax-ename->vla-object obj)))
                (cond
                  ((= pilihan "Prefix")
                   (setq nilai_baru (strcat teks nilai)))
                  ((= pilihan "Suffix")
                   (setq nilai_baru (strcat nilai teks)))
                  ((= pilihan "PrefixSpace")
                   (setq nilai_baru (strcat teks " " nilai)))
                  ((= pilihan "SuffixSpace")
                   (setq nilai_baru (strcat nilai " " teks)))
                )
                (vla-put-TextString (vlax-ename->vla-object obj) nilai_baru)
                (setq i (1+ i))
              )
              (princ (strcat "\n" (itoa (sslength ss)) " objek teks telah diubah."))
            )
            (princ "\nTidak ada objek teks yang dipilih.")
          )
        )
        (princ "\nTidak ada teks yang dimasukkan.")
      )
    )
    (princ "\nPilihan tidak valid.")
  )
  (princ)
)
```

### Cara Menggunakan
Setelah mengkopi kode ke dalam file LISP Anda, Anda dapat menggunakan fungsi ini di AutoCAD dengan cara berikut:
1. Jalankan AutoCAD dan buka command line.
2. Ketik `PES` dan pilih opsi yang diinginkan.
3. Masukkan teks yang ingin ditambahkan.
4. Pilih objek teks yang ingin diubah.
5. Teks pada objek akan diperbarui sesuai dengan opsi yang dipilih.

### Informasi Tambahan
- **Dibuat oleh**: Syaiful Wachid
- **Posisi**: Senior Project Designer di Fiberhome Indonesia
- **LinkedIn Profile**: [Syaiful Wachid](https://www.linkedin.com/in/syaiful-wachid-5373n/)

### Kode Tambahan
Fungsi `show-usage-instructions` dan `copylinkedinprofilelink` dapat digunakan untuk menampilkan petunjuk penggunaan dan menyalin tautan profil LinkedIn.

```lisp
(defun show-usage-instructions ()
  (alert (strcat
    "Cara menggunakan fungsi PES (Prefix/Suffix):\n\n"
    "1. Ketik 'PES' di command line AutoCAD.\n"
    "2. Pilih salah satu opsi:\n"
    "   - Prefix: Menambahkan teks di awal tanpa spasi tambahan\n"
    "   - Suffix: Menambahkan teks di akhir tanpa spasi tambahan\n"
    "   - PrefixSpace: Menambahkan teks di awal dengan spasi tambahan\n"
    "   - SuffixSpace: Menambahkan teks di akhir dengan spasi tambahan\n"
    "3. Masukkan teks yang diinginkan.\n"
    "4. Tekan Enter untuk menyelesaikan input.\n"
    "5. Pilih objek teks yang ingin diubah.\n\n"
    "Catatan: Fungsi ini bekerja dengan objek TEXT dan MTEXT.\n\n"
    "Dibuat oleh: Syaiful Wachid\n"
    "Senior Project Designer: Fiberhome Indonesia\n"
    "Linkedin Profile: https://www.linkedin.com/in/syaiful-wachid-5373n/"
  ))
)

(defun c:copylinkedinprofilelink ()
  (setq linkedin-url "https://www.linkedin.com/in/syaiful-wachid-5373n/")
  (alert (strcat "Salin link profil LinkedIn berikut:\n\n" linkedin-url))
  (princ (strcat "\nLink profil LinkedIn: " linkedin-url))
  (princ)
)
```

--- 

Ini akan memberikan penjelasan lengkap mengenai penggunaan serta informasi penggembangnya.
