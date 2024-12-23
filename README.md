# TridentExtruder: A Bio 3D Printer Extruder with Peltier Module Based on Klipper

TridentExtruder is a bio 3D printer extruder designed to extend the functionality of Klipper firmware. One of its key features is the integration of a Peltier module for efficient cooling of the printer head. This project modifies Klipper’s open-source code, adapting the PID and `watermark` algorithms in the `klippy/extras/heaters.py` file to support cooling functionality, which they originally did not provide.

## Features

- Supports Peltier module control for efficient cooling of the printer head.
- Extends Klipper's PID and `watermark` algorithms to enable cooling functionality, improving cooling efficiency and precision.
- Allows simultaneous heating and cooling for different targets (e.g., heating the bed and cooling the print head).
- Tailored for bio 3D printing applications requiring precise temperature management.
- Requires minimal configuration changes to implement cooling functionality.

## How to Use

### 1. Download and Replace Code

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/Shirayukihiyou/TridentExtuder.git
   ```
2. Replace the `heaters.py` file in the Klipper source code:
   - File path: `klippy/extras/heaters.py`
   - Backup the original file before replacing it.

   ```bash
   cp ~/klipper/klippy/extras/heaters.py ~/klipper/klippy/extras/heaters.py.bak
   cp TridentExtuder/extras/heaters.py ~/klipper/klippy/extras/heaters.py
   ```

3. Replace the `pid_calibrate.py` file in the Klipper source code:
   - File path: `klippy/extras/pid_calibrate.py`
   - Backup the original file before replacing it.

   ```bash
   cp ~/klipper/klippy/extras/pid_calibrate.py ~/klipper/klippy/extras/pid_calibrate.py.bak
   cp TridentExtuder/extras/pid_calibrate.py ~/klipper/klippy/extras/pid_calibrate.py
   ```

4. Perform PID calibration for cooling:
   - Restart the Klipper server and run the following command in your terminal:

   ```bash
   PID_CALIBRATE HEATER=extruder TARGET=4
   ```

   - Once calibration is complete, restore the original `pid_calibrate.py` file:

   ```bash
   cp ~/klipper/klippy/extras/pid_calibrate.py.bak ~/klipper/klippy/extras/pid_calibrate.py
   ```

### 2. Modify Configuration File

Update the `printer.cfg` file to set the `[extruder]` `control` parameter. Use `watermark` for cooling and `pid` for heating. Example:

```ini
[extruder]
control: watermark  # For cooling
...

[heater_bed]
control: pid  # For heating
...
```

### 3. Restart Klipper Service

Restart the Klipper service to apply the changes:

```bash
sudo service klipper restart
```

## Notes

- Always backup the original files before making any modifications.
- The original `watermark` algorithm has been adapted for cooling and is no longer available in its original form.
- If issues arise after the changes, check the log files or report them on the Issues page of this repository.
- Ensure the printer head hardware supports Peltier cooling and is properly connected.

## Background

Klipper is a powerful 3D printer firmware. However, neither the default PID nor the `watermark` algorithms supported cooling functionality. TridentExtruder adapts these algorithms to enable precise cooling control, making it suitable for bio 3D printing and other specialized applications.

## Contributions

Feel free to submit Issues or Pull Requests to suggest improvements or contribute code to this project.

## License

This project follows Klipper’s open-source license, maintaining consistency with the original project.

