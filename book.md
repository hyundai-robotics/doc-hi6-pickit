
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - Pick-it 插件
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](01_env/README.md)
# 1. 环境配置

此页面描述了运行 pick-it 插件所需的硬件和软件配置。

- [1.1 硬件配置](./1-hw/README.md)
- [1.2 安装](./2-sw_install/README.md)
- [1.3 网络配置](./3-network/README.md)
[__SOURCE](01_env/1-hw/README.md)
## 1.1 硬件配置

插件操作所需的主要组件包括：  
`${cont_model} COM`、`${cont_model} TP`、`pick-it 处理器`、`pick-it 相机`、`集线器` 或 `路由器`  

<br>

### a. 在 192.168.2.XX 范围内连接时
- 192.168.2 网络范围用于 TP 和 COM 之间的通信。因此，插件无法通过 2.x 范围接收图像。  
- 然而，如果绝对需要使用 2.x 范围，可以通过如下所示的配置使用集线器来接收图像。  
<img src="../../_assets/04_hardware_net.png" height=310hv>

### b. 对于其他网络范围
- 可以使用 ${cont_model} COM 的通用 LAN 端口进行连接。
- 示例) 如果视频服务器主机地址是 192.168.1.100，通信端口是 8070：
#### b-1. 配置视频服务器的网关
- 将视频服务器的网关设置为与您要连接的控制器的 IP 地址匹配。  
  例如) 通过 LAN1 连接时，视频服务器的网关必须设置为 192.168.1.150。

    {% hint style="info" %}
    在 Windows 10 中配置时  

    1. 开始 → 查看网络连接
    2. 右键单击已连接的以太网 → 属性
    3. 选择互联网协议版本 4 (TCP/IPv4) → 属性
    4. 选择"使用下面的 IP 地址"
    5. 输入 IP 地址 / 子网掩码 / 网关

    {% endhint %}

#### b-2. TP 网络配置

- TP > 进入管理员模式 (R314) > 服务 > 13: 教学挂件网络 > 确认协议 > 按照以下设置进行操作：

    {% hint style="warning" %}
    [注意] 选择以下选项之外的任何选项将更改 TP IP 地址， 
    导致控制器之间的通信丢失。由于现场恢复非常困难， 
    您必须严格按照以下指示进行配置。  

    - IP: 192.168.2.77  
    - 子网掩码: 24  
    - 网关: 192.168.2.150  
    {% endhint %}

- 重启控制器



#### b-3. 修改插件 URL

