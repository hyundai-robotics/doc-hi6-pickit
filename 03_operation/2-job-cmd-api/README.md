## 3.2. pick-it robot language function

The current page explains the functions of the job file for the pick-it plugin.  
As shown in `Figure a`, functional operation and status monitoring of the job file are possible at the same time.


<img src="../../_assets/01_panel.png" height=350hv> 

`Fig a` Image of the `is_running()` function is executed

<br><br>

### 3.2.1 pick-it f-button commands

You can enter the pick-it commands as follows:    

1. Click the `cmd.input` > Check the `f-button` list > Select the `pickit`   

    <img src="../../_assets/05_pickit_cmd_1.png" height=90hv> 

    `Fig b` pick-it f-button

2. Select the command you want to enter  

    <img src="../../_assets/06_pickit_cmd_2.png" height=90hv> 

    `Fig c` commands for the pick-it plugin

3. When you select the command, registered argument values are displayed.

    <img src="../../_assets/07_pickit_cmd_3.png" height=350hv>   
    
    `Fig d` When the execute `is_running()` command.

<br><br>

### 3.2.2 pick-it function for the command

A more detailed description of the functions used in the aforementioned pick-it command is as follows.  
Basically, the robot language functions uses an xhost-based nonblocking communication method.    
Because a communication request is made through one xhost module, the returned value is the same.    
But you can check the response status for the each command through the `Status` field in the monitoring window.  

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

<br>

The return value of the above functions is as follows:  

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