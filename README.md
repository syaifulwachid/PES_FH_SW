(defun c:PES ()
  (initget "Prefix Suffix PrefixSpace SuffixSpace")
  (setq pilihan (getkword "\nPilih opsi [Prefix/Suffix/PrefixSpace/SuffixSpace]: "))
  
  (if pilihan
    (progn
      (setq teks (getstring T (strcat "\nMasukkan " pilihan ": ")))
      (princ (strcat "\nInput pengguna: '" teks "'")) ; Debugging
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

(vl-load-com)
(show-usage-instructions)
(princ "\nKetik PES untuk menjalankan fungsi Prefix/Suffix.")
(princ "\nKetik copylinkedinprofilelink untuk menyalin link profil LinkedIn.")
(princ)

; Cara Compile ke FAS
;(vlisp-compile 'st "C:/Users/VICTUS/OneDrive/Notepad++ Files/PES_FH_SW.lsp")
