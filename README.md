# Run-Wivrn

`run-wivrn` is a Bash script that ensures the WiVRn application is running on your Linux system. It checks if the `avahi-daemon` is active and starts it if necessary. Then, it looks for the WiVRn dashboard process and launches the application if it's not already running.

## Description

This script is designed to simplify the management of the WiVRn application, which is useful for enhancing the virtual reality gaming experience on Linux. It automates the checking and launching of the application, ensuring you can focus on your gameplay without manual setup.

## Requirements

- **Linux Environment**: Tested on various Linux distributions.
- **Flatpak**: Ensure that WiVRn is installed via Flatpak.
- **Avahi-daemon**: This script checks for and manages the avahi-daemon service.

## Installation

1. **Install Flatpak** (if not already installed):
   ```bash
   sudo apt install flatpak
   ```

2. **Install WiVRn**:
   Follow the instructions on the [WiVRn GitHub page] to install the application via Flatpak.

3. **Create the Script File**:
   Create a new file for the script:
   ```bash
   nano ~/Desktop/run-wivrn.sh
   ```

4. **Copy the Script**:
   Paste the following code into the file:

   ```bash
   #!/usr/bin/env bash
   set -euo pipefail

   # Ensure avahi-daemon is running/enabled
   systemctl is-active --quiet avahi-daemon || { systemctl enable --now avahi-daemon; }

   # Check for WiVRn running (case-insensitive search for "wivrn" and "dashboard") and start if not present
   ps aux | grep -i wivrn | grep -i dashboard >/dev/null 2>&1 || nohup flatpak run io.github.wivrn.wivrn >/dev/null 2>&1 &
   ```

5. **Make the Script Executable**:
   Run the following command:
   ```bash
   chmod +x ~/Desktop/run-wivrn.sh
   ```

## Usage

To run the script along with `steamkill`, use the following command in your terminal:

```bash
/home/a/Desktop/run-wivrn.sh && sudo /home/a/Desktop/steamkill.sh
```

This command will start the WiVRn application and then execute the SteamKill script.

## Acknowledgments

- Thanks to **xytovl** for creating **WiVRn**, an excellent open-source project for enhancing Linux gaming.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.


Feel free to adjust any additional sections or details. Once you're satisfied, you can create or update the `README.md` file in your GitHub repository with this content. Let me know if there's anything else you need!
