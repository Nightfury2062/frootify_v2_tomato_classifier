# 🍅 Frootify V2

Frootify V2 is an AI-powered tomato quality monitoring system designed for Raspberry Pi 4. It uses a YOLOv8 ONNX model to detect fresh and rotten tomatoes in real time, monitors environmental conditions using a DHT sensor, controls warning LEDs through GPIO, and uploads monitoring data to ThingSpeak for remote visualization.

## Features

* Real-time tomato detection using a YOLOv8 ONNX model
* Detects **Fresh** and **Rotten** tomatoes
* Environmental monitoring (Temperature & Humidity)
* LED indicators for rotten tomatoes and environmental warnings
* Automatic rotten tomato counting
* Daily rotten count reset at midnight
* Uploads data to ThingSpeak every 60 seconds
* Works in simulation mode when Raspberry Pi hardware is unavailable
* Logging for system events and detections

---

## Project Structure

```text
frootify_v2/
│
├── app.py                  # Main application
├── detector.py             # YOLO ONNX inference
├── gpio_manager.py         # GPIO LED control
├── env_sensor.py           # DHT temperature & humidity sensor
├── thingspeak_client.py    # ThingSpeak cloud uploader
├── test_detector.py        # Detector testing utility
├── requirements.txt
├── models/
│   └── best.onnx
└── logs/
```

---

## Hardware Requirements

* Raspberry Pi 4
* USB Webcam
* DHT11 or DHT22 Sensor
* Red LED (Rotten Warning)
* Yellow/Green LED (Environment Warning)
* 330 Ω resistors
* Breadboard and jumper wires

---

## Software Requirements

* Python 3.9+
* ONNX Runtime
* OpenCV
* RPi.GPIO
* Adafruit CircuitPython DHT library

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Place your trained ONNX model inside:

```text
models/best.onnx
```

Start the application:

```bash
python app.py
```

Stop the application using:

* **Ctrl + C**
* Press **Q** on the display window

---

## Testing the Detector

Test using the webcam:

```bash
python test_detector.py
```

Test using an image:

```bash
python test_detector.py --image path/to/image.jpg
```

An annotated output image will be saved as:

```text
test_output.jpg
```

---

## ThingSpeak Setup

1. Create a ThingSpeak account.
2. Create a new channel.
3. Configure four fields:

   * Daily Rotten Count
   * Temperature
   * Humidity
   * Total Rotten Count
4. Copy the **Write API Key** and **Channel ID**.
5. Update `thingspeak_client.py` with your credentials.

---

## LED Indicators

| LED          | Status                                    |
| ------------ | ----------------------------------------- |
| Red          | Rotten tomato detected                    |
| Yellow/Green | Temperature or humidity exceeds threshold |

---

## Environmental Thresholds

* Temperature > **30°C**
* Humidity > **80%**

When either threshold is exceeded, the environmental warning LED is activated.

---

## Logs

Application logs are automatically stored in the `logs/` directory with timestamped filenames.

---

## Notes

* The project supports simulation mode if Raspberry Pi GPIO or DHT hardware is not available.
* Rotten tomatoes are counted only when a new detection event is confirmed, preventing duplicate counting.
* Environmental readings are cached and updated periodically to reduce unnecessary sensor access.

---

## Future Improvements

* Dashboard for historical analytics
* Email or SMS alerts
* Support for additional fruit types
* Database integration
* Web-based monitoring interface
* MQTT/IoT integration

