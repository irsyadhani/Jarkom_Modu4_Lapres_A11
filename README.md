# Jarkom_Modul4_Lapres_A11
Kelompok A11:
* _Irsyadhani Dwi Shubhi (0511184000022)_
* _Anggun Wahyuni (05111840000154)_

----------------------------------------------------------------
## Soal
* [VLSM](#vlsm)
* [CIDR](#cidr)
----------------------------------------------------------------
# VLSM

## Tabel Subnetting
![alt text](/img/tabel.png)

## Cisco Packet Tracer dengan metode VLSM

### Perhitungan Subnet

#### 1. Menentukan jumlah subnet pada topologi
![alt text](/img/vlsm_1.png)

#### 2. Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan
![alt text](/img/vlsm_2.png)

#### 3. Menghitung pembagian IP berdasarkan NID dan netmask menggunakan pohon serta melakukan subnetting
![alt text](/img/vlsm_3.png)

#### 4. Dari pohon tersebut, subnet akan mendapat pembagian IP sebagai berikut
![alt text](/img/vlsm_4.png)

#### 5. Pembagian IP server menggunakan IP DMZ adalah sebagai berikut
![alt text](/img/vlsm_5.png)

### Praktik

#### 1. Membuat topologi pada CPT
![alt text](/img/vlsm_6.png)

#
#### 2. Subnetting
Mengatur IP untuk masing-masing interface yang ada di setiap device sesuai dengan pembagian subnet pada pohon VLSM dengan menu Config > Interface > "nama interface". Contoh untuk mengatur IP pada interface KEDIRI yang terhubung dengan subnet A2, A3 dan Server.

Pada subnet A2, ROUTER KEDIRI terhubung dengan ROUTER BLITAR dan CLIENT LUMAJANG.
Karena subnet A2 memiliki Network ID 192.168.1.0, atur IP pada interface KEDIRI yang mengarah ke subnet A2 dengan 192.168.1.1
![alt text](/img/vlsm_7.png)

Atur IP pada interface BLITAR yang mengarah ke subnet A2 dengan 192.168.1.2
![alt text](/img/vlsm_8.png)

Atur IP pada CLIENT LUMAJANG yang mengarah ke KEDIRI dengan 192.168.1.3. Pengaturan IP dapat dibuat dengan cara masuk ke client > pilih tab desktop > pilih IP Configuration
![alt text](/img/vlsm_9.png)

Kemudian, ROUTER KEDIRI terhubung dengan SERVER MALANG. Karena SERVER MALANG mempunyai Network ID 10.151.73.100, atur IP pada interface KEDIRI yang mengarah ke SERVER MALANG dengan 10.151.73.101
![alt text](/img/vlsm_10.PNG)

Atur IP pada SERVER MALANG yang mengarah ke KEDIRI dengan 10.151.73.102
![alt text](/img/vlsm_11.png)

Lakukan hal yang sama untuk mengatur alamat IP setiap interface pada device yang ada dalam topologi.

#
#### 3. Routing
Atur routing seperti tabel berikut

![alt text](/img/vlsm_12.png)

Routing dapat dilakukan pada menu Config > Routing > Static pada device Router dengan menambahkan NID (network), netmask (mask) dan gateway (next hop) lalu menekan tombol Add. Pada static routing juga dibutuhkan default routing agar router dapat mengirimkan paket sesuai tujuan. Default routing dibutuhkan untuk router yang berada di bawah router utama (SURABAYA). Sebagai contoh router KEDIRI hanya mengenal A2, A3 dan server MALANG sehingga harus dikenalkan dengan subnet A1 dan juga dilakukan default routing
![alt text](/img/vlsm_13.png)

#
#### 4. Testing
Hasil testing

![alt text](/img/vlsm_14.png)

###
# CIDR

## Topologi Subnet
![alt text](/img/A11_CIDR_fix.jpg)

* B1: Gabungan subnet A1 dan A2
* B2: Gabungan subnet A6 dan A5
* B3: Gabungan subnet A12 dan A13
* C1: Gabungan subnet B1 dan A3
* C2: Gabungan subnet B2 dan A4
* C3: Gabungan subnet B3 dan A11
* D1: Gabungan subnet C1 dan C2
* D2: Gabungan subnet C3 dan A10
* E1: Gabungan subnet D1 dan A7
* E2: Gabungan subnet D1 dan A9
* F1: Gabungan subnet E1 dan A8
* G1: Gabungan subnet F1 dan E2

#
## Tree Subnet
![alt text](/img/A11_Tree.jpg)

#
## Pembagian IP

### Tabel Pembagian IP
![alt text](/img/A11_Tabel_Pembagian_IP.jpg)

### Tree Pembagian IP
![alt text](/img/Pembagian_IP_CIDR.jpg)

#
## UML dengan metode CIDR
* Visualisasi Setting UML 
![alt text](/img/A11_Setting_UML.jpg)

##
* Membuat `nano topologi.sh`
```
#Switch
uml_switch -unix switch0 > /dev/null < /dev/null &
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch6 > /dev/null < /dev/null &
uml_switch -unix switch7 > /dev/null < /dev/null &
uml_switch -unix switch8 > /dev/null < /dev/null &
uml_switch -unix switch9 > /dev/null < /dev/null &
uml_switch -unix switch10 > /dev/null < /dev/null &
uml_switch -unix switch11 > /dev/null < /dev/null &
uml_switch -unix switch12 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch14 > /dev/null < /dev/null &

#Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,'10.151.72.49' eth1=daemon,,,switch1 eth2=daemon,,,switch2 eth3=daemon,,,switch7 eth4=daemon,,,switch0 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch6 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3 eth1=daemon,,,switch4 eth2=daemon,,,switch5 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch7 eth1=daemon,,,switch8 eth2=daemon,,,switch12 eth3=daemon,,,switch13 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch8 eth1=daemon,,,switch9 eth2=daemon,,,switch11 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch9 eth1=daemon,,,switch10 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch13 eth1=daemon,,,switch14 mem=64M &

#Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch11 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO ,jarkom umid=MOJOKERTO  eth0=daemon,,,switch0 mem=64M &

#Klien
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch4 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch5 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch5 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch6 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch9 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch10 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch12 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch14 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch13 mem=64M &
```
##
* Membuat `nano bye.sh`
```
uml_mconsole SURABAYA halt
uml_mconsole PASURUAN halt 
uml_mconsole PROBOLINGGO halt
uml_mconsole BATU halt
uml_mconsole MADIUN halt
uml_mconsole KEDIRI halt
uml_mconsole BLITAR halt
uml_mconsole MALANG halt
uml_mconsole MOJOKERTO halt
uml_mconsole SAMPANG halt 
uml_mconsole SIDOARJO halt
uml_mconsole BANYUWANGI halt
uml_mconsole JEMBER halt
uml_mconsole BONDOWOSO halt
uml_mconsole JOMBANG halt 
uml_mconsole BOJONEGORO halt 
uml_mconsole NGANJUK halt 
uml_mconsole LUMAJANG halt 
uml_mconsole TULUNGAGUNG halt
```
* Uncomment ipv4forward pada setiap router di `nano /etc/sysctl.conf`
* Seperti contoh di Router Surabaya:
![alt text](/img/uncomment_surabaya.jpg)
##
* Penambahan setting network interface untuk setiap UML dengan mengetikkan `nano /etc/network/interfaces`
```
# SURABAYA
auto eth0
iface eth0 inet static
address 10.151.72.50
netmask 255.255.255.252
gateway 10.151.72.49

#A8/22
auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

#A9/30
auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

#A7/30
auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

#Server Mojokerto
auto eth4
iface eth4 inet static
address 10.151.73.97
netmask 255.255.255.252
PASURUAN
#A9/30
auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

#A11/30
auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

#A10/22
auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.252.0

# PROBOLINGGO
#A11/30
auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252
gateway 192.168.144.1

#A13/25
auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.252.128

#A12/21
auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0

# BATU
#A7/30
auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

#A3/30
auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

#A4/22
auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

#A5/23
auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0

# KEDIRI
#A3/30
auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.255.252
gateway 192.168.8.1

#A2/24
auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0

#Server Malang
auto eth2
iface eth2 inet static
address 10.151.73.101
netmask 255.255.255.252

# BLITAR
#A2/24
auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateway 192.168.4.1

#A1/22
auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.252.0

# MADIUN
#A5/23
auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

#A6/28
auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240

# MOJOKERTO
auto eth0
iface eth0 inet static
address 10.151.73.98
netmask 255.255.255.252
gateway 10.151.73.99

# MALANG
auto eth0
iface eth0 inet static
address 10.151.73.102
netmask 255.255.255.252
gateway 10.151.73.101

# SAMPANG
#A8/22
auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1

# BONDOWOSO
#A8/22
auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1

# JEMBER
#A12/21
auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1

# BANYUWANGI
#A12/21
auto eth0
iface eth0 inet static
address 192.168.128.3
netmask 255.255.248.0
gateway 192.168.128.1

# SIDOARJO
#A10/22
auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.252.0
gateway 192.168.192.1

# LUMAJANG
#A2/24
auto eth0
iface eth0 inet static
address 192.168.4.3
netmask 255.255.255.0
gateway 192.168.4.1

# TULUNGAGUNG
#A1/22
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateway 192.168.0.1

# NGANJUK
#A4/22
auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1

# BOJONEGORO
#A6/28
auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1

# JOMBANG
#A5/23
auto eth0
iface eth0 inet static
address 192.168.16.3
netmask 255.255.254.0
gateway 192.168.16.1
```
##
* Untuk menyetting routing nya membuat `nano route.sh`
```
# SURABAYA routing pada D1, D2, MALANG
route add -net 192.168.0.0 netmask 255.255.224.0 gw 192.168.32.2
route add -net 192.168.128.0 netmask 255.255.192.0 gw 192.168.192.2
route add -net 10.151.73.102 netmask 255.255.255.252 gw 192.168.32.2

# PASURUAN routing pada B2
route add -net 192.168.16.0 netmask 255.255.240.0 gw 192.168.144.2

# BATU routing pada B1, A6, MALANG
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.8.2
route add -net 192.168.18.0 netmask 255.255.255.240 gw 192.168.16.2
route add -net 10.151.73.102 netmask 255.255.255.252 gw 192.168.8.2

# KEDIRI routing pada A1
route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.4.2
```
##
* Restart network dengan mengetikkan `service networking restart` pada setiap UML
* Pada semua router jalankan `iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16`
* Cek routing dengan `ping its.ac.id`
##### Surabaya
![alt text](/img/sukses_surabaya.jpg)
##### Pasuruan
![alt text](/img/sukses_pasuruan.jpg)
##### Batu
![alt text](/img/sukses_batu.jpg)
##### Kediri
![alt text](/img/sukses_kediri.jpg)