- 导航到：pickit 文件夹 > ui 文件夹 > js 文件夹 > display.js  
  相应地更新视频流服务 URL。

    <div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
    目前，该插件仅提供给已获得使用批准的客户。<br>
    联系人：现代重工机器人研究工程师，李东亨 (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
    </div><br>

    <div style="max-width:fit-content;">

    ```python
    # 示例：主机 IP = 192.168.1.100，端口 = 8070，按照服务构造查询
    var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
    ```
    </div>

#### b-4. 安装插件  
- 参考 [安装指南](../2-sw_install/README.md) 在控制器上安装第 3 步中的修改插件。

[__SOURCE](01_env/2-sw_install/README.md)
## 1.2 安装

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
目前，插件仅提供给已获得使用许可的客户。<br>
联系方式：现代重工机器人研究工程师，李东亨 (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div><br>

请通过TP屏幕使用USB安装插件。  
详细过程如下。

<div style="max-width:fit-content;">

|步骤|内容|
|---: |:---|
| `翻译 (1)` | 将pick-it插件程序保存到USB。 |
| `翻译 (2)` | 将USB连接到TP。 |
| `翻译 (3)` | `服务 (Service)` > `5: 文件管理器 (5: File manager)` > `USB` > `pickit`文件夹 > `复制 (copy)` |
| ` (4)` | `MAIN`文件夹 > `apps`文件夹 > `粘贴 (paste)` |
| ` (5)` | 重启${cont_model} COM |
| ` (6)` | `系统 (system)` > `4: 应用参数 (4: Application parameter)` > `25: pickit` |

</div>
[__SOURCE](01_env/3-network/README.md)
## 1.3 网络配置

${cont_model} 主处理器和 pick-it 处理器使用以太网通信方法。  
${cont_model} 主处理器和 pick-it 处理器的 IP 子网掩码为 1 段。  
${cont_model} TP 和 pick-it 相机的 IP 子网掩码为两段。  
有关更多详细信息，请参阅 [pick-it 官方文档](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)。

<div style="max-width:fit-content;">

|属性|内容|
|:----|:----|
|`连接类型 (Connection Type)`| `TCP/IP Socket` |
|`端口 (Port)`| 5001(TCP) |
|`字节顺序`| 网络顺序（大端） |

</div>

对于 pick-it 相机设置，您可以使用 pick-it 网络界面。  
请参阅 [pick-it 的官方文档](https://docs.pickit3d.com/en/latest/documentation/web-interface/index.html)。
[__SOURCE](02_preview/README.md)
# 2. 预览

在此页面上，我们将查看使用 pick-it 插件时可以看到的两个代表性用户界面。  

- [2.1 监控面板](./1-panel/README.md)
- [2.2 设置窗口](./2-setup/README.md)
[__SOURCE](02_preview/1-panel/README.md)
## 2.1 监控面板

它与现有的TP UI功能兼容，因此您可以利用窗口分屏、缩放功能等。  
您可以通过监控面板实时检查pick-it机器人语言功能操作的结果。  
在`Request to Pickit`字段中确认Pickit处理器请求的命令和属性值。  
在`Response from Pickit`字段中，您可以检查响应状态和附加信息。

以下是如何分割窗口：  
- `窗格布局 (pane layout)` > `分割 (split)` > 点击右侧的分割面板。 > `窗格布局 (pane layout)` > `选择 (select)` > 向下滚动并点击`pickit monitoring`。

以下是如何缩放监控面板：  
- 点击`pickit monitoring panel` > 点击`shift + esc`  

重复相同的操作将缩小缩放的窗口。  

<img src="../../_assets/00_panel_select.png" height=320hv>

`Fig a` 选择pick-it监控面板

{% hint style="warning" %}

长时间进行实时视频流传输时，由于 TP 的 CPU 负载较高，可能会导致流传输速度下降等问题。

{% endhint %}

<img src="../../_assets/01_panel.png" height=320hv>

`Fig b` pick-it监控面板

<img src="../../_assets/02_expanded.png" height=320hv>

`Fig c` 放大的监控面板

[__SOURCE](02_preview/2-setup/README.md)
## 2.2 设置窗口

{% hint style="warning" %}

长时间进行实时视频流传输时，由于 TP 的 CPU 负载较高，可能会导致流传输速度下降等问题。

{% endhint %}

进入插件设置屏幕的过程如下。

- `系统 (System)` > `4: 应用参数 (4: Application parameter)` > `25: pickit` >

<img src="../../_assets/03_setup_ui.png" height=330hv>  

`Fig d` 设置 UI


您可以在设置屏幕上执行以下附加任务：  
1. 您可以输入连接到 pick-it 处理器时使用的 `ip` 和 `port`，并在连接时输入和更改插座的 `timeout` 值。  
2. `Reconnect` 按钮允许您在连接丢失或 `ip` 或 `port` 更改时重新连接。
3. 您可以查看与 `2.1 监控面板` 中看到的相同的值。
4. 单击 `确认 (OK)` 按钮将当前的 `ip` 和 `port` 信息保存到控制器中。

[__SOURCE](03_operation/README.md)
# 3. 插件详情  

本节涵盖应用于 pick-it 插件的内容。  
您可以检查发送请求到 pick-it 处理器的命令及相关错误代码。  
此外，您还可以检查应用于该插件的机器人语言功能。  
与 pick-it 处理器相关的详细信息可以通过  
每个页面提供的 pick-it 官方文档链接找到。  

  - [3.1. 在 Pick-it 处理器中使用的常量](./1-pickit_constants/README.md)
  - [3.2. pick-it 机器人语言功能](./2-job-cmd-api/README.md)
[__SOURCE](03_operation/1-pickit_constants/README.md)
## 3.1. 在 Pick-it 处理器中使用的常量

当前页面关于请求 Pick-it 处理器的 `commands` 和 `responses`。  
有关更多信息，请参阅 [pick-it 官方文档](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)。

<img src="../../_assets/02_expanded.png" height=350hv> 

`图 a` 放大 Pick-it 监控面板

<br>

<div style="max-width:fit-content;">

|属性| 方向 | 内容|
|:---|:---|:---|
|`命令 (Command)`|${cont_model} com &rightarrow; pick-it processor| 表示请求命令。 |
|`连接 (Connection)`|${cont_model} com &leftrightarrow; pick-it processor| 表示 ${cont_model} com 和 Pick-it 处理器之间的通信连接状态。 |
|`有效载荷 1`, `有效载荷 2`|${cont_model} com &leftarrow; pick-it processor| [参见 pick-it 官方文档](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-message) |
|`状态 (Status)`|${cont_model} com &leftarrow; pick-it processor| 表示对请求的响应。 |
|`X,Y,Z,RX,RY,RZ`|${cont_model} com &leftarrow; pick-it processor| 表示 PickIt 处理器确定的物体位置信息。 |
|`选择 ID`|${cont_model} com &leftarrow; pick-it processor| 表示从 Pick-it 处理器选择的物体的标识符。 |  
|`剩余物体`|${cont_model} com &leftarrow; pick-it processor| 如果不为零，则包含可检索的剩余物体数量。 |  

</div>

<br>

### 3.1.1 pick-it 命令常量

以下是请求 Pick-it 处理器时使用的指令常量。  
有关更多信息，请参阅 [pick-it 官方文档](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)。

<div style="max-width:fit-content;">

|命令|值|
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
<<<SOURCE_MARKDOWN_START>>>|`SAVE_ACTIVE_SETUP`|42|
|`SAVE_ACTIVE_PRODUCT`|43|
|`SAVE_SCENE`|50|
|`BUILD_BACKGROUND`|60|
|`GET_PICK_POINT_DATA`|70|

</div>

<br>

### 3.1.2 pick-it 处理器模式常量

有关更多信息，请参见 [pick-it 官方文档](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)。

<div style="max-width:fit-content;">

|Pick-it 模式|值|
|:---|:---|
|`UNDEFINED`| -1|
|`ROBOT_MODE`|0|
|`CALIBRATION MODE`|1|
|`空闲 (IDLE)`|2|

</div>

<br>

### 3.1.3 pick-it 响应常量

有关更多信息，请参见 [pick-it 官方文档](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)。

<div style="max-width:fit-content;">

|Pick-it 响应|值|
|:---|:---|
|`ROBOT_MODE`                 |  0|
|`IDLE_MODE`                  |  1|
|`FIND_CALIB_PLATE_OK`        | 10|
|`FIND_CALIB_PLATE_FAILED`    | 11|
|`CONFIGURE_CALIB_OK`         | 12|
|`CONFIGURE_CALIB_FAILED`     | 13|
|`COMPUTE_CALIB_OK`           | 14|
|`COMPUTE_CALIB_FAILED`       | 15|
|`VALIDATE_CALIB_OK`          | 16|
|`VALIDATE_CALIB_FAILED`      | 17|
|`OBJECTS_FOUND`              | 20|
|`NO_OBJECTS`                 | 21|
|`NO_IMAGE_CAPTURED`          | 22|
|`EMPTY_ROI`                  | 23|
|`IMAGE_CAPTURED`             | 26|<<<SOURCE_MARKDOWN_END>>>
|`INVALID_LICENSE`            | 27|
|`CONFIG_OK`                  | 40|
|`CONFIG_FAILED`              | 41|
|`GET_PICK_POINT_DATA_OK`     | 70|
|`GET_PICK_POINT_DATA_FAILED` | 71|
|`CONNECTED`                  | 98|
|`DISCONNECTED`               | 99|
|`UNKNOWN_COMMAND`            |-99|

</div>
[__SOURCE](03_operation/2-job-cmd-api/README.md)
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