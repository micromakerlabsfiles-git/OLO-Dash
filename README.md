# OLO Dash 🚀

Welcome to the OLO Dash release! This folder contains precompiled binaries, web manifests, and the browser-based Web Serial Controller utility to easily flash and set up your OLO Dash device.

---

## ⚡ 1. Flashing the Firmware

You can flash the OLO Dash firmware directly from your web browser (Chrome or Edge) without installing any development tools.

1. Connect your **ESP32-C3 SuperMini** to your PC using a USB-C data cable.
2. Open the [**`OLO Dash Web Controller`**](https://micromakerlabsfiles-git.github.io/OLO-Dash/) file in this directory using Chrome or Edge.
3. Select your display controller environment from the dropdown menu:
   - **SSD1306** — For standard 0.96" OLED modules.
   - **SH110X** — For 1.3" OLED modules (SH1106 / SH1107).
4. Click **⚡ Install OLO Dash**.
5. Choose the appropriate USB serial port in the browser popup and click **Connect**.
6. Follow the prompts to flash the firmware.

---

## 📡 2. WiFi Configuration & PC Time Sync

Once flashed, configure WiFi credentials and synchronize time directly over the USB connection.

1. On the same [**`OLO Dash Web Controller`**](https://micromakerlabsfiles-git.github.io/OLO-Dash/) web controller, go to the **WiFi Configuration** tab.
2. Click **🔌 Connect via USB Serial** and select your device port.
3. Upon connection, the page will **automatically synchronize your local PC time and timezone** to the device (crucial for accurate offline time display).
4. Enter your home **WiFi Network Name (SSID)** and **WiFi Password**.
5. Click **📶 Send to Device & Reboot**.

---

## 🌐 3. Web Dashboard & Settings Setup

Once the device connects to your local network, you can access the full-featured configuration dashboard from any browser.

1. Navigate to [**`OLO Dash Web Server`**](http://olodash.local) (or the IP address displayed on the device serial log/screen).
2. The dashboard contains the following panels:
   - **Dashboard**: View system status, WiFi connectivity, and local/NTP sync statistics.
   - **Screens**: Customize screen order via drag-and-drop, toggle specific screens, and enable/disable screen auto-cycling.
   - **Animations**: Toggle idle facial animations and change screensaver/idle timings.
   - **API Settings**: Change lat/long coordinates for weather/daylight, setup Yahoo Finance symbols, choose crypto IDs (CoinLore), and set up currency conversions.
   - **Quick Settings**: Toggle buzzer sound, adjust OLED brightness, invert display contrast, and configure the Home Timezone and Dual Time setup (both features support convenient dropdown lists for sorted IANA timezone locations).
