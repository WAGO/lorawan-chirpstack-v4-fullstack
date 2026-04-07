# LoRa-Packet-Forwarder for WAGO Edge Computer 752-94xx with full stack implementation of Chirpstack V4

## Prerequisites
- Wago Edge Computer 752-94xx
- Advantech LoRa Gateway Mini-PCIe-Card (WISE-R311) => Wago Ordernumber: xxx-xxx 
- LoRa Skills (only small skills :-))
- Actual OS from Wago on your Edge Device => Download here: https://downloadcenter.wago.com/wago/software/details/mfgikzq7c3ra4l9ejo
- Edge PC connection to the internet to download the needed stuff
- SSH Connection or use the Portainer instance on the Edge PC
<br>
<p align="center" style="margin:0;">
<img src="images/LoRaWan Stack.jpg"
     alt="LoRaWan"
     title="LoRaWan"/>
</p>

This Container setup the whole Chirpstack with the needed LoRaWan packet forwarder for Advantech Card with Semtech Chip.
All Settings will be done within the Rollout-Engine inside the Rollout Container.

## Take care => please choose a uniqe gateway id in the docker start command by youself

### Seeting UP the stack via SSH

```bash
 docker run -it --rm --name="rollout" \
-v /root:/root \
-e GATEWAY_ID="AA555A0000240xxx" \
wagoautomation/chirpstack-rollout-v4:1.0.5
```
If the Rollout Container has finished you find the UI at: <http://IP-EDGE:8080><br>
User: admin<br>
Password: admin<br>
You also will find preinstalled sensor devices inside.<br>

### Seeting UP the stack via Portainer
- Login to Portainer => https://IP-EDGE:9443
- Create a new stack
- Paste the code inside the editor window of the stack
- Deploy the stack via "Deploy" button
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
After Login in to th UI simple add a Gateway with your ID.



