# ENet for Growtopia 5.15+ (Private Server Fix)

**Fixes the 'error connection' issue for Growtopia v5.15+ private servers by enabling support for the new packet system.**

---

## Table of Contents

- [About](#about)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage Example](#usage-example)
- [Troubleshooting](#troubleshooting)
- [Credits](#credits)

---

## About

This is a patched version of [ENet](https://github.com/ZTzTopia/enet/tree/20193ae48ef4bf2e7829105d7f7c9f185e580619) for Growtopia private servers.  
It enables compatibility with Growtopia client version 5.15 and above, which require a new packet system for successful connections.

---

## Prerequisites

- Visual Studio (recommended) or any C/C++ compiler supporting your platform
- Your Growtopia private server source code

---

## Installation

1. **Backup Your Existing ENet Folder**

   - Go to your source folder and locate the `enet` directory.
   - Backup or delete the following files:
     ```
     callback.c
     host.c
     packet.c
     compress.c
     list.c
     protocol.c
     win32.c
     ```
   - Also, remove the `include` folder inside `enet`.

   ![Locate and clean your enet folder](https://github.com/user-attachments/assets/88fc4afe-390c-4e39-9831-0a195d5d9e8f)

2. **Download and Extract This Repository**

   - Download the latest release or clone this repository.
   - Copy the `include` and `lib` folders from this repo into your `enet` directory.

   ![Extract and copy include/lib](https://github.com/user-attachments/assets/15b371aa-26f4-4730-abd4-26acc3743174)

3. **Configure Your Project in Visual Studio**

   - Open your `.sln` file in Visual Studio.
   - Go to `Project > Properties`.

   - **VC++ Directories:**
     - Add the path to the new `include` folder under `Include Directories`.
     - Add the path to the new `lib` folder under `Library Directories`.

     ![VC++ Directories](https://github.com/user-attachments/assets/8704d039-b2e8-4505-a6df-cca808ee7676)

   - **Linker > Input:**
     - Add `enet.lib` to the top of the `Additional Dependencies` list.

     ![Linker Input](https://github.com/user-attachments/assets/5631bf46-06c6-4067-9d61-fc9bd77b62d7)

---

## Configuration

1. **Enable the New Packet System**

   - In your server source code, search for:
     ```cpp
     server->checksum = enet_crc32;
     ```
   - Add the following line *above* it:
     ```cpp
     server->usingNewPacketForServer = 1; // Enables new packet system for Growtopia 5.15+
     ```

   ![Set usingNewPacketForServer in code](https://github.com/user-attachments/assets/ba441e62-6cbe-4912-aff6-e97195d21d2b)

2. **Update `server_data.php`**

   - Add the following line to your `server_data.php`:
     ```
     type2|1
     ```

   ![Add type2|1 to server_data.php](https://github.com/user-attachments/assets/da61cb7f-d396-4d6f-a70d-7210b8e1b479)

   - If you are using HTTPS/JS, add it as shown:

   ![Add type2|1 in JS](https://github.com/user-attachments/assets/994f26ad-e09a-488d-ab86-c577fa94db7c)

---

## Usage Example

```cpp
#include <enet/enet.h>

// ... your server setup code ...

server->usingNewPacketForServer = 1; // Enable new packet system
server->checksum = enet_crc32;
```

---

## Troubleshooting

- **Error:** "Error connection" when connecting with Growtopia 5.15+  
  **Solution:** Ensure `usingNewPacketForServer` is set to `1` before setting the checksum.

- **Linker Error:** `enet.lib` not found  
  **Solution:** Make sure the path to the `lib` folder is correctly set in your project properties, and `enet.lib` is at the top of the dependencies list.

- **Other Issues:**  
  - Double-check that you replaced all old ENet source files and headers.
  - Clean and rebuild your project after making changes.

---

## Credits

Special thanks to:
- [ZTzTopia](https://github.com/ZTzTopia)
- [@RainBolt1](https://t.me/RainBolt1)
- [GTPSHax/Oxygen](https://github.com/GTPSHAX)
- [IkazuGt](https://github.com/ikazuGt)

---

*For more help, open an issue or join the Growtopia private server community!*
