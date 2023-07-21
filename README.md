# Uni-Sync
### A Synchronization Tool for Lian Li Fan Controllers

This tool allows you to configure the synchronization settings for Uni Fan controllers on any OS. No more booting into Windows to enable PWM or LED synchronization. 
- Enable/Disable Motherboard PWM Sync
- Enable/Disable LED ARGB Header Sync
- Manually Set Fan Speeds

[![Support](https://img.shields.io/badge/Support-Buy_Me_A_Coffee-yellow?style=for-the-badge&logo=buy%20me%20a%20coffee&color=FFDD00)](https://www.buymeacoffee.com/CameronHalter)


## Device Support

| Device                          | PID          | Status                          | Set Fan RPM | Set PWM Sync | Set ARGB Sync |
| ------------------------------- | ------------ | ------------------------------- | ------------ | ----------- | ----------- |
| LianLi-UNI SL                   | `7750, a100` | Supported                       | ✔️           | ✔️         | ✔️         |
| LianLi-UNI AL                   | `a101`       | Untested                        | ❓          | ❓         | ❓         |
| LianLi-UNI SL-Infinity          | `a102`       | Untested                        | ❓          | ❓         | ❓         |
| LianLi-UNI SL v2                | `a103, a105` | Untested                        | ❓          | ❓         | ❓         |
| LianLi-UNI AL v2                | `a104`       | Untested                        | ❓          | ❓         | ❓         |


## Installation

Uni-Sync requires [Rust](https://www.rust-lang.org/learn/get-started) to build. Please install before proceeding.

### a. Windows

Run install.bat. This will build the application and move it into ```%APPDATA%\Local\uni-sync```. Added to startup.

### b. Linux

Run install.sh. Please note, this will set up a service named uni-sync and will execute once on system startup.

## Configuration

Uni-Sync will generate a uni-sync.json configuration file in the same directory as the execuatable. For Windows, that is ```%APPDATA%\Local\uni-sync\uni-sync.json```. For Linux, it is ```/usr/sbin/uni-sync.json```.

This file will contain an autogenerated configuration profile for each controller attached to the system:

```json
{
  "configs": [
    {
      "device_id": "VID:3314/PID:41216/SN:624314930",
      "sync_rgb": false,
      "channels": [
        // Channel 1
        {
          "method": "Manual",
          "speed": 50
        },
        // Channel 2
        {
          "method": "Manual",
          "speed": 50
        },
        // Channel 3
        {
          "method": "Manual",
          "speed": 50
        },
        // Channel 4
        {
          "method": "PWM",
          "speed": 50
        }
      ]
    }
  ]
}
```

The following options can be configured: 

| Configuration                   | Description                                          | Type         | Options     |
| ------------------------------- | ---------------------------------------------------- | ------------ | ----------- |
| ``` "sync_rgb": false ```       | Enable/Disables ARGB header sync                     | bool         | **true** or **false** |
| ``` "method": "Manual" ```      | **PWM** to enable PWM sync. **Manual** to set speed. | string       | **PWM** or **Manual** |
| ``` "speed": 50 ```             | Fan speed as percentage (1-100)                      | int          | 1-100 |

## Removal

This will delete the uni-sync.json file.

### a. Windows

Run uninstall.bat

### b. Linux

Run uninstall.sh