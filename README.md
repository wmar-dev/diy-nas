## Components

- Jonsbo N3
- CWWK NAS-N150-8P CW-AT-10G-8P-N150
- Corsair SF750
- Crucial 8 GB RAM
- Crucial 1 TB NVMe

The build of the NAS should be around the number of drive bays and how you want the ZFS pool setup. For my case, I wanted 8 drive bays and to do mirrored vdevs and keep adding pairs as I expand. Mirrored vdevs, because it takes too long to rebuild if you are using RAID-Z1 or RAID-Z2.

I wanted to keep a small form factor, so that led to choosing an ITX case. The NAS-N150-8P has been popular, so I opted for the N150 version since it was the only thing in stock. I don't plan on heavy VM usage. If I am going to do VMs, I could build another machine for that. 

I wanted to max out the RAM, but I waited too long and RAM prices shot up and went out of stocks. Eventually got my hands on 8 gigabytes of Crucial RAM and SSD. I chose Crucial, because I was worried about compatibility issues.

Normally I buy Seasonic, but I couldn't find a SFX form factor, so I went with Corsair, which is 80 PLUS® Platinum Certified High Performance. High efficiency means less fan noise.

## Bootable USB Stick

1. Find or purchase a USB stick that has a 4 GB or greater capacity.
2. [Download TrueNAS Community Edition](https://www.truenas.com/download/) iso.
3. Stick USB into Linux computer and identify where the device is located (/dev/sdc).
4. Copy iso to usb drive using `dd`.

`sudo dd status=progress if=TrueNAS-SCALE-25.10.2.1.iso of=/dev/sdc`

## Assembly

1. Remove 4 screws to remove top of Jonsbo N3 case using supplied hex key.
2. Remove 2 thumbscrews to remove bottom fan panel.
3. Remove 4 screws with PH1 head to remove PSU bracket.
4. Attach PSU to bracket with 6 supplied screws with PSU
5. Reattach the PSU bracket with the 4 screws from before.
6. Push in the power connector into the PSU.

*Motherboard*

![Motherboard](images/motherboard)


1. Push in the back panel plate until it snaps into place. The protrusions should be outside the case.
2. Add memory to motherboard.
3. Add M.2 NVMe to motherboard.
4. Carefully place motherboard and screw in with 4 supplied screws from motherboard. One of my standoff threads were messed up.
5. Plug in SFF-8643 into motherboard and feedthrough hole to reach backplane.
6. Plug in SATA1 - SATA8 corresponding to the motherboard. SATA1 is to the left of the case if you are looking at the case.
7. Plug in front panel connector.
8. Plug in USB connectors.
9. Plug in power connectors for motherboard. Note, there are two. 

*Other*
1. Plug in power connector for SATA
11. Plug in ATX power connector to backpanel.
12. Plug in fans.
13. Screw back panel back in with thumbscrews.
14. Flip power on power supply on since the case will be enclosed.
15. Screw top back on with 4 screws using supplied hex wrench.

## Installation

*BIOS Setup*
1. Press F7 for system bios.
2. Check CPU and total memory.
3. Enable Wake On LAN under Advanced -> ACPI Settings -> Resume By Onboard LAN.
4. Save and exit.

*Installation*
1. Turn on power supply.
2. Close case.
3. Plug.
4. Stick in USB stick.
5. Turn on.
6. Follow instructions.
7. Web UI Authentication. Choose Configure using Web UI over Administrative user.
8. Wait for system to boot up.
9. Take note of IP address.
10. Use console option 4) Set up local administrator to set up password for truenas_admin.

## Configuration

*Wake On LAN*
1. Login through web UI using Multicast DNS https://truenas.local or ip address from before.
2. Find MAC address in UI under network for Wake On LAN.
3. Turn off NAS.
4. Turn on NAS using Wake On LAN from another computer.

```bash
sudo apt install wakeonlan
wakeonlan {mac_address}
```

*ZFS*

1. Pray that AI bubble bursts and hard drive prices come down in price.
