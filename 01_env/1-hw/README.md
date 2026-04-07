## 1.1 Hardware Configuration

The main components required for the plugin operation are:  
`${cont_model} COM`, `${cont_model} TP`, `pick-it processor`, `pick-it camera`, `hub` or `router`  

<br>

### a. When connecting in the 192.168.2.XX range
- The 192.168.2 network range is used for communication between the TP and COM. Therefore, the plugin cannot receive images through the 2.x range.
- However, if it is absolutely necessary to use the 2.x range, you can still receive images by configuring the network with a hub as shown below.
<img src="../../_assets/04_hardware_net.png" height=310hv>

### b. For other network ranges
- You can use the general-purpose LAN port of ${cont_model} COM for connection.
- Example) If the video server host address is 192.168.1.100 and the communication port is 8070:

#### b-1. Configure the gateway of the video server
- Set the gateway of the video server to match the IP address of the controller you want to connect to.  
  ex) When connecting via LAN1, the gateway of the video server must be set to 192.168.1.150.

{% hint style="info" %}
When configuring in Windows 10  

1. Start → View Network Connections
2. Right-click the connected Ethernet → Properties
3. Select Internet Protocol Version 4 (TCP/IPv4) → Properties
4. Select "Use the following IP address"
5. Enter IP Address / Subnet Mask / Gateway

{% endhint %}

#### b-2. TP Network Configuration

- After entering Engineer Mode(R314), then navigate to `[F1: Service] - 13: Teach Pendant Network`. Confirm the agreement and proceed with the following settings:

{% hint style="warning" %}

[Caution] Selecting any option other than the ones below will change the TP IP address, 
causing loss of communication between controllers. Since recovery in the field is very difficult, 
you must configure exactly as instructed below.

- IP: 192.168.2.77  
- Subnet Mask: 24  
- Gateway: 192.168.2.150  

{% endhint %}

- Reboot the controller

#### b-3. Modify the plugin URL

- Navigate to: pickit folder > ui folder > js folder > display.js  
  Update the video streaming service URL accordingly.

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
Currently, the plugin is provided only to customers who have obtained prior approval for use.<br>
Contact: HD Hyundai Robotics Research Engineer, Donghyeong Lee (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div>

<div style="max-width:fit-content;">

```python
# Example: host IP = 192.168.1.100, port = 8070, construct the query according to the service
var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
```
</div>

#### b-4. Install the plugin  
- Refer to the [Installation Guide](../2-sw_install/README.md) to install the modified plugin from step 3 on the controller.
