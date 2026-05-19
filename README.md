# Parking Space Detection Using Raspberry Pi and CircuitDigest Cloud

Finding a parking space in crowded places like malls or theme parks can be frustrating. This project implements a smart parking space detection system that monitors a parking area and automatically detects how many spaces are vacant (empty) and how many are occupied (filled). By leveraging a Raspberry Pi, a USB camera, and the CircuitDigest Cloud Parking Space Detection API, this solution avoids complex local model training, datasets, or labeling.

## Features
- **Real-Time Detection:** Automatically identifies filled and vacant slots using cloud-based computer vision.
- **Multiple Operating Modes:**
  - **Keyboard Mode:** Capture images manually by pressing the `SPACE` key.
  - **Auto Mode:** Automatically captures images at a fixed time interval (e.g., every 5 seconds).
  - **SSH Mode:** Runs completely headless from the terminal without an OpenCV display window.
- **No Local Model Training:** Relies on a pre-trained API in the CircuitDigest Cloud.
- **Easy Deployment:** Simplifies parking management and reduces traffic congestion with basic hardware.

## Hardware Requirements
- **Raspberry Pi** (Pi 3, Pi 4, or newer, connected to external power)
- **USB Web Camera** (Positioned at a top-view angle for best results)
- **Laptop/PC** (For initial setup and output monitoring)
- MicroSD Card (with Raspberry Pi OS installed)

## Hardware Setup
1. Mount the USB Camera in a stable, top-view position overlooking the parking slots.
2. Connect the USB Camera to one of the USB ports on the Raspberry Pi.
3. Ensure the Raspberry Pi is powered by a sufficient external power supply.

## Software Setup
1. Setup your Raspberry Pi using the **Raspberry Pi Imager** with a standard OS installation.
2. Create an account on the [CircuitDigest Cloud](https://www.circuitdigest.cloud/).
3. Navigate to the **Parking Space Detection** feature and copy your **API Key**.
4. Open **Thonny IDE** on your Raspberry Pi.
5. Install the necessary Python packages:
   ```bash
   pip install opencv-python requests
   ```

## Installation & Usage
1. Clone this repository or copy the Python script to your Raspberry Pi.
2. Edit the script to configure your parameters:
   ```python
   SERVER_URL = "https://www.circuitdigest.cloud/api/v1/parking-detection/detect"
   API_KEY    = "YourApikey"  # <-- Paste your CircuitDigest API Key here
   MODE = "keyboard"          # <-- Set to "keyboard", "auto", or "ssh"
   AUTO_INTERVAL = 5          # <-- Interval in seconds for auto mode
   ```
3. Run the script:
   ```bash
   python parking_detection.py
   ```
4. Depending on the mode selected, the system will capture images of the parking lot, upload them to the CircuitDigest Cloud API, and display the counts of occupied and empty slots in the terminal.

## Troubleshooting
- **Camera not found! Check USB camera connection:** 
  Verify the USB cable connection. You may need to change `cv2.VideoCapture(0)` to `cv2.VideoCapture(1)` if multiple video devices are detected.
- **API request timeout:** 
  Check that the Raspberry Pi has a stable Wi-Fi or Ethernet connection. Try increasing the timeout value in the script.
- **Invalid API key error:** 
  Double-check your API key from the CircuitDigest Cloud panel and ensure there are no trailing spaces.
- **Incorrect parking detection counts:** 
  Ensure the camera is mounted with a clear top-down view and there is good lighting. Avoid heavy shadows or angles where vehicles obstruct the view of other slots.
- **Program crashes during execution:** 
  Confirm that `opencv-python` and `requests` are installed correctly. Restart the script or the Raspberry Pi if necessary.

## Advantages & Limitations
| Advantages | Limitations |
| :--- | :--- |
| Automatically detects occupied and empty slots in real time | Requires a stable internet connection for cloud processing |
| Reduces manual inspection work for guards or supervisors | Accuracy depends on camera placement and quality |
| Easy to set up with standard hardware and a USB camera | Dark conditions or heavy shadows can affect results |
| Supports both manual (keyboard) and automatic capture | Cloud API usage limits may apply based on subscription plan |
| Improves parking management efficiency | Slight network latency depending on internet speed |

## Relevant Links
- [CircuitDigest Cloud Platform](https://www.circuitdigest.cloud/)
- [Raspberry Pi based Parking Space Detection GitHub Repo](https://github.com/Circuit-Digest/Raspberry-Based-Parking-Space-Detection)
