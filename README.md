# Agrosense Node 🌾

**Agrosense Node** is a firmware implementation for a Smart Irrigation System, designed to run on FreeRTOS-enabled microcontrollers (e.g., ESP32). It simulates a resource-constrained IoT environment where sensor data collection and network communication must coexist efficiently.

The project demonstrates advanced embedded systems concepts including real-time task scheduling, dynamic memory management with quotas, and continuous system health monitoring.

## 🚀 Key Features

-   **Real-Time Multitasking**: Leverages FreeRTOS to handle concurrent operations:
    -   `SensorTask`: Simulates periodic data acquisition from soil/environmental sensors.
    -   `CommTask`: Simulates data packet preparation and transmission to a gateway/cloud.
-   **Smart Memory Management**:
    -   **Quota Enforcement**: Custom `pvPortMallocWithQuota` allocator prevents any single task from hogging system memory.
    -   **Leak Detection**: Tracks allocated vs. freed memory per task.
    -   **Thread Safety**: Uses Mutexes (`SemaphoreHandle_t`) to protect shared memory tracking structures.
-   **System Health Monitoring**:
    -   **Heap Monitor**: Continuously tracks free heap size and reports minimum ever free heap to detect potential fragmentation or leaks.
    -   **Stack Monitor**: Uses `uxTaskGetStackHighWaterMark` to warn about potential stack overflows for every active task.

## 🛠️ Technical Architecture

The system is built using **C++** and **FreeRTOS** within the Arduino framework.

| Component | Description |
| :--- | :--- |
| **SensorTask** | Allocates memory to simulate reading sensors, processes data, and frees memory. |
| **CommTask** | Simulates varying network packet sizes and transmission delays. |
| **HeapMonitor** | Diagnostic task that prints global heap statistics. |
| **StackMonitor** | Diagnostic task that checks stack usage for `SensorTask` and `CommTask`. |

## 📦 Getting Started

### Prerequisites
-   **Hardware**: ESP32 or any Arduino-compatible board with FreeRTOS support.
-   **Software**:
    -   [VS Code](https://code.visualstudio.com/) with [PlatformIO](https://platformio.org/) (Recommended)
    -   OR [Arduino IDE](https://www.arduino.cc/en/software)

### Installation

1.  **Clone the Repository**:
    ```bash
    git clone https://github.com/Kanishkhan/Agrosense-node.git
    ```
2.  **Open the Project**:
    -   **PlatformIO**: Open the folder as a project.
    -   **Arduino IDE**: Open `AgroSense.cpp` (you may need to rename it to `.ino` or place it in a matching folder structure depending on your setup).
3.  **Upload**: Connect your board and upload the firmware.
4.  **Monitor**: Open the Serial Monitor at **115200 baud** to see the logs.

## 📊 Example Output

```text
🌾 Smart Irrigation Node Starting...
[SensorTask] 🌱 Allocating 512 bytes...
[SensorTask] ✅ Allocated | Usage: 512 / 2048
[CommTask] 📡 Allocating 1024 bytes...
[HeapMonitor] 📉 Free Heap: 210452 bytes | Min Ever: 210400 bytes
[StackMonitor] 🧠 Stack - Sensor: 1024 | Comm: 1024 | HeapMon: 1024 (words)
[CommTask] 🧹 Freed memory.
```

## 🤝 Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or bug fixes.

## 👤 Author

**Kanishk Khan**
-   GitHub: [@Kanishkhan](https://github.com/Kanishkhan)

---
*Built for educational purposes to demonstrate OS concepts in Embedded Systems.*
