## 3.1. Constants used in the Pick-it processor

The current page is about the `commands` and `responses` requested to the pick-it processor.  
For more information, see [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface).

<img src="../../_assets/02_expanded.png" height=350hv> 

`Fig a` Zoomed pick-it monitoring panel

<br>

|Property| Direction | Content|
|:---|:---|:---|
|`Command`|Hi6 com &rightarrow; pick-it processor| Indicates a request command. |
|`Connection`|Hi6 com &leftrightarrow; pick-it processor| Indicates the communication connection status between Hi6 com and pick-it processor. |
|`Payload 1`, `Payload 2`|Hi6 com &leftarrow; pick-it processor| [Refer to pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-message) |
|`Status`|Hi6 com &leftarrow; pick-it processor| Indicates a response to a request. |
|`X,Y,Z,RX,RY,RZ`|Hi6 com &leftarrow; pick-it processor| Indicates the location information of the object determined by the PickIt processor. |
|`Pick ID`|Hi6 com &leftarrow; pick-it processor| Indicates the identifier of the object to select from pick-it processor. |  
|`Remaining Object`|Hi6 com &leftarrow; pick-it processor| If non-zero, contains the remaining number of objects that can be retrieved. |  
  
<br>

### 3.1.1 pick-it command constants

The following are instruction constants used when making requests to the pick-it processor.  
For more information, please refer to [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status).

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

<br>

### 3.1.2 pick-it processor mode constants

For more information, please refer to [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status).

|Pick-it mode|Value|
|:---|:---|
|`UNDEFINED`| -1|
|`ROBOT_MODE`|0|
|`CALIBRATION MODE`|1|
|`IDLE`|2|

<br>

### 3.1.3 pick-it response constants

For more information, please refer to [pick-it official documentation](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status).

|Pick-it response|Value|
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
|`IMAGE_CAPTURED`             | 26|
|`INVALID_LICENSE`            | 27|
|`CONFIG_OK`                  | 40|
|`CONFIG_FAILED`              | 41|
|`GET_PICK_POINT_DATA_OK`     | 70|
|`GET_PICK_POINT_DATA_FAILED` | 71|
|`CONNECTED`                  | 98|
|`DISCONNECTED`               | 99|
|`UNKNOWN_COMMAND`            |-99|