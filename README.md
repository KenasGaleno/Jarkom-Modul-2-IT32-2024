# Jarkom-Modul-2-IT32-2024

- Muhammad Kenas Galeno Putra (5027231069)
- Veri Rahman (5027231088)

Topologi IT32
![Screenshot 2024-10-03 032352](https://github.com/user-attachments/assets/a0226adb-891c-4ae4-adba-23c41c2e3d45)

1. Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave.

**Nusantara**

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


**Majapahit**

auto eth0

iface eth0 inet static

  address 10.79.1.2
  
  netmask 255.255.255.0
  
  gateway 10.79.1.1
  

up echo nameserver 192.168.122.1>/etc/resolv.conf


**Hayam Wuruk**


auto eth0 

iface eth0 inet static

  address 10.79.1.3
  
  netmask 255.255.255.0
  
  gateway 10.79.1.1
  

up echo nameserver 192.168.122.1 > /etc/resolv.conf


**Solok**


auto eth0

iface eth0 inet static

  address 10.79.1.4
  
  netmask 255.255.255.0
  
  gateway 10.79.1.1
  

up echo nameserver 192.168.122.1 > /etc/resolv.conf


**Srikandi**


auto eth0

iface eth0 inet static

  address 10.79.1.5
  
  netmask 255.255.255.0
  
  gateway 10.79.1.1
  

up echo nameserver 192.168.122.1 > /etc/resolv.conf


**Sriwijaya**


auto eth0

iface eth0 inet static

  address 10.79.3.2
  
  netmask 255.255.255.0
  
  gateway 10.79.3.1
  

up echo nameserver 198.162.122.1 > /etc/resolv.conf


**Albert Einstein**


auto eth0

iface eth0 inet static

  address 10.79.2.2
  
  netmask 255.255.255.0
  
  gateway 10.79.2.1
  

up echo nameserver 198.162.122.1 > /etc/resolv.conf


**Tanjung Kulai**


auto eth0

iface eth0 inet static

  address 10.79.2.3
  
  netmask 255.255.255.0
  
  gateway 10.79.2.1
  

up echo nameserver 192.168.122.1 > /etc/resolv.conf


**Bedahulu**


auto eth0

iface eth0 inet static

  address 10.79.2.4
  
  netmask 255.255.255.0
  
  gateway 10.79.2.1
  

up echo nameserver 192.168.122.1 > /etc/resolv.conf


**Kotalingga**


auto eth0

iface eth0 inet static

  address 10.79.2.5
  
  netmask 255.255.255.0
  
  gateway 10.79.2.1
  

up echo nameserver 192.168.122.1 > /etc/resolv.conf


