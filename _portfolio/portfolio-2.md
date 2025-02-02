---
title: "Smart Mirror Project Using Python and Raspberry Pi"
excerpt: "A **Smart Mirror** is a two-way mirror with an electronic display behind it, showing useful information such as time, weather, calendar events, and news updates."
collection: projects
---

## Overview

A **Smart Mirror** is a two-way mirror with an electronic display behind it, showing useful information such as time, weather, calendar events, and news updates. This project uses a **Raspberry Pi** and **Python** to build a fully customizable smart mirror that integrates various APIs and modules to enhance its functionality. This guide will walk you through each step, from gathering materials to coding and assembling the mirror.

## Features

- **Time and Date Display**
- **Weather Forecast** (via OpenWeatherMap API)
- **Calendar Integration** (Google Calendar API)
- **News Feed** (RSS Feeds)
- **Compliment Generator**
- **Voice Control** (using Google Assistant SDK)
- **Custom Modules** (e.g., reminders, to-do lists)

## Components Required

### Hardware

1. **Raspberry Pi 4** (with microSD card, 16GB minimum, and official power supply)
2. **Two-Way Acrylic Mirror** (sized to fit your monitor)
3. **Monitor** (preferably with HDMI input, size depends on your mirror frame)
4. **HDMI Cable** (for connecting the Pi to the monitor)
5. **Wooden Frame** (custom-built to house the monitor and mirror)
6. **USB Keyboard and Mouse** (for initial setup)
7. **Wi-Fi Connectivity** (via built-in Pi Wi-Fi or Ethernet)
8. **Speakers** (for voice assistant functionality)
9. **Double-sided Tape or Mounting Hardware** (to secure components)
10. **Cooling Fan** (optional, if you plan to run the Pi for extended periods)

### Software

1. **Raspberry Pi OS** (Raspbian)
2. **Python 3** (comes pre-installed with Raspbian)
3. **PIP** (Python Package Installer)
4. **MagicMirror² Framework** (Node.js-based with Python integration)
5. **OpenWeatherMap API Key** (for weather data)
6. **Google Calendar API Setup** (for calendar events)
7. **Google Assistant SDK** (for voice control)
8. **VNC Viewer** (optional, for remote access)

## Step-by-Step Instructions

### Step 1: Setting Up the Raspberry Pi

1. **Download Raspberry Pi OS:**
   - Visit the [official Raspberry Pi website](https://www.raspberrypi.org/software/) and download the Raspberry Pi Imager.

2. **Flash OS to microSD Card:**
   - Insert the microSD card into your computer.
   - Open Raspberry Pi Imager, select "Raspberry Pi OS (32-bit)", choose your microSD card, and click "Write".

3. **Initial Boot and Configuration:**
   - Insert the microSD card into the Raspberry Pi.
   - Connect the Pi to the monitor using an HDMI cable.
   - Attach the keyboard and mouse.
   - Plug in the power supply to boot up the Raspberry Pi.

4. **Complete Setup Wizard:**
   - Follow the on-screen instructions to set up language, Wi-Fi, and password.

5. **Update the System:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

### Step 2: Installing Required Software

1. **Install Python Libraries:**
   ```bash
   sudo apt install python3-pip
   pip3 install requests feedparser google-auth google-api-python-client
   ```

2. **Install Node.js and MagicMirror²:**
   ```bash
   curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
   sudo apt install -y nodejs
   git clone https://github.com/MichMich/MagicMirror
   cd MagicMirror
   npm install
   ```

3. **Auto-Start MagicMirror on Boot:**
   ```bash
   npm install -g pm2
   pm2 start npm --name "magicmirror" -- start
   pm2 save
   pm2 startup
   ```

### Step 3: Configuring MagicMirror Modules

1. **Navigate to Configuration File:**
   ```bash
   cd ~/MagicMirror/config
   nano config.js
   ```

2. **Add Default Modules:**
   - Time, Calendar, Weather, and Newsfeed modules come pre-configured. Modify them according to your needs:
   ```javascript
   modules: [
       {
           module: "clock",
           position: "top_left"
       },
       {
           module: "calendar",
           header: "Google Calendar",
           position: "top_right",
           config: {
               calendars: [
                   {
                       symbol: "calendar",
                       url: "YOUR_GOOGLE_CALENDAR_URL"
                   }
               ]
           }
       },
       {
           module: "weather",
           position: "top_right",
           config: {
               location: "Your City",
               appid: "YOUR_OPENWEATHERMAP_API_KEY"
           }
       }
   ]
   ```

### Step 4: Creating Custom Python Modules

1. **Write a Python Script for Weather Information:**
   ```python
   import requests
   from datetime import datetime

   def get_weather():
       API_KEY = 'YOUR_OPENWEATHERMAP_API_KEY'
       CITY = 'YourCity'
       response = requests.get(f'http://api.openweathermap.org/data/2.5/weather?q={CITY}&appid={API_KEY}')
       data = response.json()
       weather = data['weather'][0]['description']
       temp = round(data['main']['temp'] - 273.15, 2)
       return f'Weather: {weather}, Temperature: {temp} °C'

   def get_time():
       now = datetime.now()
       return now.strftime('%H:%M:%S')

   if __name__ == "__main__":
       print(get_time())
       print(get_weather())
   ```

2. **Integrate Python Output with MagicMirror:**
   - Use Node.js `child_process` to execute Python scripts from MagicMirror modules.
   ```javascript
   const { exec } = require('child_process');

   exec('python3 /path/to/your/script.py', (error, stdout, stderr) => {
       if (error) {
           console.error(`exec error: ${error}`);
           return;
       }
       console.log(`Weather Output: ${stdout}`);
   });
   ```

### Step 5: Building the Mirror Frame

1. **Measure and Cut the Frame:**
   - Measure your monitor dimensions and cut the wooden frame pieces accordingly.

2. **Assemble the Frame:**
   - Use screws or nails to assemble the frame securely.

3. **Install the Monitor:**
   - Place the monitor behind the two-way acrylic mirror and secure it with mounting brackets or double-sided tape.

4. **Mount the Raspberry Pi:**
   - Attach the Raspberry Pi to the back of the monitor using adhesive strips or screws.

5. **Cable Management:**
   - Organize cables to ensure a clean setup, using cable ties or clips.

6. **Power Up and Test:**
   - Connect all components, power up the Raspberry Pi, and ensure the smart mirror display is functioning correctly.

![Smart Mirror Assembly](/images/imag%201_24259.png)

### Step 6: Adding Voice Control with Google Assistant

1. **Install Google Assistant SDK:**
   ```bash
   python3 -m pip install --upgrade google-assistant-sdk[samples]
   python3 -m pip install --upgrade google-auth-oauthlib[tool]
   ```

2. **Configure Google Assistant:**
   - Follow the [Google Assistant SDK setup guide](https://developers.google.com/assistant/sdk) to create credentials.

3. **Test Google Assistant:**
   ```bash
   google-assistant-demo
   ```

### Step 7: Customizing Your Smart Mirror

- **Add More Modules:** Explore additional modules from the MagicMirror² community to extend functionality.
- **Styling:** Customize the CSS in `MagicMirror/css/custom.css` for a unique display.
- **Expand Functionality:** Add modules like to-do lists, traffic updates, and more.

## Conclusion

This **Smart Mirror Project** not only adds a futuristic touch to your home but also serves as a practical tool for everyday information. With detailed customization options, you can continuously expand its capabilities to suit your needs. 

![Final Smart Mirror](/images/final_front_big.jpg)

---

Happy Building! 🚀


