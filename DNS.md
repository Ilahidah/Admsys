# DOMAIN NAME SERVER (DNS)
Kelompok:
- Ahmad Firdaus
- Farrah Labita
- Ilahidah Fah Ngestu

## Langkah-langkah menginstall DNS
1. Untuk memulai konfigurasi DNS pertama kita instal terlebih dahulu dengan cara  apt-get install bind9

2. Untuk mengecek instalan berhasil atau tidak dengan cara systemctl status bind9, jika seperti ini maka menandakan installasi yang kita lakukan berhasil

## Langkah-langkah konfigurasi DNS
1. Untuk mengkonfigurasi BIND9 kita dapat masuk ke direktori cd /etc/bind terlebih dahulu, Setelah itu ls untuk melihat list file di folder bind.

2. Edit file named.conf.local menggunakan perintah nano named.conf.local lalu isi dengan perintah sejenis dibawah ini:

   zone "farrah.com"{
          type master;
          file "/etc/bind/db.farrah";
   };
   zone "21.1.168.192"{
          type master;
          file "/etc/bind/db.192";
   };
   
   Di zone pertama isi dengan domain name yang akan kita gunakan untuk menamai server dan zone kedua isi dengan ip address dimulai dari bit terbelakang sampai terdepan.
   
3. Selanjutnya masukkan perintah cp db.127 db.192 dan cp db.local db.farrah. Perintah ini adalah perintah untuk menduplikat data db.127 (file hasil duplikasinya akan dinamai db.192) dan untuk untuk menduplikat data db.local (file hasil duplikasinya akan dinamai db.farrah).
   Lakukan pengecekan file baru tersebut dengan perintah ls.

4. Edit file db.192 dengan perintah nano db.192 lalu ganti semua localhost menjadi domain name yang diinginkan kemudian simpan konfigurasi db.192.

5. Edit file db.farrah dengan perintah nano db.farrah lalu ganti semua localhost menjadi domain name yang diinginkan kemudian simpan konfigurasi db.farrah.

6. Lanjutkan konfigurasi file resolv.conf dengan perintah nano /etc/resolv.conf.
   search farrah.com
   nameserver 192.168.1.1
   nameserver 8.8.8.8
   
7. Restart dns menggunakan systemctl restart bind9.

8. Kemudian beralih ke Windows anda. Masuk ke Control panel > jaringan dan internet > Network Sharing center ( lihat komputer dan perangkat jaringan) > change adapter settings.

9. Klik kanan pada Wi -Fi > properties > internet  protocol Version 4 (TCP/Ipv4) > klik Use the following DNS server addressing  isi ip address sesuai dengan domain yang sudah disetting di Debian.

10. Buka cmd tulis ping farrah.com jika seperti gambar di bawah maka konfigurasi DNS berhasil.
