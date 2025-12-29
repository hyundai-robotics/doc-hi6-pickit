## 1.2 Hardware Configuration

The main components required for the plugin operation are:  
`Hi6 COM`, `Hi6 TP`, `pick-it processor`, `pick-it camera`, `hub` or `router`  

<br>

1. When connecting in the 192.168.2.XX range
   - The 192.168.2 network range is used for communication between the TP and COM. Therefore, the plugin cannot receive images through the 2.x range.
   - However, if it is absolutely necessary to use the 2.x range, you can still receive images by configuring the network with a hub as shown below.
   - Hardware configuration diagram<br>
   <img src="../../_assets/04_hardware_net.png" height=310hv>

2. For other network ranges
   - You can use the general-purpose LAN port of Hi6 COM for connection.
   - Example) If the video server host address is 192.168.1.100 and the communication port is 8070:
     1. Configure the gateway of the video server
        - Set the gateway of the video server to match the IP address of the controller you want to connect to.  
        ex) When connecting via LAN1, the gateway of the video server must be set to 192.168.1.150.

            <div style="border:3px solid #0B57D0; background:#E9F2FF; color:#0B2E57; padding:1px 3px; border-radius:10px; max-width:fit-content; rgba(0,0,0,.08);">
            <span>🛠️</span><span>When configuring in Windows 10</span>
            <ol style="margin:0; padding-left:25px; line-height:1.8; font-size:14px;">
                <li>Start → View Network Connections</li>
                <li>Right-click the connected Ethernet → Properties</li>
                <li>Select Internet Protocol Version 4 (TCP/IPv4) → Properties</li>
                <li>Select "Use the following IP address"</li>
                <li>Enter IP Address / Subnet Mask / Gateway</li>
            </ol>
            </div>

      2. TP Network Configuration

   - TP > Enter Administrator Mode (R314) > Service > 13: Teach Pendant Network > Confirm agreement > Proceed with the following settings:

       <div style="border:2px solid red; background-color:#ffecec; color:#d8000c; padding:12px; font-weight:bold; font-size:14px; max-width:fit-content; border-radius:6px;">
       ⚠️ [Caution] Selecting any option other than the ones below will change the TP IP address, 
       causing loss of communication between controllers. Since recovery in the field is very difficult, 
       <strong>you must configure exactly as instructed below.</strong>
       </div><br>

       - IP: 192.168.2.77  
       - Subnet Mask: 24  
       - Gateway: 192.168.2.150  

   - Reboot the controller



     3. Modify the plugin URL

   - Navigate to: pickit folder > ui folder > js folder > display.js  
     Update the video streaming service URL accordingly.

       <div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
       Currently, the plugin is provided only to customers who have obtained prior approval for use.<br>
       Contact: HD Hyundai Robotics Research Engineer, Donghyeong Lee (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
       </div><br>

        <div style="max-width:fit-content;">

        ```python
        # Example: host IP = 192.168.1.100, port = 8070, construct the query according to the service
        var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
        ```
        </div>

     4. Install the plugin  
   - Refer to the [Installation Guide](../3-sw_install/README.md) to install the modified plugin from step 3 on the controller.
