# 📱 Live Phone Sensor Setup Guide

## Overview
This guide will help you connect your smartphone to the Activity Recognition app and get real-time predictions!

## 🤖 Android Setup

### Step 1: Install SensorServer App
1. Open Google Play Store on your Android phone
2. Search for **"SensorServer"** or **"Sensor Server"**
3. Install the app by **Aexol** (free app)
4. Alternative: Install **"Physics Toolbox Sensor Suite"**

### Step 2: Configure the App
1. Open SensorServer app
2. Tap on **"Start Server"** or similar button
3. **Note the IP address** shown in the app (e.g., `192.168.1.100`)
4. The default port is usually `8080`

### Step 3: Connect Same WiFi
⚠️ **IMPORTANT**: Your phone and computer MUST be on the **same WiFi network**

- Phone WiFi: Settings → WiFi → Check network name
- Computer WiFi: Make sure it's the same network

### Step 4: Run the Streamlit App
```bash
cd "/Users/rehmankhan/Desktop/ hc/myenv"
./bin/streamlit run app.py
```

### Step 5: Enter Connection Details
1. In the app, go to **"📱 Live Phone Data"** page
2. Enter your phone's IP address (from Step 2)
3. Enter port (default: `8080`)
4. Click **"🟢 Start"** button
5. Move your phone around and watch predictions!

## 🍎 iOS Setup

### Option 1: Sensor Logger (Recommended)
1. Install **"Sensor Logger"** from App Store
2. Enable accelerometer recording
3. Configure to stream data via WiFi
4. Note the IP address and port
5. Use same connection process as Android

### Option 2: Phyphox
1. Install **"phyphox"** from App Store
2. Select "Acceleration (with g)"
3. Enable remote access in settings
4. Note the IP and port provided

## 🔧 Troubleshooting

### Connection Issues
**Problem**: Can't connect to phone
- ✅ Check both devices are on same WiFi
- ✅ Verify IP address is correct
- ✅ Make sure SensorServer is running
- ✅ Check firewall settings on computer
- ✅ Try restarting the SensorServer app

**Problem**: Connection drops
- ✅ Keep phone screen on
- ✅ Disable battery optimization for SensorServer
- ✅ Move closer to WiFi router

### No Predictions
**Problem**: Connected but no predictions showing
- ✅ Make sure accelerometer is selected in SensorServer
- ✅ Move the phone to generate sensor data
- ✅ Check if sensor data is showing in the chart

## 📊 App Features

### 🎯 Single Prediction Page:
- Manual input of accelerometer values (X, Y, Z)
- Random sample selection from test dataset
- Instant activity prediction with visual representation
- See cluster assignment and activity label

### 📱 Live Phone Data Page:
1. **Real-time Charts**: Live X, Y, Z accelerometer values
2. **Activity Predictions**: Current detected activity with emoji
3. **Distribution Pie Chart**: Breakdown of all activities
4. **Recent Predictions Table**: Last 15 predictions with timestamps
5. **Connection Status**: Monitor phone connection in real-time
6. **Current Sensor Values**: Live X, Y, Z measurements

### Activity Types:
- 🧍 **STANDING**: Phone is relatively still, upright
- 🪑 **SITTING**: Phone is stationary
- 🛌 **LAYING**: Phone is horizontal
- 🚶 **WALKING**: Regular movement pattern
- 🪜⬆️ **WALKING_UPSTAIRS**: Climbing motion
- 🪜⬇️ **WALKING_DOWNSTAIRS**: Descending motion

## 💡 Tips for Best Results

1. **Keep phone in pocket or hand** while moving
2. **Walk naturally** for WALKING detection
3. **Stay still** for STANDING/SITTING/LAYING
4. **Use stairs** for upstairs/downstairs detection
5. **Wait 2-3 seconds** after changing activity for accurate detection
6. **Keep phone screen on** to prevent connection drops
7. **Stay close to WiFi router** for stable connection

## 🎯 Testing Without a Phone

If you don't have a phone or can't connect:
1. Go to **"🎯 Single Prediction"** page
2. Choose **"Random Sample from Test Set"**
3. Click **"🎲 Get Random Sample"** repeatedly
4. Click **"🔮 Predict Activity"** to see predictions
5. Compare predicted activity with the true label shown

## 🆘 Still Having Issues?

### Check these requirements:
- [ ] Phone and computer on same WiFi
- [ ] SensorServer app is running
- [ ] IP address is correct
- [ ] Port is 8080 (or correct port from app)
- [ ] Firewall allows the connection
- [ ] Phone screen is on

### Quick Test:
Open a browser and go to: `http://YOUR_PHONE_IP:8080`
- If you see a webpage: Connection is working ✅
- If you get an error: Connection problem ❌

## 📞 App Information

**SensorServer App Features:**
- Streams accelerometer data via WiFi
- Supports multiple sensor types
- Real-time data transmission
- No phone rooting required
- Works on WiFi (no mobile data needed)

**Data Format:**
The app receives JSON data like:
```json
{
  "type": "android.sensor.accelerometer",
  "values": [x, y, z],
  "timestamp": 1234567890
}
```

## 🎯 What to Expect

**Initial Connection:**
- Takes 2-5 seconds to connect
- Status will show "Connected" in green
- Charts will start updating

**During Use:**
- Predictions update every ~0.5 seconds
- Charts show last 100 samples
- Activity distribution updates in real-time

**Performance:**
- Low latency: ~100-200ms
- Smooth visualization
- No lag with good WiFi connection

---

## 📝 Quick Reference

| Device | App Name | Store | Cost |
|--------|----------|-------|------|
| Android | SensorServer | Play Store | Free |
| Android | Physics Toolbox | Play Store | Free |
| iOS | Sensor Logger | App Store | Free |
| iOS | phyphox | App Store | Free |

**Default Settings:**
- Port: `8080`
- Sensor: Accelerometer
- Update Rate: ~50-100ms
- Protocol: WebSocket

---

**Enjoy real-time activity recognition! 🎉**
