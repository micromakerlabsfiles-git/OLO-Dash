# OLO Dash 🎛️

**OLO Dash** is a feature-rich desk gadget OS for the **ESP32-C3 SuperMini** with a 128×64 OLED display. It shows real-time data (weather, crypto, stocks, air quality, and more), plays animated face expressions, and is controlled entirely via web — no phone apps, no PC companion software required.

---

## ✨ Features

### 📊 Data Screens
| Screen | Data Source |
|---|---|
| 🕐 Time & Date | NTP (automatic timezone lookup) |
| 📅 Calendar | Public holidays (date.nager.at) |
| 🌤 Weather | Open-Meteo (free, no API key) |
| 💨 Air Quality | Open-Meteo AQI (free) |
| ☀️ Daylight Times | Sunrise-Sunset API |
| 📈 Stock Prices | Yahoo Finance (up to 5 symbols, dynamically added/sorted) |
| 🪙 Crypto Prices | CoinLore (up to 5 coins) |
| 💱 Currency Rates | FawazAhmed Currency API (up to 5 dynamic conversions) |
| 🕰️ Dual Time | WorldTimeAPI (fetches dynamic IANA daylight offsets for your target city) |

### 😊 Face Animations (14 total)
- **Blinking** — Default idle animation (blinking eye sequence)
- Look Left / Right / Down
- UwU (featuring 😚 and sneezing face 🤧)
- Angry, Awkward Laugh, Cry, Furious, Happy, Scared, Smile, Sneeze
- **Sleepy** — Sleep screensaver (triggered automatically from idle)

### 🌐 Web Interface
- **`olodash.local`** — Full premium web dashboard (mobile-responsive)
- **Web Controller** — Browser-based firmware installer + WiFi config over Web Serial
- No AP mode — credentials configured safely over USB
- Dynamic row editors for Stocks and Currency conversions

### 📳 Gesture Controls
| Gesture | Action |
|---|---|
| 1 Tap | Next screen / Wake instantly from sleep |
| 2 Taps | Open Settings Menu (while in IDLE) / Go back to idle (from DATA_SCREEN) |
| 3+ Taps | Open Settings Menu |
| Long Press | Return to Idle |

### 💡 Hardware & Feedback
- **LED (GPIO 6)** — Breathing in idle, 4s booting rainbow loop, status colors for boot/sleep
- **Buzzer (GPIO 2)** — Boot chime (Classic Mac, Sweet, Retro, or Cozy), tick tones, success melodies

---

## 🔧 Hardware Requirements

| Component | Specification |
|---|---|
| Microcontroller | ESP32-C3 SuperMini |
| Display | SSD1306 or SH110X 128×64 OLED |
| Button | Tactile or capacitive (GPIO1) |
| LED | Simple LED or WS2812 NeoPixel (GPIO6) |
| Buzzer | Passive piezo buzzer (GPIO2) |

### Wiring Table

| Component | Pin | GPIO |
|---|---|---|
| OLED SDA | I²C Data | GPIO 20 |
| OLED SCL | I²C Clock | GPIO 21 |
| Touch Button | Input | GPIO 1 |
| LED | Status Light | GPIO 6 |
| Buzzer | Audio | GPIO 2 |
| VCC | Power (OLED, LED) | 3.3V |
| GND | Ground | GND |

---

## 🚀 Quick Start

### Step 1 — Wire the Hardware
Connect all components as shown in the wiring table above.

### Step 2 — Flash the Firmware
1. Open `webcontroller/index.html` in Chrome or Edge
2. Select your OLED type (SSD1306 or SH110X)
3. Connect the ESP32-C3 via USB
4. Click **"Install OLO Dash"**

### Step 3 — Configure WiFi
1. In the Web Controller, go to **WiFi Setup** tab
2. Click **"Connect via USB Serial"**
3. Enter your WiFi SSID and Password
4. Click **"Send to Device & Reboot"**

