# How to Fix Growtopia 5.15
How to fix the 'error connection' issue in Growtopia v5.15 (Private Server Only)

This is a library (build version) of [ENet for Growtopia](https://github.com/ZTzTopia/enet/tree/20193ae48ef4bf2e7829105d7f7c9f185e580619).
FYI: Growtopia recently released a significant update on the client side. In version 5.15, the server must support the new packet system for the client to connect to the ENet server.
FYI: Growtopia baru aja rilis versi baru yang buat login versi 5.16+ Error

## How to Fix / Cara Fix
## 1. Bukan Folder Source kalian, kalian cari, folder Enet. trus buka 

![image](https://github.com/user-attachments/assets/88fc4afe-390c-4e39-9831-0a195d5d9e8f)

Nah disini kan ada folder include tuh, itu hapus aja. trus file c/cpp nya hapus file file ini : 
```
callback.c
host.c
packet.c
compress.c
list.c
protocol.c
win32.c
```

## 2.Download repo ini trus extract

![image](https://github.com/user-attachments/assets/15b371aa-26f4-4730-abd4-26acc3743174)

Nah disitu kan ada file Include, sama Lib tuh, itu kalian copy/cut trus kalian paste di folder Enet tadi yang di source kalian

## 3.Kalian bukan Visual Studio / File .sln source kalian, lalu click tombol Projects->lalu click (nama-source) Properties

## 4.Lalu kalian ke bagian VC++ Directories
![image](https://github.com/user-attachments/assets/8704d039-b2e8-4505-a6df-cca808ee7676)

Trus kalian ke **External Include Directories** kalian Edit->New Line, trus tambahin Path Ke Folder include tadi, jadi contoh : 
D:\GTPS\InfinityPS\enet\include
trus click Okay, trus click **Apply**

Sekarang kalian ke bagian **Library Directores** click Edit->New Line, trus tambahin path ke Folder lib tadi, jadi contoh :
D:\GTPS\InfinityPS\enet\lib
click Okay, trus click **Apply**

## 5.Sekarang ke bagian **Linker->Input**
![image](https://github.com/user-attachments/assets/5631bf46-06c6-4067-9d61-fc9bd77b62d7)

Trus ke bagian **Additional Dependencies**, lalu kalian click Edit, lalu **PALING ATAS** penting ini cuy harus paling atas, soalnya tadi gw tes paling bawah Error, kalian Tambahin
enet.lib
Jadi contoh : yang tadinya
dpp.lib
winmm.lib

kalian tambahin tuh jadi
enet.lib
dpp.lib
winmm.lib

Lalu kalian click OK, trus **Apply**

## 6. Kalian CTRL+F aja lalu cari 	
```cpp
server->checksum = enet_crc32;
```
Lalu diatasnya itu ditambahin ini
```cpp
server->usingNewPacketForServer = true; 
```
![image](https://github.com/user-attachments/assets/ba441e62-6cbe-4912-aff6-e97195d21d2b)

Jadinya kaya gitu

## 7. Add the data `type2|1` to your `server_data.php` (HTTP).
Kalo itu di text file 

:![image](https://github.com/user-attachments/assets/da61cb7f-d396-4d6f-a70d-7210b8e1b479)

Kalo itu di Https/js file : 

![image](https://github.com/user-attachments/assets/994f26ad-e09a-488d-ab86-c577fa94db7c)




## Credit
Special thanks to this awesome person:
- [ZTzTopia](https://github.com/ZTzTopia)
- [@RainBolt1](https://t.me/RainBolt1)
- **[GTPSHax/Oxygen]** (https://github.com/GTPSHAX)
- [IkazuGt](https://github.com/ikazuGt)
