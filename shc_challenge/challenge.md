# You'll need
- challenge board
- USB Cable (connect to UART /dev/ttyACM0, baud rate 2000000)
- Bouffalo Labs Dev Cube (https://dev.bouffalolab.com/download), have a look at View --> Advanced to dump the flash if you want to ;)
- Some inspiration from here: https://github.com/sipeed/M1s_BL808_Linux_SDK


# Challenge Description
This is a very secure kernel level HSM implementation. Once you connect to UART (use the lower port number of both for shell, higher for programming), press the reset button and you'll see the system boot up.
You'll be dropped in the terminal of the HSM directly. Enter the correct pin code, and you'll get the flag.

This device has been hardened, so no, you don't have direct access to the passwordless busybox root shell anymore, too bad...
