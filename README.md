# TridentExtruder: A Bio 3D Printer Extruder with Peltier Module Based on Klipper

TridentExtruder is a bio 3D printer extruder designed to extend the functionality of Klipper firmware. One of its key features is the integration of a Peltier module for efficient cooling of the printer head. This project modifies Klipper’s open-source code, replacing the `watermark` cooling algorithm in the `klipper/extras/heaters.py` file with a PID-based cooling algorithm.

## Features

- Supports Peltier module control for efficient cooling of the printer head.
- Replaces Klipper's default `watermark` cooling control with a PID-based algorithm.
- Tailored for bio 3D printing applications requiring precise temperature management.
- Requires minimal configuration changes to implement cooling functionality.

## How to Use

### 1. Download and Replace Code

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/Shirayukihiyou/TridentExtuder.git
   ```
2. Replace the `heaters.py` file in the Klipper source code:
   - File path: `klipper/extras/heaters.py`
   - Backup the original file before replacing it.

   ```bash
   cp /path/to/klipper/extras/heaters.py /path/to/backup/heaters.py.bak
   cp klipper-cooling-mod/heaters.py /path/to/klipper/extras/heaters.py
   ```

### 2. Modify Configuration File

Update the `printer.cfg` file to set the `[extruder]` `control` parameter to `watermark`. Example:

```ini
[extruder]
control: watermark
...
```

### 3. Restart Klipper Service

Restart the Klipper service to apply the changes:

```bash
sudo service klipper restart
```

## Notes

- Always backup the original files before making any modifications.
- If issues arise after the changes, check the log files or report them on the Issues page of this repository.
- Ensure the printer head hardware supports Peltier cooling and is properly connected.

## Background

Klipper is a powerful 3D printer firmware. However, the default `watermark` cooling algorithm may not suit specific cooling needs. TridentExtruder enhances Klipper’s functionality by improving cooling control, making it suitable for bio 3D printing and other specialized applications.

## Contributions

Feel free to submit Issues or Pull Requests to suggest improvements or contribute code to this project.

## License

This project follows Klipper’s open-source license, maintaining consistency with the original project.

