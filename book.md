
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - Pick-it 插件
[__SOURCE](0-about-this-manual/README.md)
# 关于手册
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全注意事项

{% include file="zh/safety-notice.md" %}
[__SOURCE](01_env/README.md)
# 1. 环境配置

此页面描述了运行 pick-it 插件所需的硬件和软件配置。

- [1.1 硬件配置](./1-hw/README.md)
- [1.2 安装](./2-sw_install/README.md)
- [1.3 网络配置](./3-network/README.md)
[__SOURCE](01_env/1-hw/README.md)
## 1.1 硬件配置

插件操作所需的主要组件是：  
`${cont_model} COM`，`${cont_model} TP`，`pick-it processor`，`pick-it camera`，`hub` 或 `router`  

<br>

### a. 在 192.168.2.XX 范围内连接时
- 192.168.2 网络范围用于 TP 和 COM 之间的通信。因此，插件无法通过 2.x 范围接收图像。
- 然而，如果绝对需要使用 2.x 范围，您仍然可以通过如下所示配置网络与 hub 来接收图像。
<img src="../../_assets/04_hardware_net.png" height=310hv>

### b. 对于其他网络范围
- 您可以使用 ${cont_model} COM 的通用 LAN 端口进行连接。
- 示例）如果视频服务器主机地址为 192.168.1.100，通信端口为 8070：

#### b-1. 配置视频服务器的网关
- 设置视频服务器的网关以匹配您要连接的控制器的 IP 地址。  
  例如）通过 LAN1 连接时，视频服务器的网关必须设置为 192.168.1.150。

{% hint style="info" %}
在 Windows 10 中配置  

1. 开始 → 查看网络连接
2. 右键单击已连接的以太网 → 属性
3. 选择 Internet 协议版本 4 (TCP/IPv4) → 属性
4. 选择“使用以下 IP 地址”
5. 输入 IP 地址 / 子网掩码 / 网关

{% endhint %}

#### b-2. TP 网络配置

- 进入工程模式（R314），然后导航到 `[F1: 服务] - 13: Teach Pendant Network ([F1: Service] - 13: Teach Pendant Network)`。确认协议并进行以下设置：

{% hint style="warning" %}

[注意] 选择以下选项以外的任何选项将更改 TP IP 地址，
导致控制器之间的通信丧失。由于现场恢复非常困难，
您必须严格按照以下说明进行配置。

- IP: 192.168.2.77  
- 子网掩码: 24  
- 网关: 192.168.2.150  

{% endhint %}

- 重启控制器

#### b-3. 修改插件 URL

