## 3.1. pick-it 프로세서에서 사용되는 상수

현재 페이지는 pick-it 프로세서에 요청하는 명령어와 응답 내용에 대한 것입니다.  
자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)를 참조하십시오.  

<img src = "../../_assets/02_expanded.png" width="60%">  

`Fig a` 모니터링 용 창분할 화면을 확대한 경우

<br>

|속성|방향|내용|
|:---|:---|:---|
|`Command`|Hi6 com &rightarrow; pick-it processor|요청 명령어를 나타냅니다. |
|`Connection`|Hi6 com &leftrightarrow; pick-it processor|Hi6 com 과 pick-it processor 의 통신 연결 상태를 나타냅니다. |
|`Payload 1`, `Payload 2`|Hi6 com &leftarrow; pick-it processor| [pick-it 공식 문서 참조](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-message) |
|`Status`|Hi6 com &leftarrow; pick-it processor| 요청에 대한 응답을 나타냅니다. |
|`X,Y,Z,RX,RY,RZ`|Hi6 com &leftarrow; pick-it processor| pick-it processor 가 판단한 사물의 위치 정보를 나타냅니다. |
|`Pick ID`|Hi6 com &leftarrow; pick-it processor| 피킹 대상이 되는 사물의 식별자를 나타냅니다. |  
|`Remaining Object`|Hi6 com &leftarrow; pick-it processor| 0이 아닌 경우 검색 가능한 나머지 개체 수가 포함됩니다. |  
  
<br>

### 3.1.1 pick-it 명령어 상수

다음은 pick-it 프로세서에 요청 시 사용되는 명령어 상수들입니다.  
자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)를 참조하십시오. 

|명령어|값|
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

### 3.1.2 pick-it 모드 상수

자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)를 참조하십시오. 

|모드|값|
|:---|:---|
|`UNDEFINED`|-1|
|`ROBOT_MODE`|0|
|`CALIBRATION MODE`|1|
|`IDLE`|2|

<br>

### 3.1.3 pick-it 응답 상수

자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)를 참조하십시오. 

|응답|값|
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