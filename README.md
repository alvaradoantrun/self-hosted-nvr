# Self-Hosted IP Camera System with Tailscale & go2rtc

A home lab project where I built a self-hosted remote camera system using a Raspberry Pi, go2rtc, and Tailscale — allowing secure remote access to a live camera feed from anywhere without port forwarding or third-party cloud services.

🔗 **GitHub Repo:** https://github.com/alvaradoantrun/self-hosted-nvr

**Related Projects:**
- [Active Directory Home Lab](https://github.com/alvaradoantrun/active-directory-home-lab)
- [osTicket Help Desk Lab](https://github.com/alvaradoantrun/osticket-lab)
- [Wazuh SIEM Lab](https://github.com/alvaradoantrun/Wazuh-SIEM-Lab)
- [OWASP Juice Shop Lab](https://github.com/alvaradoantrun/Juice-shop-lab)

## Overview

Instead of relying on a cloud-based camera service, I built my own system where the camera stream goes directly from the camera to my Raspberry Pi to my phone over a private VPN — no router changes, no third-party servers.

## Environment

| Component | Details |
|---|---|
| Stream Relay | go2rtc v1.9.14 on Raspberry Pi |
| VPN | Tailscale |
| Camera Protocol | RTSP |
| Remote Access | Tailscale IP 100.116.224.7 |
| Web UI Port | 1984 |

## What I Built

- Scanned the network to locate the IP camera and identify its IP address
- Pulled the raw RTSP stream URL from the camera
- Downloaded and configured go2rtc on the Raspberry Pi
- Created a `go2rtc.yaml` config file pointing to the camera RTSP stream
- Ran go2rtc and verified it was listening on the correct ports
- Installed Tailscale on the Raspberry Pi and connected a phone to the same tailnet
- Accessed the go2rtc web UI remotely from a phone using the Tailscale IP
- Verified live camera stream was accessible outside the home network

## go2rtc Config

```yaml
streams:
  cam1: rtsp://admin:PASSWORD@CAMERA_IP:554/Streaming/Channels/101
```

## Problems Encountered

- go2rtc YAML config errors — resolved by fixing formatting issues in the config file
- Stream not accessible remotely — resolved by installing Tailscale for private VPN access
- Had to debug go2rtc startup logs to confirm the API and WebRTC were listening correctly

## Screenshots

### go2rtc Running on Raspberry Pi via VNC
![go2rtc terminal](pictures/Screenshot%20from%202026-04-20%2019-01-08%20(2).png)

### Tailscale Dashboard — Pi and Phone Connected
![Tailscale dashboard](pictures/Screenshot%20from%202026-04-20%2019-01-35.png)

### go2rtc Web UI Accessed from Phone over Tailscale
![go2rtc on phone](pictures/Screenshot_20260420-190224.Chrome%20-%20Copy.png)

## Skills Demonstrated

- RTSP stream configuration
- Linux command line
- Network scanning and device identification
- VPN setup and management with Tailscale
- go2rtc deployment and configuration
- Remote access without port forwarding
- YAML configuration files

## Tools Used

- Raspberry Pi OS
- go2rtc
- Tailscale
- RTSP
- nano
- Linux terminal
- RealVNC Viewer

## Why This Matters

Most consumer camera systems send your footage through a third-party cloud server. This setup keeps everything private — the stream never leaves your own devices. It also demonstrates a real-world understanding of VPN tunneling, stream protocols, and self-hosted infrastructure.