- 导航到：pickit 文件夹 > ui 文件夹 > js 文件夹 > display.js  
  相应更新视频流服务 URL。

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
目前，插件仅提供给已获得使用批准的客户。<br>
联系方式：HD 现代机器人研究工程师，Donghyeong Lee (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div>

<div style="max-width:fit-content;">

```python
# 示例：主机 IP = 192.168.1.100，端口 = 8070，根据服务构建查询
var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
```
</div>

#### b-4. 安装插件  
- 请参考 [安装指南](../2-sw_install/README.md) 在控制器上安装第 3 步修改后的插件。
[__SOURCE](01_env/2-sw_install/README.md)
## 1.2 安装

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
目前，该插件仅提供给已获得使用事先批准的客户。<br>
联系方式：HD 현대 로보틱스 연구 엔지니어, 동형 이 (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div><br>

通过TP屏幕使用USB安装插件。  
详细过程如下。  

<div style="max-width:fit-content;">

|Step|Contents|
|---: |:---|
| `1` | 将pick-it插件程序保存到USB。 |
| `2` | 将USB连接到TP。 |
| `3` | 输入`[F1: 服务] - 5: 文件管理器 ([F1: Service] - 5: File manager)`，然后`USB` > `pickit`文件夹 > `复制 (copy)` |
| `4` | `MAIN`文件夹 > `apps`文件夹 > `粘贴 (paste)` |
| `5` | 重启${cont_model} COM |
| `6` | `[F2: 系统] - 4: 应用参数 - 25: pickit ([F2: System] - 4: Application parameter - 25: pickit)` |

</div>
[__SOURCE](01_env/3-network/README.md)
## 1.3 网络配置

${cont_model} 主处理器和 pick-it 处理器使用以太网通信方法。  
${cont_model} 主处理器和 pick-it 处理器的 IP 子网掩码是 1 带。  
${cont_model} TP 和 pick-it 相机的 IP 子网掩码是双带。    
有关更多详细信息，请参阅 [pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)。

<div style="max-width:fit-content;">

|Property|Contents|
|:----|:----|
|`连接类型 (Connection Type)`| `TCP/IP Socket` |
|` (Port)`| 5001(TCP) |
|`字节顺序`| 网络顺序 (大端) |

</div>

要设置 pick-it 相机，您可以使用 pick-it 网络界面。  
请参阅 [pick-it 的官方文档](https://docs.pickit3d.com/zh/latest/documentation/web-interface/index.html)。
[__SOURCE](02_preview/README.md)
# 2. 预览

On this page, we will look at two representative UIs that can be seen when using the pick-it plugin.  

- [2.1 监控面板](./1-panel/README.md)
- [2.2 设置窗口](./2-setup/README.md)
[__SOURCE](02_preview/1-panel/README.md)
## 2.1 监控面板

它与现有的TP用户界面功能兼容，因此您可以使用窗口分屏、缩放功能等。  
您可以通过监控面板实时检查pick-it机器人语言功能操作的结果。  
在 `Request to Pickit` 字段中确认Pickit处理器请求的命令和属性值。  
在 `Response from Pickit` 字段中，您可以检查响应的状态和附加信息。

以下是如何拆分窗口：  
- `窗口调整 (pane layout)` > `拆分 (split)` > 点击右侧的拆分面板。 > `窗口调整 (pane layout)` > `选择 (select)` > 向下滚动并点击 `pickit monitoring`。

以下是如何缩放监控面板：  
- 点击 `pickit monitoring panel` > 点击 `shift + esc`  

重复相同的操作将缩小缩放窗口。  

<img src="../../_assets/00_panel_select.png" height=320hv>

`Fig a` 选择pick-it监控面板


{% hint style="warning" %}

当长时间流式传输实时视频时，由于TP的CPU负载过高，流式速度可能会下降，并可能发生其他问题。

{% endhint %}


<img src="../../_assets/01_panel.png" height=320hv>

`Fig b` pick-it监控面板

<img src="../../_assets/02_expanded.png" height=320hv>

`Fig c` 缩放的监控面板
[__SOURCE](02_preview/2-setup/README.md)
## 2.2 设置窗口

{% hint style="warning" %}

在长时间流式传输实时视频时，由于TP的高CPU负载，流媒体速度可能会下降，并可能出现其他问题。

{% endhint %}

进入插件设置屏幕的程序如下。

- `[F2: 系统] - 4: 应用参数 - 25: pickit ([F2: System] - 4: Application parameter - 25: pickit)`

<img src="../../_assets/03_setup_ui.png" height=330hv>  

`Fig d` 设置 UI


您可以在设置屏幕上执行以下附加任务：  
1. 您可以输入连接到pick-it处理器时使用的`ip`和`port`，并在连接时输入和更改socket `timeout`值。  
2. `Reconnect`按钮允许您在连接丢失或`ip`或`port`发生改变时重新连接。
3. 您可以检查与`2.1 监控面板`中看到的相同值。
4. 点击`确定 (OK)`按钮将当前的`ip`和`port`信息保存到控制器中。
[__SOURCE](03_operation/README.md)
# 3. 插件详情  

本节涵盖应用于 pick-it 插件的内容。  
您可以检查发送请求到 pick-it 处理器的命令及相关错误代码。    
此外，您还可以检查应用于插件的机器人语言功能。    
有关 pick-it 处理器的详细信息可以通过  
每个页面提供的链接访问 pick-it 官方文档。  

  - [3.1. 在 Pick-it 处理器中使用的常量](./1-pickit_constants/README.md)
  - [3.2. pick-it 机器人语言功能](./2-job-cmd-api/README.md)
[__SOURCE](03_operation/1-pickit_constants/README.md)
## 3.1. 在 Pick-it 处理器中使用的常量

当前页面介绍了请求给 Pick-it 处理器的 `commands` 和 `responses`。  
有关更多信息，请参见 [pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)。

<img src="../../_assets/02_expanded.png" height=350hv> 

`图 a` 放大后的 Pick-it 监控面板

<br>

<div style="max-width:fit-content;">

|属性| 方向 | 内容|
|:---|:---|:---|
|`指令值 (Command)`|${cont_model} com &rightarrow; pick-it processor| 表示请求命令。 |
|`连接 (Connection)`|${cont_model} com &leftrightarrow; pick-it processor| 表示 ${cont_model} com 和 Pick-it 处理器之间的通信连接状态。 |
|`Payload 1`, `Payload 2`|${cont_model} com &leftarrow; pick-it processor| [参见 pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#response-message) |
|`状态 (Status)`|${cont_model} com &leftarrow; pick-it processor| 表示对请求的响应。 |
|`X,Y,Z,RX,RY,RZ`|${cont_model} com &leftarrow; pick-it processor| 表示 PickIt 处理器确定的物体位置信息。 |
|`Pick ID`|${cont_model} com &leftarrow; pick-it processor| 表示从 Pick-it 处理器中选择的物体标识符。 |  
|`剩余物体 (Remaining Object)`|${cont_model} com &leftarrow; pick-it processor| 如果不为零，包含可检索的剩余物体数量。 |  

</div>

<br>

### 3.1.1 Pick-it 命令常量

以下是请求 Pick-it 处理器时使用的指令常量。  
有关更多信息，请参见 [pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#response-status)。

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
|`SAVE_ACTIVE_SETUP`|42|
|`SAVE_ACTIVE_PRODUCT`|43|
|`SAVE_SCENE`|50|
|`BUILD_BACKGROUND`|60|
|`GET_PICK_POINT_DATA`|70|

</div>

<br>

### 3.1.2 Pick-it 处理器模式常量

有关更多信息，请参见 [pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#response-status)。

<div style="max-width:fit-content;">

|Pick-it 模式|值|
|:---|:---|
|`UNDEFINED`| -1|
|`ROBOT_MODE`|0|
|`CALIBRATION MODE`|1|
|`空闲 (IDLE)`|2|

</div>

<br>

### 3.1.3 Pick-it 响应常量

有关更多信息，请参见 [pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#response-status)。

<div style="max-width:fit-content;">

|响应|值|
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
## 3.2. Pick-it 机器人语言功能

当前页面解释了 pick-it 插件的工作文件的功能。  
如 `图 a` 所示，可以同时进行工作文件的功能操作和状态监控。

<img src="../../_assets/01_panel.png" height=350hv> 

`图 a` 执行 `is_running()` 函数的图像

<br>

### 3.2.1 pick-it f-button 命令

在 `图 a` 中显示的屏幕上，可以通过以下步骤使用基于点击的接口输入命令：

1. 点击 `指令输入 (cmd.input)` > 检查 f-button 列表 > 点击 `pickit`。
<img src="../../_assets/05_pickit_cmd_1.png" style="width: 400px;">  
`图 b` pick-it f-button 屏幕

2. 选择您希望输入的功能。
<img src="../../_assets/06_pickit_cmd_2.png" style="width: 400px;">  
`图 c` pick-it 插件的命令列表屏幕

3. 选择功能后，可以配置其注册的参数值。  
<img src="../../_assets/07_pickit_cmd_3.png" style="width: fit-content;">  
`图 d` Pick-it 插件的命令调用屏幕

4. 在使用之前，将 `pickit. var` 部分修改为 `var`。  
修改前  
<img src="../../_assets/07_pickit_cmd_4.png" style="width: fit-content;">  
修改后  
<img src="../../_assets/07_pickit_cmd_5.png" style="width: fit-content;">  

<br>

### 3.2.2 pick-it 命令的功能
#### 1. 发送到 Pick-it 处理器的命令列表 (= Pick-it API)
这在 UI 屏幕的向 Pick-it 请求的信息下显示为请求的命令。

<div style="width:630px;">

<table>
  <tbody>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>process_img</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">描述</td>
      <td>将 <code>PROCESS_IMAGE</code> 命令发送到 Pick-it 处理器。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td>无</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>1</code>：发送成功<br><code>-1</code>：发送数据有问题<br><code>-2</code>：套接字未连接<br><code>-3</code>：发送失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get next object</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>NEXT_OBJECT</code> 命令发送到 Pick-it 处理器。<br>您可以随后调用 <code>get_result()</code> 来接收物体检测结果。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code> (= 时间限制)<br><code>addr_on_timeout</code> (= 超时时的分支地址，如 99, 错误)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>1</code>：发送成功<br><code>-1</code>：发送数据有问题<br><code>-2</code>：套接字未连接<br><code>-3</code>：发送失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>configure</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CONFIGURE</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>40(CONFIG_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>setup_id</code>(1~500)<br><code>product_id</code>(1~500)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>40</code>：CONFIG_OK<br><code>41</code>：CONFIG_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>is running</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CHECK_MODE</code> 命令发送到 Pick-it 处理器。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>0</code>：ROBOT_MODE<br><code>1</code>：IDLE_MODE<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find calib plate</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>FIND_CALIB_PLATE</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>10(FIND_CALIB_PLATE_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>10</code>：FIND_CALIB_OK<br><code>11</code>：FIND_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>config calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CONFIGURE_CALIB</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>12(CONFIGURE_CALIB_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>method</code>(0: 单位姿，1: 多个姿势)<br><code>camera_mount</code>(1: 机器人安装，0: 其他)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>12</code>：CONFIGURE_CALIB_OK<br><code>13</code>：CONFIGURE_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败<br><code>-6</code>: <code>method</code> 或 <code>camera_mount</code> 缺失</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>compute calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>COMPUTE_CALIB</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>14(COMPUTE_CALIB_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>14</code>：COMPUTE_CALIB_OK<br><code>15</code>：COMPUTE_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>validate calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>VALIDATE_CALIB</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>16(VALIDATE_CALIB_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>16</code>：VALIDATE_CALIB_OK<br><code>17</code>：VALIDATE_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find objects</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>如果重试为 0，则发送 <code>LOOK_FOR_OBJECTS</code>，否则发送 <code>LOOK_FOR_OBJECTS_WITH_RETRIES</code>。<br>您可以随后调用 <code>get_result()</code> 来接收物体检测结果。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>retries</code> (= 重试次数)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>1</code>：发送成功<br><code>-1</code>：数据类型无效<br><code>-2</code>：套接字连接失败<br><code>3</code>：发送失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>capture image</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CAPTURE_IMAGE</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>IMAGE_CAPTURED</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>26</code>：IMAGE_CAPTURED<br><code>22</code>：NO_IMAGE_CAPTURED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get pick point</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>GET_PICK_POINT_DATA</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>GET_PICK_POINT_DATA_OK</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>70</code>：GET_PICK_POINT_DATA_OK<br><code>71</code>：GET_PICK_POINT_DATA_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get result</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>等待来自 Pick-it 处理器的 <code>OBJECT_FOUND</code> 响应。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>20</code>：OBJECT_FOUND<br><code>21</code>：NO_OBJECTS<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>save_snapshot</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>SAVE_SNAPSHOT</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>50(SAVE_SNAPSHOT_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>subfoler</code>(1~255)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>50</code>：SAVE_SNAPSHOT_OK<br><code>51</code>：SAVE_SNAPSHOT_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-5</code>：请求失败</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 2. 发送到 ${cont_model} COM 的命令列表

<div style="max-width:630px;">
<table>
    <tbody>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>debug on</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">描述</td>
        <td>在进入 TP > <code>pane layout</code> > <code>history</code> 时打印与 pick-it 通信状态相关的日志。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>无</td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>debug off</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>在进入 TP > <code>pane layout</code> > <code>history</code> 时关闭与 pick-it 通信状态相关的日志。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>无</td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick pose</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>将当前设置的拾取姿态值作为字符串返回。可以转换为 <code>Pose()</code>。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>姿态字符串<br>例如：<code>'[574.500, 0.0, 931.000, 0.0, 90.00, 0.000, "base", "auto"]'</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick offset</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>返回当前设置的拾取偏移值。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>数字字符串<br>例如：<code>"0"</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick id</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>返回当前设置的拾取 ID 值。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>整数<br>例如：<code>0</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>reconnect</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>尝试重新建立以太网连接。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>重试次数</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td><code>1</code>: 套接字打开 & 连接成功<br><code>-1</code>: 套接字打开失败<br><code>-2</code>: 套接字连接失败</td>
      </tr>
    </tbody>
</table>

</div>