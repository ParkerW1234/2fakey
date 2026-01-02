<h1>USB-C nRF52840 Passkey</h1>

<p>
This is a small USB-C security key built around the Nordic nRF52840.
The goal of this project was to make something that feels like a YubiKey.
</p>

<p>
It’s meant for learning, experimenting, and building custom 2FA / passkey style
devices.
</p>

<hr>

<h2>Overview</h2>

<ul>
  <li>MCU: nRF52840 (ARM Cortex-M4F)</li>
  <li>USB-C device (UFP)</li>
  <li>SWD programming using test pads</li>
  <li>On-board LED and reset button</li>
  <li>Simple 2-layer PCB</li>
</ul>

<p>
The design keeps things as simple as possible while still supporting USB and
debug access.
</p>

<hr>

<h2>Schematic</h2>

<p>
Below is the full schematic for the board. It includes USB-C CC resistors,
USB ESD protection, a 32 MHz crystal for USB operation, power regulation,
and SWD test points for programming.
</p>

<img width="576" height="363" alt="Screenshot 2025-12-31 at 7 29 01 PM" src="https://github.com/user-attachments/assets/d6489833-2578-4374-9d0d-ef2b68611414" />

<hr>

<h2>PCB</h2>

<p>
The PCB is laid out to be small and USB drive/key shaped.
It was very difficult to route this pcb as everything is quite close.
</p>

<img width="620" height="301" alt="Screenshot 2026-01-01 at 11 02 58 AM" src="https://github.com/user-attachments/assets/2e85413e-ce74-4f9c-ac20-fe77155b46ea" />

<img width="742" height="337" alt="Screenshot 2026-01-01 at 11 04 22 AM" src="https://github.com/user-attachments/assets/1f025a9b-88e0-499f-8328-5fb99b0c3ef3" />

<p>
The overall shape and layout are inspired by a YubiKey or another 2fa key but everything here is custom.
All components are standard parts that can be sourced easily.
</p>

<hr>

<h2>Programming & Setup</h2>

<p>
The board is programmed over SWD using test pads. There are no permanent headers,
which keeps the board small, but it does mean you need pogo pins or temporary wires
to program it.
</p>

<h3>Required Hardware</h3>
<ul>
  <li>CMSIS-DAP compatible SWD programmer</li>
  <li>Pogo pins or thin jumper wires</li>
  <li>USB-C cable</li>
</ul>

<h3>SWD Connections</h3>

<p>
Connect the programmer to the board using the following pads:
</p>

<table>
  <tr>
    <th>Board Test Pad</th>
    <th>Programmer Pin</th>
  </tr>
  <tr>
    <td>SWDIO</td>
    <td>SWDIO</td>
  </tr>
  <tr>
    <td>SWDCLK</td>
    <td>SWCLK</td>
  </tr>
  <tr>
    <td>GND</td>
    <td>GND</td>
  </tr>
  <tr>
    <td>3V3</td>
    <td>VTref / VCC Sense</td>
  </tr>
  <tr>
    <td>RESET</td>
    <td>RESET</td>
  </tr>
</table>

<h3>Software</h3>
<ul>
  <li>pyOCD or OpenOCD</li>
  <li>ARM GCC toolchain</li>
  <li>Nordic nRF5 SDK or Zephyr</li>
</ul>

<p>
Zephyr is recommended for anything involving USB or HID,
but basic bring-up and testing can be done with simple bare-metal code.
</p>

<h3>Flashing Firmware</h3>

<pre>
pyocd flash yourfirmware.hex
</pre>

<p>
Firmware is flashed over SWD first. Once valid USB firmware is running,
the device will show up as a USB device when plugged in.
</p>

<hr>

<h2>Bill of Materials (BOM)</h2>

<p>
Below is a simplified BOM listing the main parts used on the board.
Exact part numbers and sourcing details are available in the full BOM files.
</p>

<table>
  <tr>
    <th>Reference</th>
    <th>Part</th>
    <th>Description</th>
    <th>Package</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>U1</td>
    <td>nRF52840</td>
    <td>Bluetooth LE SoC with USB</td>
    <td>QFN</td>
    <td>Main MCU</td>
  </tr>
  <tr>
    <td>USB1</td>
    <td>USB-C Receptacle</td>
    <td>USB Type-C connector</td>
    <td>SMD</td>
    <td>Device mode</td>
  </tr>
  <tr>
    <td>D1</td>
    <td>USB6B1RL</td>
    <td>USB ESD Protection</td>
    <td>SOT-23</td>
    <td>Protects D+/D−</td>
  </tr>
  <tr>
    <td>U2</td>
    <td>AP2112K-3.3</td>
    <td>3.3&nbsp;V LDO Regulator</td>
    <td>SOT-23-5</td>
    <td>VBUS to 3V3</td>
  </tr>
  <tr>
    <td>X1</td>
    <td>32&nbsp;MHz Crystal</td>
    <td>Main system clock</td>
    <td>SMD</td>
    <td>Required for USB</td>
  </tr>
  <tr>
    <td>R1, R2</td>
    <td>5.1&nbsp;kΩ</td>
    <td>USB-C CC pull-down resistors</td>
    <td>0603</td>
    <td>UFP configuration</td>
  </tr>
  <tr>
    <td>N/A</td>
    <td>Programmer</td>
    <td>DAPLink CMSIS-DAP Programmer Debugger, Cortex, STM32</td>
    <td>N/A</td>
    <td>Used for flashing over SWD</td>
  </tr>
  <tr>
    <td>C*</td>
    <td>Various</td>
    <td>Decoupling and bulk capacitors</td>
    <td>0603</td>
    <td>DEC, DCC, VDD</td>
  </tr>
</table>
