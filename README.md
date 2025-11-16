# SnapEyeMech: Zero-Fastener Animatronic Eye Mechanism

A fully 3D-printed animatronic eye system with computer vision tracking, designed for educational robotics. No screws, glue, or fasteners required - everything snaps together!

![SnapEyeMech Assembly](images/assembly.jpg)

## Overview

SnapEyeMech is a low-cost binocular animatronic eye mechanism that uses snap-fit joints for tool-free assembly. The system integrates real-time face tracking using OpenCV and can be built in under 10 minutes once parts are printed.

**Key Features:**
- 🔧 Zero fasteners - completely snap-fit assembly
- 💰 Low cost - approximately ₹1700 in components
- ⚡ Fast assembly - 8-10 minutes average build time
- 👁️ Dual-axis movement - ±40° horizontal, ±35° vertical per eye
- 🎥 Real-time face tracking with OpenCV
- 🤖 Arduino + Raspberry Pi architecture
- 📖 Open source hardware and software

## Project Details

**Authors:** Mohd. Umar Farhan, Harsh Kumar, Mohit Kumar  
**Institution:** KIET Group of Institutions, Ghaziabad  
**Supervisor:** Ms. Ragini Sharma  
**Project Code:** BEC-753, Session 2025-26

## Hardware Requirements

### Electronics
- 4× TowerPro SG90 Micro Servos (~₹400)
- 1× Arduino Mega 2560 (~₹600)
- 1× Raspberry Pi 4 (4GB) (~₹3500)
- 1× USB Webcam 640×480 (~₹300)
- 1× Joystick Module (~₹100)
- 1× 5V 2A Power Supply (~₹100)
- Jumper wires and breadboard (~₹150)

### 3D Printing
- PLA Filament: ~50g per complete assembly (~₹50)
- Printer: Any FDM printer (tested on Creality Ender-3)
- Print time: 12-14 hours total for one binocular mechanism

**Total Cost: ₹1700** (excluding Raspberry Pi if already available)

## Repository Structure

```
SnapEyeMech/
├── hardware/
│   ├── CAD_files/          # Fusion 360 .f3d files
│   ├── STL_files/          # Ready-to-print STL files
│   │   ├── eyeball_left.stl
│   │   ├── eyeball_right.stl
│   │   ├── orbital_frame.stl
│   │   ├── servo_mount_x4.stl
│   │   └── linkages.stl
│   └── PCB/                # Optional EyeBoard PCB files
│       ├── schematic.pdf
│       ├── gerber_files/
│       └── BOM.csv
├── software/
│   ├── arduino/
│   │   └── eye_controller/
│   │       └── eye_controller.ino
│   └── raspberry_pi/
│       ├── face_tracker.py
│       ├── kalman_filter.py
│       └── requirements.txt
├── docs/
│   ├── assembly_guide.pdf
│   ├── calibration_guide.md
│   ├── research_paper.pdf
│   └── images/
├── examples/
│   ├── basic_movement.ino
│   ├── joystick_control.ino
│   └── tracking_demo.py
└── README.md
```

## Quick Start Guide

### 1. Print the Parts

Print settings (PLA):
- Layer height: 0.2mm
- Infill: 20% gyroid
- Supports: None required
- Orientation: Parts are pre-oriented

Print all STL files from `hardware/STL_files/`

### 2. Assemble the Mechanism

**Assembly takes 8-10 minutes:**

1. Snap servo mounts into orbital frame (firm pressure, no tools)
2. Insert SG90 servos into mounts
3. Attach servo horns to linkages (use tiny screws that come with servos)
4. Snap linkages into eyeball sockets
5. Position eyeballs in orbital frame

See `docs/assembly_guide.pdf` for detailed photos.

### 3. Wire the Electronics

**Servo Connections to Arduino:**
- Left Eye Horizontal → Pin 9
- Left Eye Vertical → Pin 10
- Right Eye Horizontal → Pin 11
- Right Eye Vertical → Pin 12
- All servos: 5V and GND

**Joystick (optional for testing):**
- X-axis → A0
- Y-axis → A1

**Raspberry Pi:**
- USB connection to Arduino (serial communication)

### 4. Upload Arduino Code

```bash
cd software/arduino/eye_controller
# Open eye_controller.ino in Arduino IDE
# Select Board: Arduino Mega 2560
# Upload
```