### Step 4 — Open the Dashboard
Once connected to WiFi, navigate to **`http://olodash.local`** from any device on the same network.

---

## 🌐 olodash.local Web Dashboard

The device hosts a full-featured web panel with 5 tabs:

| Tab | Features |
|---|---|
| **Dashboard** | Device status, WiFi info, API quota today, quick actions |
| **Screens** | Enable/disable screens (including Dual Time), drag to reorder, set cycle interval |
| **Animations** | Toggle each animation, set sleep timeout, idle return time |
| **API Settings** | Location, timezone, temp unit, screen toggles, stock/crypto config, dynamic list rows |
| **Quick Settings** | Sound, LED, display invert, time format, brightness, startup boot chime selection, Dual Time setup |

### API Quota Display
Every API call is counted per-service and shown in both:
- The **olodash.local Dashboard** tab
- The **OLED Settings Menu** (triple-tap → API Quota item)

Counts reset automatically at midnight.

---

## 📁 Project Structure

```
OLO-Dash-Project/
├── platformio.ini          # Build configuration
├── README.md               # This file
├── QUICKSTART.md           # 1-page quick start
├── src/
│   ├── main.cpp            # State machine + gesture handling
│   ├── structs.h           # All data structures + enums
│   ├── ConfigManager.*     # NVS settings persistence
│   ├── JsonSerializer.*    # JSON config serialization
│   ├── AnimationManager.*  # 14-animation face system
│   ├── DisplayService.*    # U8g2-based screen rendering
│   ├── BuzzerService.*     # Audio feedback
│   ├── WebServerService.*  # olodash.local web panel
│   ├── WebSerialService.*  # USB Serial JSON protocol
│   ├── TimeService.*       # NTP + timezone
│   ├── WeatherService.*    # Open-Meteo weather
│   ├── AirQualityService.* # Open-Meteo AQI
│   ├── DaylightService.*   # Sunrise-sunset API
│   ├── CalendarService.*   # Public holidays API
│   ├── CryptoService.*     # CoinLore crypto prices
│   ├── CurrencyService.*   # Currency exchange rates
│   ├── StockService.*      # Yahoo Finance stocks
│   └── zones.h/cpp         # IANA → POSIX timezone lookup
└── webcontroller/
    └── index.html          # Web Controller (flasher + WiFi setup)
```

---

## ⚙️ Building

### Prerequisites
- [PlatformIO](https://platformio.org/) (VSCode extension or CLI)
- GIF animation headers in `../OLO-Dash/gif/` (referenced from OLO-TinyTosh repo)

### Build Commands
```bash
# Build for SH110X display (default)
pio run -e sh110x

# Build for SSD1306 display
pio run -e ssd1306

# Flash to device
pio run -t upload -e sh110x

# Open serial monitor
pio device monitor
```

---

## 🔧 Configuration

All configuration is stored in NVS (non-volatile storage) and survives reboots.

### Via Web Dashboard (`olodash.local`)
Change any setting from any browser on the same WiFi network.

### Via Web Serial (USB)
Send JSON commands from the Web Controller:
```json
{"cmd":"set_wifi","ssid":"MyNetwork","pass":"mypassword"}
{"cmd":"set_config","show_weather":1,"temp_unit":"C"}
{"cmd":"get_config"}
{"cmd":"reboot"}
```

---

## 🐞 Troubleshooting

| Problem | Solution |
|---|---|
| Display blank after flash | Check OLED type — re-flash with SH110X or SSD1306 |
| WiFi not connecting | Re-send credentials via USB Serial (check SSID/password) |
| `olodash.local` not found | Try the IP address shown on OLED; some routers block mDNS |
| No animations | Ensure GIF headers are in `../OLO-Dash/gif/` and rebuild |
| Web Serial not working | Use Chrome or Edge (not Firefox/Safari) |
| Buzzer too loud | Triple-tap → Settings → Sound → OFF |

---

## 📄 License
MIT License — See LICENSE file for details.

---

*Made with ❤️ for desk gadget enthusiasts*
