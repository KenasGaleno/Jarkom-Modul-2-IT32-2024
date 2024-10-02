# Jarkom-Modul-2-IT32-2024

- Muhammad Kenas Galeno Putra (5027231069)
- Veri Rahman (5027231088)

Topologi IT32
![Screenshot 2024-10-03 032352](https://github.com/user-attachments/assets/a0226adb-891c-4ae4-adba-23c41c2e3d45)

1. Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave.

    **Nusantara**
    ```bash
    auto eth0
    
    iface eth0 inet dhcp
    
    
    auto eth1 
    
    iface eth1 inet static
    
      address 10.79.1.1
      
      netmask 255.255.255.0
      
    
    auto eth2
    
    iface eth2 inet static
    
      address 10.79.2.1
      
      netmask 255.255.255.0
      
    
    auto eth3
    
    iface eth3 inet static
    
      address 10.79.3.1
      
      netmask 255.255.255.0
      
    
    up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.79.0.0/16
    ```
    
    **Majapahit**
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.1.2
      
      netmask 255.255.255.0
      
      gateway 10.79.1.1
      
    
    up echo nameserver 192.168.122.1>/etc/resolv.conf
    ```
    
    **Hayam Wuruk**
    
    ```bash
    auto eth0 
    
    iface eth0 inet static
    
      address 10.79.1.3
      
      netmask 255.255.255.0
      
      gateway 10.79.1.1
      
    
    up echo nameserver 192.168.122.1 > /etc/resolv.conf
    ```
    
    **Solok**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.1.4
      
      netmask 255.255.255.0
      
      gateway 10.79.1.1
      
    
    up echo nameserver 192.168.122.1 > /etc/resolv.conf
    ```
    
    **Srikandi**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.1.5
      
      netmask 255.255.255.0
      
      gateway 10.79.1.1
      
    
    up echo nameserver 192.168.122.1 > /etc/resolv.conf
    ```
    
    **Sriwijaya**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.3.2
      
      netmask 255.255.255.0
      
      gateway 10.79.3.1
      
    
    up echo nameserver 198.162.122.1 > /etc/resolv.conf
    ```
    
    **Albert Einstein**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.2.2
      
      netmask 255.255.255.0
      
      gateway 10.79.2.1
      
    
    up echo nameserver 198.162.122.1 > /etc/resolv.conf
    ```
    
    **Tanjung Kulai**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.2.3
      
      netmask 255.255.255.0
      
      gateway 10.79.2.1
      
    
    up echo nameserver 192.168.122.1 > /etc/resolv.conf
    ```
    
    **Bedahulu**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.2.4
      
      netmask 255.255.255.0
      
      gateway 10.79.2.1
      
    
    up echo nameserver 192.168.122.1 > /etc/resolv.conf
    ```
    
    **Kotalingga**
    
    ```bash
    auto eth0
    
    iface eth0 inet static
    
      address 10.79.2.5
      
      netmask 255.255.255.0
      
      gateway 10.79.2.1
      
    
    up echo nameserver 192.168.122.1 > /etc/resolv.conf
    ```

2. Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.

   1. Pertama membuat
      ```bash
      nano /etc/bind/named.conf.local
      ```
      
   3. Isi dengan

      ```bash
            zone "sudarsana.it32.com" {
          type master;
          file "/etc/bind/it32/sudarsana.it32.com";
      };
      ```
      
   4. membuat directory
      
      ```bash
      mkdir -p /etc/bind/it32
      ```
      
   5. ```bash
      cp /etc/bind/db.local /etc/bind/it32/sudarsana.it32.com
      ```

   6. Edit file zona
  
      ```bash
      nano /etc/bind/it32/sudarsana.it32.com
      ```

   7. Edit
      
      ```bash
      ;
      ; BIND data file for local loopback interface
      ;
      $TTL    604800
      @       IN      SOA     sudarsana.it32.com. root.sudarsana.it32.com. (
                                    2         ; Serial
                               604800         ; Refresh
                                86400         ; Retry
                              2419200         ; Expire
                               604800 )       ; Negative Cache TTL
      ;
      @       IN      NS      sudarsana.it32.com.
      @       IN      A       10.79.1.4
      @       IN      AAAA    ::1
      www     IN      CNAME   sudarsana.it32.com.
      ```

   8. Restart

      ```bash
      service bind9 restart
      ```


3. Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.


   1. Masuk kedalam named.conf.local
      ```bash
      nano /etc/bind/named.conf.local
      ```
   2. Membuat configurasi Domain
      ```bash
      zone "pasopati.it32.com" {
      type master;
      file "/etc/bind/it32/pasopati.it32.com";
      };
      ```

   3. Copy db.local
      ```bash
      cp /etc/bind/db.local /etc/bind/it32/pasopati.it32.com
      ```
   4. Masuk ke direktori yang sudah dibuat
      ```bash
      cd /etc/bind/it32/
      ```
   5. Masuk domain yang dibuat
      ```bash
      nano pasopati.it32.com
      ```
   6. Isi dengan
      ```bash
      ;
      ; BIND data file for local loopback interface
      ;
      $TTL    604800
      @       IN      SOA     pasopati.it32.com. root.pasopati.it32.com. (
                                    2         ; Serial
                               604800         ; Refresh
                                86400         ; Retry
                              2419200         ; Expire
                               604800 )       ; Negative Cache TTL
      ;
      @       IN      NS      pasopati.it32.com.
      @       IN      A       10.79.2.5
      @       IN      AAAA    ::1
      www     IN      CNAME   pasopati.it32.com.
      ```
   7. Lakukan restart
      ```bash
      service bind9 restart
      ```
   8. check terus
       ```bash
       ping pasopati.it32.com
       ```

5. Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.

   1. Masuk kedalam named.conf.local
      ```bash
      nano /etc/bind/named.conf.local
      ```
   2. isi dengan configurasi
      ```bash
      zone "rujapala.it32.com" {
      type master;
      file "/etc/bind/it32/rujapala.it32.com";
      };
      ```
   3. Copy db.local ke etc/binnd ke dalam folder it32
      ```bash
      cp /etc/bind/db.local /etc/bind/it32/rujapala.it32.com
      ```
   4. Masuk ke direktori
      ```bash
      cd /etc/bind/it32/
      ```
   5. Masuk ke dalam domain yang dibuat
      ```bash
      nano rujapala.it32.com
      ```
   6. isi dengan
      ```bash
      ;
      ; BIND data file for local loopback interface
      ;
      $TTL    604800
      @       IN      SOA     rujapala.it32.com. root.rujapala.it32.com. (
                                    2         ; Serial
                               604800         ; Refresh
                                86400         ; Retry
                              2419200         ; Expire
                               604800 )       ; Negative Cache TTL
      ;
      @       IN      NS      rujapala.it32.com.
      @       IN      A       10.79.2.3
      @       IN      AAAA    ::1
      www     IN      CNAME   rujapala.it32.com.
      ```
   7. Restart
       ```bash
       service bind9 restart
       ```
   8. ping rujakala.it32,com (buat ngececk)
  
6. Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.

   1. ping.sudarsana.it32.com
   2. ping.rudapala.it32.com
   3. ping.pasopati.it32.com
  
7. Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).

  1. cd /etc/bind
  2. nano named.conf.local
  3. masukkan
           zone "2.79.10.in-addr.arpa" {
        type master;
        file "/etc/bind/it32/2.79.10.in-addr.arpa";
      };
   4. cd it32
   5. cp pasopati.it32.com 2.79.10.in-addr.arpa
   6. ls
   7. nano 2.79.10.in-addr.arpa
   8. masukkan
      ;
      ; BIND data file for local loopback interface
      ;
      $TTL    604800
      @       IN      SOA     pasopati.it32.com. root.pasopati.it32.com. (
                                    2         ; Serial
                               604800         ; Refresh
                                86400         ; Retry
                              2419200         ; Expire
                               604800 )       ; Negative Cache TTL
      ;
      2.79.10.in-addr.arpa.   IN  NS          pasopati.it32.com.
      5                       IN  PTR         pasopati.it32.com.

      
   9. service bind9 restart
       masuk ke client
   11. apt install dnsutils -y
   12. nano /etc/resolv.conf
   13. host -t PTR 10.79.2.5


           




