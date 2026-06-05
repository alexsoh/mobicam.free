# Mobicam (free)

Turn your Android phone into a **local-network RTSP camera**. Mobicam runs an RTSP server on your phone so any device on the same Wi‑Fi can watch the live feed in VLC, ffplay, or other RTSP clients.

Public download repo for the [Mobicam](https://github.com/alexsoh/mobicam) app (`io.evaultex.app.mobicam`).

## Screenshots

| Setup (before streaming) | Live stream | Watch in VLC |
|---|---|---|
| ![Mobicam setup screen](docs/screenshots/screenshot-setup.png) | ![Mobicam streaming live](docs/screenshots/screenshot-streaming.png) | ![Watch Mobicam in VLC](docs/screenshots/screenshot-vlc.png) |

## Install

1. Download the latest APK from **[Releases](https://github.com/alexsoh/mobicam.free/releases)**.
2. On your phone, allow installation from unknown sources if prompted.
3. Open the APK and install **mobicam**.

Releases are published automatically when a new version ships from the main Mobicam repo.

## How to use

### 1. Connect to Wi‑Fi

Mobicam streams over your **local network**. Connect the phone to the same Wi‑Fi as the device that will watch the stream (laptop, NVR, another phone, etc.).

### 2. Set an RTSP password

On the main screen:

1. Note the fixed RTSP username: **`admin`**
2. Enter an **RTSP password** (required before you can start)
3. The password is saved on the device for next time

The RTSP URL updates automatically with your phone’s local IP address, for example:

```text
rtsp://admin:yourpassword@192.168.1.42:8554/
```

Tap the **share** icon next to the URL to copy or send it to another app.

### 3. Choose stream quality (optional)

Before starting, you can adjust:

| Setting | Options |
|---|---|
| **Resolution** | 1080p, 720p (default), 540p, 480p |
| **Frame rate** | 15, 24, or 30 FPS (default) |
| **Orientation** | Portrait or Landscape |

A lower resolution helps on older phones or congested Wi‑Fi. Settings are locked while streaming.

### 4. Start streaming

1. Tap **START**
2. Grant **Camera**, **Microphone**, and **Notifications** when asked
3. When live, the status changes to **Streaming Live** (green) and the button becomes **STOP**

While streaming, Mobicam keeps running in the background. Use the notification to return to the app or stop the stream.

### 5. Controls while streaming

| Control | Action |
|---|---|
| **STOP** | End the RTSP stream |
| **Mic** | Mute or unmute audio |
| **Camera** | Switch front / rear camera |

### 6. Watch the stream on another device

Use any RTSP client on the **same network**. Examples:

**VLC (desktop or mobile)**

1. **Media → Open Network Stream…**
2. Paste the full URL from Mobicam (including `admin` and your password)
3. Click **Play**

**ffplay (command line)**

```bash
ffplay -rtsp_transport tcp "rtsp://admin:yourpassword@192.168.1.42:8554/"
```

Replace `192.168.1.42` with the IP shown in the Mobicam app.

## Requirements

- Android 7.0+ (API 24)
- Camera and microphone permissions
- Wi‑Fi network shared with the viewer

## Troubleshooting

**Stream won’t start**

- Set an RTSP password first
- Confirm camera and microphone permissions are allowed
- Try a lower resolution (e.g. 720p or 540p)

**Viewer can’t connect**

- Phone and viewer must be on the **same Wi‑Fi** (not mobile data)
- Use the IP address shown in Mobicam — it changes if the phone gets a new DHCP lease
- Some routers block device-to-device traffic; disable “AP isolation” / “client isolation” if enabled
- Prefer **TCP** transport in your player if UDP is blocked

**Choppy or high latency**

- Move closer to the Wi‑Fi access point
- Lower resolution or frame rate
- Reduce other traffic on the network

## Technical notes

- Default RTSP port: **8554**
- Stream path: **`/`** (root — use the exact URL shown in the app)
- Streams H.264 video and AAC audio over RTSP
- IPv4 only
