# ZeroTab

A lightweight Windows utility application that provides rapid application termination functionality via a global hotkey. ZeroTab is designed to help users quickly close all running user applications while preserving critical system processes.

## Overview

ZeroTab is a C++ Windows application that monitors for a global hotkey combination and terminates all user-level applications. The application includes intelligent process filtering to ensure that essential Windows system processes remain protected and operational.

## Features

- **Global Hotkey Support**: Uses Ctrl + Alt + Z hotkey combination for instant application closure
- **Safe Process Termination**: Protects core Windows system processes from being terminated
- **System Process Whitelist**: Maintains a safelist of critical processes including:
  - system, wininit.exe, winlogon.exe, csrss.exe
  - services.exe, svchost.exe, lsass.exe, smss.exe
  - dwm.exe, fontdrvhost.exe
- **Administrator Privileges**: Requires administrator rights for full functionality
- **Minimal Resource Footprint**: Lightweight implementation with minimal system overhead

## Project Structure

```
ZeroTab/
├── ZeroTab.sln              # Visual Studio Solution file
├── ZeroTab/
│   └── ZeroTab.cpp          # Main application source code
└── .gitignore               # Git ignore configuration
```

## Requirements

- **Platform**: Windows OS (Windows Vista or later)
- **Build Tools**: Microsoft Visual C++ compiler
- **Privileges**: Administrator rights required for hotkey registration and process termination
- **Framework**: Windows API (Windows.h, TlHelp32.h)

## Building

### Prerequisites
- Visual Studio 2015 or later (or compatible C++ compiler)
- Windows SDK

### Build Instructions

1. Open `ZeroTab.sln` in Visual Studio
2. Build the solution (Debug or Release configuration)
3. The compiled executable will be available in the build output directory

## Installation

1. Build the project using the instructions above
2. Run the compiled executable with administrator privileges
3. Upon successful execution, the hotkey will be registered and active
4. A notification will appear if hotkey registration fails

## Usage

### Activating the Hotkey
- **Press**: `Ctrl + Alt + Z`
- **Result**: All non-system user applications will be terminated
- **System Protection**: Critical Windows processes will remain untouched

### Running the Application

```bash
ZeroTab.exe
```

The application must be run as Administrator for the hotkey to register successfully.

## How It Works

1. **Initialization**: The application registers a global hotkey (Ctrl + Alt + Z)
2. **Process Monitoring**: Enters a message loop waiting for hotkey activation
3. **Safe Termination**: When triggered, the application:
   - Snapshots all running processes
   - Filters out protected system processes
   - Gracefully terminates user applications
4. **Cleanup**: Closes handles and maintains system stability

## Implementation Details

### Core Components

- **System Process List**: A whitelist of protected Windows processes that must not be terminated
- **Process Enumeration**: Uses Windows ToolHelp API to list all running processes
- **Hotkey Registration**: Windows API hotkey management for global keyboard shortcuts
- **Process Termination**: Safe termination of selected processes with error handling

### Key Functions

- `toLower()`: Case-insensitive string comparison
- `isSystemProcess()`: Validates if a process should be protected
- `closeAllUserApps()`: Main termination logic that closes all non-system applications
- `WinMain()`: Entry point and message loop

## Safety & Precautions

⚠️ **Important**: 
- This application terminates processes forcefully. Unsaved data in running applications may be lost.
- Use with caution and ensure all important work is saved before triggering the hotkey.
- Administrator privileges are required for operation.
- The application includes safeguards to protect critical Windows processes from termination.

## Contributing

For bug reports, feature requests, or contributions, please visit the original repository at:
- Upstream: [Lochangarg/ZeroTab](https://github.com/Lochangarg/ZeroTab)

## License

This project does not currently specify a license. Please check the upstream repository for licensing information.

## Author

- **Original Author**: Lochangarg
- **Repository**: [Lochangarg/ZeroTab](https://github.com/Lochangarg/ZeroTab)

## Disclaimer

This is a fork of the original ZeroTab project. Use at your own risk. The author and contributors are not responsible for any data loss or system damage caused by this application. Always ensure you have backups and saved all important work before using this tool.