### 5. Run Vision Tracking (Raspberry Pi)

```bash
cd software/raspberry_pi
pip install -r requirements.txt
python face_tracker.py
```

## Usage Examples

### Basic Movement Test
```cpp
// Arduino - Move eyes to center
servoLeftH.write(90);
servoLeftV.write(90);
servoRightH.write(90);
servoRightV.write(90);
```

### Joystick Control
Upload `examples/joystick_control.ino` for manual control during demos.

### Face Tracking
The face tracker runs automatically:
- Detects faces using Haar cascades
- Applies Kalman filtering for smooth motion
- Sends position commands via serial at 20Hz
- Eyes follow the largest detected face

## Calibration

Each servo may have slightly different center positions. To calibrate:

1. Upload the calibration sketch
2. Adjust center position values for each servo
3. Note down the values
4. Update in main code

See `docs/calibration_guide.md` for details.

## Performance Specifications

| Metric | Value |
|--------|-------|
| Assembly Time | 8-10 minutes |
| Movement Range (H/V) | ±40° / ±35° |
| Repeatability | ±1-2° |
| Tracking Latency | 100-130ms |
| Face Detection Range | 0.5m - 2m |
| Power Consumption | ~1.5A @ 5V peak |
| Durability | 500+ cycles tested |

## Troubleshooting

### Parts don't snap together
- Check print quality - may have stringing or warping
- Verify correct orientation during printing
- Try cleaning mating surfaces with fine sandpaper

### Servos jittering
- Add decoupling capacitors (100μF) near servos
- Check power supply can provide 2A
- Reduce Kalman filter Q value for more damping

### Face detection fails
- Ensure adequate lighting (>200 lux)
- Check camera is properly connected
- Verify OpenCV Haar cascade file path

### Eyes don't center properly
- Run calibration procedure
- Check for mechanical binding
- Verify servo horn attachment

## Design Modifications

Want to customize the design? The Fusion 360 files include:
- Parametric models (easy to resize)
- Assembly relationships
- Simulation setups

Common modifications:
- **Larger/smaller eyes**: Edit eyeball diameter parameter
- **Increased range**: Modify linkage lengths
- **Add eyelids**: PCB includes 2 extra servo headers
- **Different servos**: Adjust mount hole spacing

## Contributing

We welcome contributions! Areas for improvement:
- Better low-light tracking algorithms
- Emotion recognition integration
- Multi-eye synchronization for robot swarms
- Alternative materials testing (PETG, TPU)
- Power optimization

Please submit pull requests or open issues for bugs.

## Research Paper

Full technical details are available in our research paper:
> Farhan, M.U., Kumar, H., Kumar, M., Sharma, R. (2025). "Design and Control of a Zero-Fastener Animatronic Eye Mechanism with Computer Vision for Low-Cost Humanoid Robotics." B.Tech Project BEC-753, KIET Group of Institutions.

[Read the paper](docs/research_paper.pdf)

## License

This project is open source hardware and software:
- **Hardware**: [CERN Open Hardware License v2 - Permissive](LICENSE_HARDWARE)
- **Software**: [MIT License](LICENSE_SOFTWARE)

Feel free to use, modify, and distribute for educational and non-commercial purposes.

## Acknowledgments

- Ms. Ragini Sharma for project supervision and guidance
- KIET Group of Institutions for lab facilities and 3D printers
- Will Cogley for the EyeMech project that inspired aspects of this design
- OpenCV community for computer vision libraries

## Citation

If you use this project in your research or education, please cite:

```bibtex
@misc{snapeyemech2025,
  author = {Farhan, Mohd. Umar and Kumar, Harsh and Kumar, Mohit},
  title = {SnapEyeMech: Zero-Fastener Animatronic Eye Mechanism},
  year = {2025},
  publisher = {GitHub},
  url = {https://github.com/farhan-umar/SnapEyeMech}
}
```

## Contact

- **Mohd. Umar Farhan**: mohd.2226ec1004@kiet.edu
- **Harsh Kumar**: harsh.2226ec1045@kiet.edu  
- **Mohit Kumar**: mohit.2226ec1019@kiet.edu

For questions, suggestions, or collaboration opportunities, please open an issue or contact us via email.

**Status:** Active Development | **Version:** 1.0 | **Last Updated:** November 2025

⭐ Star this repo if you find it useful! ⭐
