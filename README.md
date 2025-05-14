# How to Fix Growtopia 5.15
How to fix the 'error connection' issue in Growtopia v5.15 (Private Server Only)

This is a library (build version) of [ENet for Growtopia](https://github.com/ZTzTopia/enet/tree/20193ae48ef4bf2e7829105d7f7c9f185e580619).

FYI: Growtopia recently released a significant update on the client side. In version 5.15, the server must support the new packet system for the client to connect to the ENet server.

## How to Fix
1. You must replace your ENet library with the modified ENet for Growtopia, as provided in this repository.
2. In your ENet initialization, add the following:
```cpp
server->usingNewPacketForServer = true;
```
3. Add the data `type2|1` to your `server_data.php` (HTTP).

## Credit
Special thanks to this awesome person:
- [ZTzTopia](https://github.com/ZTzTopia)
- [@RainBolt1](https://tm.me/RainBolt1)
