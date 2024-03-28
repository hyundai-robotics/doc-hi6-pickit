# Hi6 픽잇 플러그인 설명서

{% hint style="warning" %}
본 제품 설명서에서 제공되는 정보는 현대로보틱스의 자산입니다.

현대로보틱스의 서면에 의한 동의 없이 전부 또는 일부를 무단 전재 및 재배포할 수 없으며, 제3자에게 제공되거나 다른 목적에 사용할 수 없습니다.



본 설명서는 사전 예고 없이 변경될 수 있습니다.



**Copyright ⓒ 2024 by HD Hyundai Robotics**
{% endhint %}# 1. 환경 구성

해당 페이지는 pick-it 플러그인을 실행하는데 필요한 HW 및 SW 구성을 설명합니다.

- [1.1 하드웨어 구성](./1-hw/README.md)
- [1.2 플러그인 설치](./2-sw_install/README.md)
- [1.3 네트워크 통신](./3-network/README.md)## 1.1 하드웨어 구성

플러그인 동작에 필요한 주요 부품은 다음과 같습니다.  
`Hi6 COM`, `Hi6 TP`, `pick-it 프로세서`, `pick-it 카메라`,`HUB`  

예시)

<img src="../../_assets/04_hardware_net.png" width="45%">## 1.2 플러그인 설치

USB를 사용하여 TP 화면을 통해 플러그인 설치를 진행합니다.
상세 과정은 다음과 같습니다.

|Step|내용|
|---: |:---|
| `1` | pick-it 플러그인 프로그램을 USB 에 저장합니다.  |
| `2` | USB 를 TP에 연결합니다. |
| `3` | `서비스` > `5: 파일 관리` > `USB` > `pickit 폴더` > `복사` |
| `4` | `MAIN` > `apps` > `붙여넣기` |
| `5` | `제어기 재부팅` |
| `6` | `시스템` > `5: 응용 파라미터` > `픽잇` |
## 1.3 네트워크 통신

Hi6 Main 과 pick-it 프로세서는 이더넷 통신 방식을 사용합니다.  
Hi6 Main 과 pick-it 프로세서의 ip 서브넷 마스크는 1대역 입니다.   
Hi6 TP 와 pick-it 카메라 의 ip 서브넷 마스크는 2대역 입니다.  
그 외 상세 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)를 참조하십시오.  


|속성|내용|
|:----|:----|
|`연결 유형`| `TCP/IP 소켓` |
|`포트`| 5001(TCP) |
|`바이트 순서`| 네트워크 순서 (big endian) |


pick-it 카메라 설정은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/documentation/web-interface/index.html)를 참조하십시오.  # 2. 미리보기

해당 페이지에서는 pick-it 플러그인을 실행할 때 볼 수 있는 대표적인 2가지 UI를 살펴봅니다.  

- [2.1 창 분할 모니터링 화면](./1-panel/README.md)
- [2.2 설정 화면](./2-setup/README.md)## 2.1 창 분할 모니터링 화면

기존 TP UI 기능과 호환되므로, 창 분할 화면, 확대 기능 등을 활용할 수 있습니다.  
pick-it 로봇 언어 함수 동작에 따른 결과를 실시간으로 창 분할 화면을 통해 확인할 수 있습니다.  
`Request to Pickit` 창에서는 pick-it 프로세서에 요청되는 명령어와 특성 값이 확인됩니다.  
`Response from Pickit` 창에서는 돌아오는 응답 상태와 추가 정보들이 확인됩니다.  

창 분할 방법은 다음과 같습니다.  
- `창조정` 클릭 > `분할` 클릭 > 우측 분할 창 클릭 > `창조정` 클릭 > `선택` 클릭 > 스크롤 후 `픽잇 모니터링` 더블 클릭  

분할된 창을 확대하는 방법은 다음과 같습니다.  
- `픽잇 모니터링 창`이 활성화(클릭된 상태)가 된 것을 확인 > `shift + esc` 버튼 클릭  

동일한 동작을 반복하면 확대된 창이 축소 됩니다.  

<img src = "../../_assets/00_panel_select.png" width="60%">  

`Fig a` 패널 선택 메뉴 화면

<img src = "../../_assets/01_panel.png" width="60%">  

`Fig b` 창 분할 시 출력되는 화면

<img src = "../../_assets/02_expanded.png" width="60%">  

`Fig c` 분할된 화면을 확대했을 때의 화면## 2.2 설정 화면  


<img src = "../../_assets/03_setup_ui.png" width="60%">  

`Fig d` 설정 화면 UI


