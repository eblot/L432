#  Simple USB-CDC-ACM implementation: USB to UART bridge

## Overview

Simple bridge to drive a UART port from a USB port with HW flow control (RTS/CTS), for [Nucleo STM32L432KC](http://www.st.com/en/evaluation-tools/nucleo-l432kc.html) boards, and [ChibiOS](http://chibios.org/).

This code comes from [ChibiOS](http://chibios.org/) examples.

## Usage

This application may be used as a replacement for [FTDI *232](http://www.ftdichip.com) USB-UART bridges which are unable to manage HW flow control properly (see FTDI datasheet for details: FTDI may output up to 3 extra bytes after the peer UART raised its RTS signal).

It has been tested with baudrate up to 1.5 Mbps.

UART properties (baudrate, data bits, parity, stop bits) is set from the host.
HW flow control is always on (but is trivial to disable @ build time).

No driver is needed on most hosts, as the application follows the USB-CDC ACM specification.
On Windows, a `.INF` file may be required (I do not care about M$); it works out of the box with Linux and macOS hosts.

## IO pins

### UART port w/ HW flow control

 * TX:  PB.6 (STM32 -> peer)
 * RX:  PB.7 (STM32 <- peer)
 * RTS: PB.3 (STM32 -> peer)
 * CTS: PB.4 (STM32 <- peer)

### Debug port (TX only)

 * SD2 is connected to the STM32F1 on Nucleo 432KC board (USB)

### USB FS

It is recommended to use low value resistors (typically 22Ω) to connect USB
port to DP/DM signal.

 * DP: PA.12 (green)
 * DM: PA.11 (white)
