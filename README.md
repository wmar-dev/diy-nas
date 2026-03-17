
# Bootable USB Stick

1. Find or purchase a USB stick that has a 4 GB or greater capacity.
2. Download TrueNAS Community Edition iso.
3. Stick USB into Linux computer and identify where the device is located (/dev/sdc).
4. Copy iso to usb drive using `dd`.

`sudo dd status=progress if=TrueNAS-SCALE-25.10.2.1.iso of=/dev/sdc`
