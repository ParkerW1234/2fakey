<h1>USB-C nRF52840 Passkey</h1>

<p>
A compact USB-C security key based on the Nordic nRF52840.
</p>

<hr>

<h2>Overview</h2>

<ul>
  <li>MCU: nRF52840 (ARM Cortex-M4F)</li>
  <li>USB-C device (UFP)</li>
  <li>SWD programming via test pads</li>
  <li>LED and reset button</li>
  <li>2-layer PCB</li>
</ul>

<hr>

<h2>Schematic</h2>
<img width="576" height="363" alt="Screenshot 2025-12-31 at 7 29 01 PM" src="https://github.com/user-attachments/assets/d6489833-2578-4374-9d0d-ef2b68611414" />

<hr>

<h2>PCB</h2>
<img width="620" height="301" alt="Screenshot 2026-01-01 at 11 02 58 AM" src="https://github.com/user-attachments/assets/2e85413e-ce74-4f9c-ac20-fe77155b46ea" />

<img width="742" height="337" alt="Screenshot 2026-01-01 at 11 04 22 AM" src="https://github.com/user-attachments/assets/1f025a9b-88e0-499f-8328-5fb99b0c3ef3" />


<p>
The PCB is designed like a YubiKey.
</p>

<hr>

<h2>Programming & Setup</h2>

<h3>Required Hardware</h3>
<ul>
  <li>CMSIS-DAP compatible SWD programmer</li>
  <li>Pogo pins or jumper wires</li>
  <li>USB-C cable</li>
</ul>

<h3>SWD Connections</h3>

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

<h3>Flashing Firmware</h3>

<pre>
pyocd flash firmware.hex
</pre>

<p>
Program the device over SWD before enabling USB firmware.
Once programmed, the device will enumerate over USB-C.
</p>

<hr>

<h2>Bill of Materials (BOM)</h2>

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
    <td>N/A</td>
  </tr>
  <tr>
    <td>C*</td>
    <td>Various</td>
    <td>Decoupling and bulk capacitors</td>
    <td>0603</td>
    <td>DEC, DCC, VDD</td>
  </tr>
</table>
