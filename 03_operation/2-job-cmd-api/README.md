## 3.2. Pick-it 机器人语言功能

当前页面解释了 pick-it 插件的作业文件功能。  
如 `图 a` 所示，可以同时进行作业文件的功能操作和状态监控。

<img src="../../_assets/01_panel.png" height=350hv> 

`图 a` `is_running()` 功能执行的图像

<br><br>

### 3.2.1 pick-it f-button 命令

您可以按如下方式输入 pick-it 命令：

1. 点击 `命令输入 (cmd.input)` > 检查 `f-button` 列表 > 选择 `pickit`   

    <img src="../../_assets/05_pickit_cmd_1.png" height=90hv> 

    `图 b` pick-it f-button

2. 选择您想要输入的命令  

    <img src="../../_assets/06_pickit_cmd_2.png" height=90hv> 

    `图 c` pick-it 插件的命令

3. 当您选择命令时，将显示注册的参数值。

    <img src="../../_assets/07_pickit_cmd_3.png" height=350hv>   
    
    `图 d` 执行 `is_running()` 命令时。

<br><br>

### 3.2.2 针对命令的 pick-it 功能

上述 pick-it 命令中使用的功能的更详细描述如下。  
基本上，机器人语言功能使用基于 xhost 的非阻塞通信方法。    
由于通过一个 xhost 模块发出通信请求，返回值是相同的。    
但是，您可以通过监控窗口中的 `状态 (Status)` 字段检查每个命令的响应状态。  

<div style="max-width:fit-content;">

|<br>功能|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>操作|<br>参数|
|:---|:---|:---|
|`is_running`|向 pick-it 处理器发送 `CHECK_MODE` 命令。<br>正常响应为 `ROBOT_MODE`。 |`1st`) 超时 (= 请求的时间限制) <br>`2nd`) 超时的地址 (= 超时的分支地址)|
|`find_cal_plate`|向 pick-it 处理器发送 `FIND_CALIB_PLATE` 命令。<br>正常响应为 `FIND_CALIB_PLATE_OK`。|`1st`) 超时<br>`2nd`) 超时的地址|
|`config_cal`|向 pick-it 处理器发送 `CONFIGURE_CALIB` 命令。<br>正常响应为 `CONFIGURE_CALIB_OK`。|`1st`) 方法（用于校准） <br> &rightarrow; 单一姿势) 0, 多重姿势) 1<br>`2nd`) camera_mount（= 位置）<br>&rightarrow; 机器人上) 1，等等) 0 <br>`3rd`) 超时<br>`4th`) 超时的地址<br>|
|`compute_cal`|向 pick-it 处理器发送 `COMPUTE_CALIB` 命令。<br>回复 `COMPUTE_CALIB_OK` 作为正常响应。|`1st`) 超时<br>`2nd`) 超时地址|
|`validate_cal`|向 pick-it 处理器发送 `VALIDATE_CALIB` 命令。<br>回复 `VALIDATE_CALIB_OK` 作为正常响应。|`1st`) 超时<br>`2nd`) 超时地址|
|`capture_img`|向 pick-it 处理器发送 `CAPTURE_IMAGE` 命令。<br>回复 `IMAGE_CAPTURED` 作为正常响应。|`1st`) 超时<br>`2nd`) 超时地址|
|`find_objs`|如果 `retries is 0`，则发送 `LOOK_FOR_OBJECTS` 命令。<br>否则，发送 `LOOK_FOR_OBJECTS_WITH_RETRIES` 命令。<br>回复 `IMAGE_CAPTURED` 作为正常响应。|`1st`) 重试次数|
|`process_img`|向 pick-it 处理器发送 `PROCESS_IMAGE` 命令。| - |
|`get_next_obj`|向 pick-it 处理器发送 `NEXT_OBJECT` 命令。| - |
|`configure`|向 pick-it 处理器发送 `CONFIGURE` 命令。<br>回复 `CONFIG_OK` 作为正常响应。|`1st`) setup_id(1 ~ 500)<br>`2nd`) 产品文件编号(1 ~ 500)<br>`3rd`) 超时<br>`4th`) 超时地址|
|`get_result`|等待来自 pick-it 处理器的 `OBJECT_FOUND` 响应。|`1st`) 超时<br>`2nd`) 超时地址|
|`get_pick_point_data`|向 pick-it 处理器发送 `GET_PICK_POINT_DATA` 命令。<br>回复 `GET_PICK_POINT_DATA_OK` 作为正常响应。|`1st`) 超时<br>`2nd`) 超时地址|

</div>

<br>

上述函数的返回值如下：  

<div style="max-width:fit-content;">

|返回值|状态|描述|
|:---:|:---:|:---|
|`-1`| `错误`| 套接字无效..                 |
|`-2`| `错误`| 套接字未连接。               |
|`-3`| `错误`| 没有请求数据。           |
|`-4`| `错误`| xhost 超时。         |
|`-5`| `错误`| 响应数据无法解析。 |
|`-6`| `错误`| 套接字接收错误。                   |
|`-7`| `错误`| 等待接收数据时出现异常。|
|`-8`| `错误`| 尝试请求时出现异常。       |
| `0`| - |`执行模式` 或 `等待` 响应。|
| `翻译 (1)`| `成功`|执行成功。|

</div>