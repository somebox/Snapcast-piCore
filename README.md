## Installation Instructions

Download the install script to a fresh piCore Installation
```
$ wget https://github.com/bjwelker/Snapcast-piCore/raw/master/install_snapclient.sh
```
Make the script executable
```
$ chmod +x install_snapclient.sh
```

### Expanding the SD Card (if needed)

**IMPORTANT:** The SD card partition needs to be expanded before installation if you're using a fresh piCore image.

**Recommended Method - Using PiCorePlayer Web Interface:**
1. Access the PiCorePlayer web interface at http://[your-pi-ip]:80
2. Go to the "Main" tab
3. Look for the "Resize FS" button and click it
4. The system will expand the filesystem and reboot automatically

**Alternative Method - Manual Expansion (Advanced Users):**

If the web interface method is not available, you can manually expand the partition. **WARNING:** This should only be done by experienced users as incorrect commands can corrupt your SD card.

1. First, backup your data if possible
2. Use `parted` to resize the partition safely:
```bash
# Identify your partition layout
sudo parted /dev/mmcblk0 print

# Resize partition 2 to use all available space
# Replace X with your partition number (usually 2)
sudo parted /dev/mmcblk0 resizepart 2 100%

# Reboot to apply changes
sudo reboot
```

3. After reboot, expand the filesystem:
```bash
sudo resize2fs /dev/mmcblk0p2
```

### Install Snapclient

Run the installation script:
``` 
$ ./install_snapclient.sh
```

After reboot snapclient should play :)

## Audio Output Configuration

To switch between HDMI and analog output use:

HDMI:
```
$ amixer cset numid=3 2
```
Analog:
```
$ amixer cset numid=3 1
```
or just connect to the Webinterface on http://SnapCast-Client-IP