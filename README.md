# ENet for Growtopia 5.15+ (Private Server Fix)

Fixes the 'error connection' issue for Growtopia v5.15+ private servers by enabling support for the new packet system.

## Table of Contents

- [About](#about)
- [Prerequisites](#prerequisites)
- [Building ENet with CMake](#building-enet-with-cmake)
- [Configuration](#configuration)
- [Usage Example](#usage-example)
- [Troubleshooting](#troubleshooting)
- [Credits](#credits)

## About

This is a patched version of ENet for Growtopia private servers.
It enables compatibility with Growtopia client version 5.15 and above, which require a new packet system for successful connections.

## Prerequisites

- CMake: Download and install from cmake.org.
- Visual Studio (recommended) or any C/C++ compiler supporting your platform.
- Your Growtopia private server source code.

## Building ENet with CMake

Instead of manually copying files, we'll build the ENet library using CMake.
- Prepare your ENet Source Folder
  - Go to your source folder and locate the enet directory.
  - Backup or delete any existing ENet build artifacts (like enet.lib, enet.dll, or previous build directories). It's generally best to start with a clean ENet source directory from this repository.
- Download and Extract This Repository
  - Download the latest release or clone this repository into your enet directory, replacing its contents. Make sure the CMakeLists.txt file is directly within your enet folder.
- Build with CMake (Command Line)
  - Open your command prompt or terminal.
  - Navigate to your enet directory:
    ```bash
    cd path/to/your/server/source/enet
    ```

  - Create a build directory and navigate into it:
    ```bash
    mkdir build && cd build
    ```

  - Run CMake to generate project files. For Visual Studio, you might use:
    ```bash
    cmake .. -G "Visual Studio 17 2022" # Adjust "Visual Studio 17 2022" to your VS version
    ```

    - Tip: To see available generators, run cmake --help.
  - Build the ENet project:
    ```bash
    cmake --build . --config Release # Or Debug, depending on your needs
    ```

    This command will compile ENet and generate enet.lib (and potentially enet.dll if configured for shared library) in the Release or Debug subfolder within your build directory.
- Configure Your Project in Visual Studio
  - Open your .sln file in Visual Studio.
  - Go to Project > Properties.
  - VC++ Directories:
    - Add the path to the newly built include folder (it's usually `path/to/your/server/source/enet/include`) under Include Directories.
    - Add the path to the newly built lib folder (e.g., `path/to/your/server/source/enet/build/Release` or `path/to/your/server/source/enet/build/Debug`) under Library Directories.
  - Linker > Input:
    - Add **enet.lib** to the top of the Additional Dependencies list.

## Configuration

- Enable the New Packet System
  - In your server source code, search for:
    ```cpp
    server->checksum = enet_crc32;
    ```

    Add the following line above it:
    ```cpp
    server->usingNewPacketForServer = 1; // Enables new packet system for Growtopia 5.15+
    ```

- Update server_data.php
  - Add the following line to your server_data.php:
    > type2|1

## Usage Example

```cpp
#include <enet/enet.h>

// ... your server setup code ...

server->usingNewPacketForServer = 1; // Enable new packet system
server->checksum = enet_crc32;
```

## Troubleshooting

- Error: "Error connection" when connecting with Growtopia 5.15+
   Solution: Ensure usingNewPacketForServer is set to 1 before setting the checksum.
- Linker Error: enet.lib not found
   Solution: Make sure the path to the built lib folder (e.g., enet/build/Release) is correctly set in your project properties, and enet.lib is at the top of the dependencies list. Also, confirm that enet.lib was successfully generated by CMake.
- CMake Errors: "CMake not found" or issues generating build files.
   Solution: Ensure CMake is correctly installed and added to your system's PATH. Double-check the CMake generator name for your Visual Studio version.
- Other Issues:
  - Clean and rebuild your entire project after making changes.
  - Verify that the CMakeLists.txt file from this repository is present in your enet folder.

## Credits

Special thanks to:
- [lsalzman](https://github.com/lsalzman)
- [ZTzTopia](https://github.com/ZTzTopia)
