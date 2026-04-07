
[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - Pick-it Plugin

[__SOURCE](0-about-this-manual/precautions.md)
# Precautions

{% include file="en/precautions.md" %}

[__SOURCE](01_env/README.md)
# 1. Environment Configuration

This page describes the HW and SW configuration required to run the pick-it plugin.

- [1.1 H/W Configuration](./1-hw/README.md)
- [1.2 Installation](./2-sw_install/README.md)
- [1.3 Network Configuration](./3-network/README.md)
[__SOURCE](01_env/1-hw/README.md)
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

[__SOURCE](01_env/2-sw_install/README.md)
## 1.2 Installation

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
Currently, the plugin is provided only to customers who have obtained prior approval for use.<br>
Contact: HD Hyundai Robotics Research Engineer, Donghyeong Lee (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div><br>


Proceed with installing the plugin through the TP screen using USB.  
The detailed process is as follows.  

<div style="max-width:fit-content;">

|Step|Contents|
|---: |:---|
| `1` | Save the pick-it plug-in program to USB. |
| `2` | Connect USB to TP. |
| `3` | Enter `[F1: Service] - 5: File manager`, then `USB` > `pickit` folder > `copy` |
| `4` | `MAIN` folder > `apps` folder > `paste` |
| `5` | Reboot ${cont_model} COM |
| `6` | `[F2: System] - 4: Application parameter - 25: pickit` |

</div>
[__SOURCE](01_env/3-network/README.md)
## 1.3 Network Configuration

${cont_model} Main and pick-it processors use Ethernet communication method.   
The IP subnet mask of ${cont_model} Main and pick-it processors is 1 band.   
The IP subnet mask of ${cont_model} TP and pick-it camera is two-band.    
For further details, please refer to the [pick-it official document](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface).

<div style="max-width:fit-content;">

|Property|Contents|
|:----|:----|
|`Connection Type`| `TCP/IP Socket` |
|`Port`| 5001(TCP) |
|`Byte Order`| Network Order (big endian) |

</div>

For pick-it camera setup, you can use the pick-it web interface.  
Please refer to [pick-it's official documentation](https://docs.pickit3d.com/en/latest/documentation/web-interface/index.html).
[__SOURCE](02_preview/README.md)
# 2. Preview

On this page, we will look at two representative UIs that can be seen when using the pick-it plugin.  

- [2.1 Monitoring Panel](./1-panel/README.md)
- [2.2 Setup Window](./2-setup/README.md)
[__SOURCE](02_preview/1-panel/README.md)
## 2.1 Monitoring Panel

It is compatible with existing TP UI features, so you can utilize window split screen, zoom functions, etc.  
You can check the results of the pick-it robot language function operation in real time through the monitoring panel.  
In the `Request to Pickit`  field confirms the command and attribute values requested by the Pickit processor.  
In the `Response from Pickit` field, you can check the status of the response and additional information.

Here's how to split a window:  
- `pane layout` > `split` > Click on the split panel on the right. > `pane layout` > `select` > Scroll down and click on `pickit monitoring`.

Here's how to zoom a monitoring panel:  
- Click the `pickit monitoring panel` > Click `shift + esc`  

Repeating the same operation will shrink the zoomed window.  

<img src="../../_assets/00_panel_select.png" height=320hv>

`Fig a` Selecting pick-it monitoring panel


{% hint style="warning" %}

When streaming real-time video for an extended period, the streaming speed may degrade due to high CPU load on the TP, and other issues may occur.

{% endhint %}


<img src="../../_assets/01_panel.png" height=320hv>

`Fig b` pick-it monitoring panel

<img src="../../_assets/02_expanded.png" height=320hv>

`Fig c` zoomed monitoring panel

[__SOURCE](02_preview/2-setup/README.md)
## 2.2 Setup Window

{% hint style="warning" %}

When streaming real-time video for an extended period, the streaming speed may degrade due to high CPU load on the TP, and other issues may occur.

{% endhint %}

The procedure to enter the plugin settings screen is as follows.

- `[F2: System] - 4: Application parameter - 25: pickit`

<img src="../../_assets/03_setup_ui.png" height=330hv>  

`Fig d` Setup UI


You can perform the following additional tasks on the settings screen:  
1. You can enter the `ip` and `port` used when connecting to the pick-it processor, and enter and change the socket `timeout` value when connecting.  
2. The `Reconnect` button allows you to reconnect if the connection is lost or the `ip` or `port` has changed.
3. You can check the same values as seen in `2.1 Monitoring Panel`.
4. Click the `OK` button to save the current `ip` and `port` information to the controller.

[__SOURCE](03_operation/README.md)
# 3. Plugin details  

This section covers content applied to the pick-it plugin.  
You can check the command that sends a request to the pick-it processor and the related error code.    
Additionally, you can check the robot language functions applied to the plugin.    
Detailed information related to the pick-it processor can be found through  
the link to the pick-it official document provided on each page.  

  - [3.1. Constants used in the Pick-it processor](./1-pickit_constants/README.md)
  - [3.2. pick-it robot language function](./2-job-cmd-api/README.md)



[__SOURCE](03_operation/1-pickit_constants/README.md)
## 3.1. Constants used in the Pick-it processor

The current page is about the `commands` and `responses` requested to the pick-it processor.  
For more information, see [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface).

<img src="../../_assets/02_expanded.png" height=350hv> 

`Fig a` Zoomed pick-it monitoring panel

<br>

<div style="max-width:fit-content;">

|Property| Direction | Content|
|:---|:---|:---|
|`Command`|${cont_model} com &rightarrow; pick-it processor| Indicates a request command. |
|`Connection`|${cont_model} com &leftrightarrow; pick-it processor| Indicates the communication connection status between ${cont_model} com and pick-it processor. |
|`Payload 1`, `Payload 2`|${cont_model} com &leftarrow; pick-it processor| [Refer to pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-message) |
|`Status`|${cont_model} com &leftarrow; pick-it processor| Indicates a response to a request. |
|`X,Y,Z,RX,RY,RZ`|${cont_model} com &leftarrow; pick-it processor| Indicates the location information of the object determined by the PickIt processor. |
|`Pick ID`|${cont_model} com &leftarrow; pick-it processor| Indicates the identifier of the object to select from pick-it processor. |  
|`Remaining Object`|${cont_model} com &leftarrow; pick-it processor| If non-zero, contains the remaining number of objects that can be retrieved. |  

</div>

<br>

### 3.1.1 pick-it command constants

The following are instruction constants used when making requests to the pick-it processor.  
For more information, please refer to [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status).

<div style="max-width:fit-content;">

|Command|Value|
|:---|:---|
|`NO_COMMAND`|-1|
|`CHECK_MODE`|0|
|`SHUTDOWN_SYSTEM`|2|
|`FIND_CALIB_PLATE`|10|
|`CONFIGURE_CALIB`|11|
|`COMPUTE_CALIB`|12|
|`VALIDATE_CALIB`|13|
|`LOOK_FOR_OBJECTS`|20|
|`LOOK_FOR_OBJECTS_WITH_RETRIES`|21|
|`CAPTURE_IMAGE`|22|
|`PROCESS_IMAGE`|23|
|`NEXT_OBJECT`|30|
|`CONFIGURE`|40|
|`SET_CYLINDER_DIM`|41|
|`SAVE_ACTIVE_SETUP`|42|
|`SAVE_ACTIVE_PRODUCT`|43|
|`SAVE_SCENE`|50|
|`BUILD_BACKGROUND`|60|
|`GET_PICK_POINT_DATA`|70|

</div>

<br>

### 3.1.2 pick-it processor mode constants

For more information, please refer to [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status).

<div style="max-width:fit-content;">

|Pick-it mode|Value|
|:---|:---|
|`UNDEFINED`| -1|
|`ROBOT_MODE`|0|
|`CALIBRATION MODE`|1|
|`IDLE`|2|

</div>

<br>

### 3.1.3 pick-it response constants

For more information, please refer to [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status).

<div style="max-width:fit-content;">

|응답|값|
|:---|:---|
|`UNKNOWN_COMMAND`|-99|
|`ROBOT_MODE`|0|
|`IDLE_MODE`|1|
|`SHUTDOWN_REQUEST_ACCEPT`|5|
|`SHUTDOWN_REQUEST_REJECTED`|6|
|`FIND_CALIB_PLATE_OK`|10|
|`FIND_CALIB_PLATE_FAILED`|11|
|`CONFIGURE_CALIB_OK`|12|
|`CONFIGURE_CALIB_FAILED`|13|
|`COMPUTE_CALIB_OK`|14|
|`COMPUTE_CALIB_FAILED`|15|
|`VALIDATE_CALIB_OK`|16|
|`VALIDATE_CALIB_FAILED`|17|
|`OBJECTS_FOUND`|20|
|`NO_OBJECTS`|21|
|`NO_IMAGE_CAPTURED`|22|
|`EMPTY_ROI`|23|
|`IMAGE_CAPTURED`|26|
|`INVALID_LICENSE`|27|
|`CONFIG_OK`|40|
|`CONFIG_FAILED`|41|
|`SAVE_SNAPSHOT_OK`|50|
|`SAVE_SNAPSHOT_FAILED`|51|
|`BUILD_BKG_CLOUD_OK`|60|
|`BUILD_BKG_CLOUD_FAILED`|61|
|`GET_PICK_POINT_DATA_OK`|70|
|`GET_PICK_POINT_DATA_FAILED`|71|

</div>

[__SOURCE](03_operation/2-job-cmd-api/README.md)
## 3.2. Pick-it robot language function

The current page explains the functions of the job file for the pick-it plugin.  
As shown in `Figure a`, functional operation and status monitoring of the job file are possible at the same time.


<img src="../../_assets/01_panel.png" height=350hv> 

`Fig a` Image of the `is_running()` function is executed

<br>

### 3.2.1 pick-it f-button commands

In the screen shown in `Fig a`, you can enter commands using a click-based interface by following these steps:

1. Click `cmd.input` > check the f-button list > click `pickit`.
<img src="../../_assets/05_pickit_cmd_1.png" style="width: 400px;">  
`Fig b` pick-it f-button screen

2. Select the function you wish to enter.
<img src="../../_assets/06_pickit_cmd_2.png" style="width: 400px;">  
`Fig c` Command list screen for the pick-it plugin

3. When a function is selected, you can configure its registered parameter values.  
<img src="../../_assets/07_pickit_cmd_3.png" style="width: fit-content;">  
`Fig d` Command invocation screen for the Pick-it plugin

4. Modify the `pickit. var` part to `var` before use.  
Before modification  
<img src="../../_assets/07_pickit_cmd_4.png" style="width: fit-content;">  
After modification  
<img src="../../_assets/07_pickit_cmd_5.png" style="width: fit-content;">  

<br>

### 3.2.2 pick-it function for the command

A more detailed description of the functions used in the aforementioned pick-it command is as follows.  
Basically, the robot language functions uses an xhost-based nonblocking communication method.    
Because a communication request is made through one xhost module, the returned value is the same.    
But you can check the response status for the each command through the `Status` field in the monitoring window.  

<div style="max-width:fit-content;">

|<br>function|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>operation|<br>arguments|
|:---|:---|:---|
|`is_running`|Send a `CHECK_MODE` command to the pick-it processor.<br>Reply `ROBOT_MODE` as a normal response. |`1st`) timeout (= timelimit to request) <br>`2nd`) addr_on_timeout (= branch address for the timeout)|
|`find_cal_plate`|Send a `FIND_CALIB_PLATE` command to the pick-it processor.<br>Reply `FIND_CALIB_PLATE_OK` as a normal response.|`1st`) timeout<br>`2nd`) addr_on_timeout|
|`config_cal`|Send a `CONFIGURE_CALIB` command to the pick-it processor.<br>Reply `CONFIGURE_CALIB_OK` as a normal response.|`1st`) method(for calibaration) <br> &rightarrow; single pose) 0, multiple pose) 1<br>`2nd`) camera_mount(= position)<br>&rightarrow; on robot) 1, etc) 0 <br>`3rd`) timeout<br>`4th`) addr_on_timeout<br>|
|`compute_cal`|Send a `COMPUTE_CALIB` command to the pick-it processor.<br>Reply `COMPUTE_CALIB_OK` as a normal response.|`1st`) timeout<br>`2nd`) addr_on_timeout|
|`validate_cal`|Send a `VALIDATE_CALIB` command to the pick-it processor.<br>Reply `VALIDATE_CALIB_OK` as a normal response.|`1st`) timeout<br>`2nd`) addr_on_timeout|
|`capture_img`|Send a `CAPTURE_IMAGE` command to the pick-it processor.<br>Reply `IMAGE_CAPTURED` as a normal response.|`1st`) timeout<br>`2nd`) addr_on_timeout|
|`find_objs`|If `retries is 0`, then send `LOOK_FOR_OBJECTS` command.<br>Unless, send `LOOK_FOR_OBJECTS_WITH_RETRIES` command.<br>Reply `IMAGE_CAPTURED` as a normal response.|`1st`) retries(= retry counts)|
|`process_img`|Send a `PROCESS_IMAGE` command to the pick-it processor.| - |
|`get_next_obj`|Send a `NEXT_OBJECT` command to the pick-it processor.| - |
|`configure`|Send a `CONFIGURE` command to the pick-it processor.<br>Reply `CONFIG_OK` as a normal response.|`1st`) setup_id(1 ~ 500)<br>`2nd`) Product file No(1 ~ 500)<br>`3rd`) timeout<br>`4th`) addr_on_timeout|
|`get_result`|Waiting `OBJECT_FOUND` response from the pick-it processor.|`1st`) timeout<br>`2nd`) addr_on_timeout|
|`get_pick_point_data`|Send a `GET_PICK_POINT_DATA` command to the pick-it processor.<br>Reply `GET_PICK_POINT_DATA_OK` as a normal response.|`1st`) timeout<br>`2nd`) addr_on_timeout|

</div>

<br>

The return value of the above functions is as follows:  

<div style="max-width:fit-content;">

|Return Value|Status|Description|
|:---:|:---:|:---|
|`-1`| `error`| socket is not valid..                 |
|`-2`| `error`| socket is not connected.               |
|`-3`| `error`| data to request is none.           |
|`-4`| `error`| xhost is timeout.         |
|`-5`| `error`| responsed data is not proper to parse. |
|`-6`| `error`| socket recv error.                   |
|`-7`| `error`| exception for waiting receiving data.|
|`-8`| `error`| exception for trying request.       |
| `0`| - |`exec_mode` or `waiting` response.|
| `1`| `success`|execution success.|

</div>
