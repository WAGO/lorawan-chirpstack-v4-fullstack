# LoRa Packet Forwarder for WAGO Edge Computer 752-94xx

### Full Stack Implementation with ChirpStack v4

---

## 📦 Overview

This container sets up the complete **ChirpStack v4 stack**, including the required **LoRaWAN packet forwarder** for the Advantech gateway card (Semtech chipset).

All configuration steps are handled automatically by the **Rollout Engine** inside the container.

---

## ⚙️ Prerequisites

* WAGO Edge Computer 752-94xx
* Advantech LoRa Gateway Mini-PCIe Card (WISE-R311)
  → WAGO order number: `xxx-xxx`
* Basic LoRaWAN knowledge
* Latest WAGO OS installed
  → https://downloadcenter.wago.com/wago/software/details/mfgikzq7c3ra4l9ejo
* Internet connection on the Edge device
* SSH access **or** Portainer installed

---

## 🖼️ Architecture Overview

<p align="center">
  <img src="images/LoRaWan Stack.jpg" alt="LoRaWAN Stack" title="LoRaWAN Stack"/>
</p>

---

## ⚠️ Important

Make sure to use a **unique Gateway ID** when starting the container.

---

## 🚀 Setup via SSH

```bash
docker run -it --rm --name="rollout" \
  -v /root:/root \
  -e GATEWAY_ID="AA555A0000240xxx" \
  wagoautomation/chirpstack-rollout-v4:1.0.5
```

### 🔑 Access after setup

* URL: http://IP-EDGE:8080
* User: `admin`
* Password: `admin`

Preconfigured sensor devices are already available.

---

## 🐳 Setup via Portainer

1. Open Portainer: https://IP-EDGE:9443
2. Create a new **Stack**
3. Paste the following configuration
4. Click **Deploy the stack**

```yaml
version: "3.8"

services:
  rollout:
    image: wagoautomation/chirpstack-rollout-v4:1.0.5
    container_name: rollout
    stdin_open: true
    tty: true
    volumes:
      - /root:/root
    environment:
      - GATEWAY_ID=AA555A0000240xxx
    restart: "no"
```

---

## ➕ Final Step

After logging into the UI, simply add your **Gateway** using your configured Gateway ID.

---

## 💡 Notes

* The rollout container is a **one-time setup tool**
* After execution, the container will stop automatically
* This behavior is expected ✔️

---