설정화면에서는 다음 추가 작업들을 할 수 있습니다.  
1. pick-it 프로세서 연결에 사용된 `ip` 와 `port`를 입력하고 연결 시 소켓 `타임아웃` 값을 입력 및 변경할 수 있습니다.
2. `Reconnect` 버튼을 통해, 연결이 끊겼거나, `ip`, `port`가 변경됐을 때 재연결을 할 수 있습니다.
3. `1.1 창 분할 모니터링 화면` 에서 확인되는 수치들을 동일하게 확인할 수 있습니다.
4. `확인` 버튼을 통해 현재 `ip`, `port` 정보를 제어기에 저장합니다.  # 3. 플러그인 관련

해당 섹션에서는 pick-it 플러그인에 적용된 내용들을 다룹니다.  
pick-it 프로세서에 요청을 보내는 명령어와 관련 에러코드를 확인할 수 있습니다.  
추가로 플러그인에 적용되는 로봇 언어 함수들이 확인 가능합니다.  
pick-it 프로세서와 연관된 자세한 내용은 페이지 별로 안내된 pick-it 공식문서 링크로 확인 가능합니다.

  - [3.1. pick-it 프로세서에서 사용되는 상수](./1-pickit_constants/README.md)
  - [3.2. pick-it 로봇 언어 함수](./2-job-cmd-api/README.md)


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
|`UNKNOWN_COMMAND`            |-99|## 3.2. pick-it 로봇 언어 함수

현재 페이지에서는 Hi6 TP 에서 호출되는 pick-it 플러그인 용 job 파일의 함수들을 설명합니다.  

<img src = "../../_assets/01_panel.png" width="60%">  

`Fig a` pick-it 플러그인 용 `get_result()` 함수 호출 중인 장면

`Fig a` 처럼 job 파일에서 pick-it 플러그인 용 함수들을 동작시키면서 상태 모니터링이 가능합니다.  
사용자 

<br>

### 3.2.1 pick-it 로봇 명령어 사용

`Fig a` 화면에서 다음 순서로 클릭 기반의 명령어 입력이 가능합니다.  

1. `명령입력` > `f-버튼` 리스트 확인 > `pickit` 클릭  
<img src = "../../_assets/05_pickit_cmd_1.png" width="60%">   

    `Fig b` pick-it f-버튼

2. 입력하려는 함수 선택  
<img src = "../../_assets/06_pickit_cmd_2.png" width="60%">  
    `Fig c` pick-it 플러그인 용 명령어 리스트

3. 함수 선택 시 등록된 인자 값을 설정할 수 있습니다.  
<img src = "../../_assets/07_pickit_cmd_3.png" width="60%">  



<br>

### 3.2.2 pick-it 로봇 명령어 리스트

로봇 언어 함수는 xhost 기반의 nonblocking 통신 방식이 적용되었습니다.  
하나의 모듈을 통해 통신 요청이 이루어지므로 반환되는 값이 동일합니다.  
각 각의 명령어에 대한 응답 상태는 모니터링 창의 `Status` 칸에서 확인 가능합니다.

|함수명|인자|리턴|
|:---|:---|:---|
|`is_running`|timeout, addr_on_timeout|하기 참조|
||check pickit processor is running|하기 참조|
|`find_cal_plate`|timeout, addr_on_timeout|하기 참조|
|`config_cal`|Calibration method(Single pose: 0, Multi pose: 1), Camera mount(Fixed: 0, On-robot: 1)|하기 참조|
|`compute_cal`|timeout, addr_on_timeout|하기 참조|
|`validate_cal`|timeout, addr_on_timeout|하기 참조|
|`capture_img`|timeout, addr_on_timeout|하기 참조|
|`find_objs`|retry count(0 ~ 500), timeout, addr_on_timeout|하기 참조|
|`validate_cal`|timeout, addr_on_timeout|하기 참조|
|`get_result`|timeout, addr_on_timeout|하기 참조|
|`get_pick_point_data`|timeout, addr_on_timeout|하기 참조|
|`configure`|Setup file No(1 ~ 500), Product file No(1 ~ 500), timeout, addr_on_timeout|하기 참조|

|리턴 값|설명|
|:---|:---|
|`-1`| `error` socket is not valid.                  |
|`-2`| `error` socket is not connected.              |
|`-3`| `error` data to request is none.              |
|`-4`| `error` xhost is timeout.                     |
|`-5`| `error` responsed data is not proper to parse.|
|`-6`| `error` socket recv error.                    |
|`-7`| `error` exception for waiting receiving data. |
|`-8`| `error` exception for trying request.         |
| `0`| `exec_mode` or `waiting` response.            |
| `1`| `success` for execution.                      |