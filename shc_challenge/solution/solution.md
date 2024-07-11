# Recovery / flashing
- Boards are prepared already, probably not needed.
- Sensitive info is contained in whole_image.bin, rest can be handed out if they break it. Contestants may have it if the challenge is too hard I guess, but they should extract it themself.

## UART adapter broken
- Start devcube for BL702. 
- Hold BOOT while pluggin in to UART
- Flash the usb2dualuart_bl702_20230221.bin file on MCU Page

## Low level loader
- Start devcube for BL808
- select group0 on m0 low_load_bl808_m0.bin at address 0x58000000
- select group1 on d0 low_load_bl808_d0.bin at address 0x58000000
- Program on ACM1

## OS Broken
- Start devcube for BL808
- Select whole_image.bin on IOT Page
- Program on ACM1

## Modify squashfs
```bash
sudo unsquashfs squashfs_test.img 
```
modify files
```bash
sudo mksquashfs squashfs-root/* /home/toni/Desktop/M1s_BL808_Linux_SDK/out/squashfs_test.img
```


# Easiest Solution
Dump the firmware using dev cube --> view --> advanced --> Firmware. 
Dump starting at 0xD2000 till enough (e.g. 0xf00000)

Merge default squashfs file (or patch the extracted one however you want) into this image using:
```bash
dd if=squashfs_test_original.img of=flash.bin seek=4718592 bs=1 conv=notrunc
``` 

connect again after flashing via IOT img upload, now you got root access.
mknode from old squashfs file /etc/init.d/rc.local
```bash
mknod /dev/fakehsm c 249 0
```

read file /dev/fakehsm, or bruteforce pin, or whatever...


Pin is: 131694
Flag is: SHC{YayyLinuxKernelStuffOnStrangeHW}

