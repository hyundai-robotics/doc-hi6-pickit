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