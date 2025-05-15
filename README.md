![a8479a922b151b03df56a6db105dc5dd](https://github.com/user-attachments/assets/f3ddd2eb-6f17-438c-a3bc-1e79fdedb64f)# How to Fix Growtopia 5.15
How to fix the 'error connection' issue in Growtopia v5.15 (Private Server Only)

This is a library (build version) of [ENet for Growtopia](https://github.com/ZTzTopia/enet/tree/20193ae48ef4bf2e7829105d7f7c9f185e580619).

FYI: Growtopia recently released a significant update on the client side. In version 5.15, the server must support the new packet system for the client to connect to the ENet server.

## How to Fix
1. Bukan Folder Source kalian, kalian cari, folder Enet, trus buka 
![image](https://github.com/user-attachments/assets/88fc4afe-390c-4e39-9831-0a195d5d9e8f)

2. In your ENet initialization, add the following:
```cpp
server->usingNewPacketForServer = true; ![image](https://github.com/user-attachments/assets/ba441e62-6cbe-4912-aff6-e97195d21d2b)

```
3. Add the data `type2|1` to your `server_data.php` (HTTP).
Kalo itu di text file :![image](https://github.com/user-attachments/assets/da61cb7f-d396-4d6f-a70d-7210b8e1b479)
Kalo itu di Https/js file : ![image](https://github.com/user-attachments/assets/994f26ad-e09a-488d-ab86-c577fa94db7c)




## Credit
Special thanks to this awesome person:
- [ZTzTopia](https://github.com/ZTzTopia)
- [@RainBolt1](https://t.me/RainBolt1)
- **[GTPSHax/Oxygen]** (https://github.com/GTPSHAX)
