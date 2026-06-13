
[__SOURCE](README.md)
# ${cont_model} 제어기 기능설명서 - 픽잇 플러그인

[__SOURCE](0-about-this-manual/README.md)
# 이 설명서에 대하여


[__SOURCE](0-about-this-manual/precautions.md)
# 사전 주의사항

{% include file="ko/precautions.md" %}

[__SOURCE](0-about-this-manual/safety-notice.md)
# 안전 주의 사항

{% include file="ko/safety-notice.md" %}

[__SOURCE](01_env/README.md)
# 1. 환경 구성

해당 페이지는 pick-it 플러그인을 실행하는데 필요한 HW 및 SW 구성을 설명합니다.

- [1.1 하드웨어 구성](./1-hw/README.md)
- [1.2 플러그인 설치](./2-sw_install/README.md)
- [1.3 네트워크 통신](./3-network/README.md)
[__SOURCE](01_env/1-hw/README.md)
## 1.1 하드웨어 구성

플러그인 동작에 필요한 주요 부품은 다음과 같습니다.  
`${cont_model} COM`, `${cont_model} TP`, `pick-it 프로세서`, `pick-it 카메라`,`허브` 또는 `라우터`  

### a. 192.168.2.XX 대역으로 연결하는 경우  

- 192.168.2 대역은, TP 와 COM 통신에 활용되므로 플러그인에서 2대역을 통해 이미지를 받아올 수 없습니다.
- 그럼에도 불구하고 2대역을 활용해야만 하는 경우, 허브를 활용해 아래와 같이 네트워크를 구성하여 2대역을 통해 이미지를 받아올 수 있습니다.
<img src="../../_assets/04_hardware_net.png" height=310hv>

### b. 그 외 대역의 경우

- ${cont_model} COM 의 범용 LAN 포트를 활용하여 연결할 수 있습니다.
- 예제) 영상 서버 호스트 주소가 192.168.1.100 이고, 통신 포트가 8070 인 경우

#### b-1. 영상 서버의 게이트웨이 설정

- 스트리밍을 하는 영상 서버의 게이트웨이를 연결하고자하는 제어기 ip 와 일치시킵니다.  
  ex) LAN1 에 연결하는 경우, 영상 서버의 게이트웨이 설정은 192.168.1.150 이어야합니다.

{% hint style="info" %}

Windows 10 에서 네트워크 게이트웨이 설정하는 방법

1. 시작 → 네트워크 연결 보기
2. 연결된 이더넷 우클릭 → 속성
3. 인터넷 프로토콜 버전4 (TCP/IPv4) 선택 → 속성
4. 다음 IP 주소 사용(S) 선택
5. IP 주소 / 서브넷 마스크 / 게이트웨이 입력

{% endhint %}


#### b-2. TP 의 네트워크 설정

- 엔지니어 모드(R314) 진입 후 `[F1: 서비스] - 13: 티치펜던트 네트워크` 메뉴에서 동의 여부를 확인한 뒤, 하기 내용에 따라 설정 진행

{% hint style="warning" %}

[주의] 하기 옵션 외 다른 설정을 선택하면 TP의 IP 주소가 변경되어 
제어기 간 통신이 불능 상태에 빠집니다. 현장에서 원상 복구가 매우 어렵기 때문에 
반드시 아래 지침과 동일하게 설정을 진행해야 합니다.

- IP: 192.168.2.77
- 서브넷마스트: 24
- 게이트웨이: 192.168.2.150

{% endhint %}

- 제어기 재부팅 진행  

#### b-3. 플러그인 쪽 url 수정

- pickit 폴더 > ui 폴더 > js 폴더 > display.js 에서 요청하는 영상 스트리밍 서비스 url 수정

    <div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
    현재 <strong>사전 협의</strong>를 통해 사용 허가를 받은 고객에 대해서만 플러그인을 제공하고 있습니다.<br>
    문의 : HD현대로보틱스 이동형 연구원 (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
    </div>  

    <div style="max-width:fit-content;">

    ```python 
    # host ip: 192.168.1.100, port: 8070 이고 서비스에 맞게 쿼리 구성
    var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
    ```
    </div>


#### b-4. 플러그인 설치

- [설치 페이지](../2-sw_install/README.md)를 참조하여 3에서 수정한 플러그인을 제어기에 설치

[__SOURCE](01_env/2-sw_install/README.md)
## 1.2 플러그인 설치

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
현재 <strong>사전 협의</strong>를 통해 사용 허가를 받은 고객에 대해서만 플러그인을 제공하고 있습니다.<br>
문의 : HD현대로보틱스 이동형 연구원 (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div><br>

USB를 사용하여 TP 화면을 통해 플러그인 설치를 진행합니다.  



<div style="max-width:fit-content;">

|Step|내용|
|:---: |:---|
| `1` | pick-it 플러그인 프로그램을 USB 에 저장합니다.  |
| `2` | USB 를 TP에 연결합니다. |
| `3` | `[F1: 서비스] - 5: 파일 관리` 진입 후 `USB` > `pickit 폴더` > `복사` |
| `4` | `MAIN` > `apps` > `붙여넣기` |
| `5` | `제어기 재부팅` |
| `6` | `[F2: 시스템] - 4: 응용 파라미터 - 픽잇` |

</div>

[__SOURCE](01_env/3-network/README.md)
## 1.3 네트워크 통신

${cont_model} Main 과 pick-it 프로세서는 이더넷 통신 방식을 사용합니다.  
${cont_model} Main 과 pick-it 프로세서의 ip 서브넷 마스크는 1대역 입니다.   
${cont_model} TP 와 pick-it 카메라 의 ip 서브넷 마스크는 2대역 입니다.  
그 외 상세 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)를 참조하십시오.  

<div style="max-width:fit-content;">

|속성|내용|
|:----|:----|
|`연결 유형`| `TCP/IP 소켓` |
|`포트`| 5001(TCP) |
|`바이트 순서`| 네트워크 순서 (big endian) |

</div>

pick-it 카메라 설정은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/documentation/web-interface/index.html)를 참조하십시오.  
[__SOURCE](02_preview/README.md)
# 2. 미리보기

해당 페이지에서는 pick-it 플러그인을 실행할 때 볼 수 있는 대표적인 2가지 UI를 살펴봅니다.  

- [2.1 창 분할 모니터링 화면](./1-panel/README.md)
- [2.2 설정 화면](./2-setup/README.md)
[__SOURCE](02_preview/1-panel/README.md)
## 2.1 창 분할 모니터링 화면

기존 TP UI 기능과 호환되므로, 창 분할 화면, 확대 기능 등을 활용할 수 있습니다.  
pick-it 로봇 언어 함수 동작에 따른 결과를 실시간으로 창 분할 화면을 통해 확인할 수 있습니다.  
`Request to Pickit` 창에서는 pick-it 프로세서에 요청되는 명령어와 특성 값이 확인됩니다.  
`Response from Pickit` 창에서는 돌아오는 응답 상태와 추가 정보들이 확인됩니다.  

창 분할 방법은 다음과 같습니다.  
- `창조정` 클릭 > `분할` 클릭 > 우측 분할 창 클릭 > `창조정` 클릭 > `선택` 클릭 > 스크롤 후 `픽잇 모니터링` 더블 클릭  

분할된 창을 확대하는 방법은 다음과 같습니다.  
- `픽잇 모니터링 창`이 활성화(클릭된 상태)가 된 것을 확인 > `shift + esc` 버튼 클릭  

동일한 동작을 반복하면 확대된 창이 축소 됩니다.  

<img src="../../_assets/00_panel_select.png" height=320hv>

`Fig a` 패널 선택 메뉴 화면

{% hint style="warning" %}  

장시간 동안 실시간 영상 스트리밍 시 TP 의 cpu 부하로 인해 스트리밍 속도가 저하되는 등의 문제가 발생할 수 있습니다.

{% endhint %}

<img src="../../_assets/01_panel.png" height=320hv>

`Fig b` 창 분할 시 출력되는 화면


<img src="../../_assets/02_expanded.png" height=320hv>

`Fig c` 분할된 화면을 확대했을 때의 화면

[__SOURCE](02_preview/2-setup/README.md)
## 2.2 설정 화면  

{% hint style="warning" %}  

장시간 동안 실시간 영상 스트리밍 시 TP 의 cpu 부하로 인해 스트리밍 속도가 저하되는 등의 문제가 발생할 수 있습니다.

{% endhint %}

<img src="../../_assets/03_setup_ui.png" height=330hv>  

`Fig d` 설정 화면 UI

설정화면에서는 다음 추가 작업들을 할 수 있습니다.  
1. pick-it 프로세서 연결에 사용된 `ip` 와 `port`를 입력하고 연결 시 소켓 `타임아웃` 값을 입력 및 변경할 수 있습니다.
2. `Reconnect` 버튼을 통해, 연결이 끊겼거나, `ip`, `port`가 변경됐을 때 재연결을 할 수 있습니다.
3. `2.1 창 분할 모니터링 화면` 에서 확인되는 수치들을 동일하게 확인할 수 있습니다.
4. `확인` 버튼을 통해 현재 `ip`, `port` 정보를 제어기에 저장합니다.  


[__SOURCE](03_operation/README.md)
# 3. 플러그인 관련

해당 섹션에서는 pick-it 플러그인에 적용된 내용들을 다룹니다.  
pick-it 프로세서에 요청을 보내는 명령어와 관련 에러코드를 확인할 수 있습니다.  
추가로 플러그인에 적용되는 로봇 언어 함수들이 확인 가능합니다.  
pick-it 프로세서와 연관된 자세한 내용은 페이지 별로 안내된 pick-it 공식문서 링크로 확인 가능합니다.

  - [3.1. pick-it 프로세서에서 사용되는 상수](./1-pickit_constants/README.md)
  - [3.2. pick-it 로봇 언어 함수](./2-job-cmd-api/README.md)



[__SOURCE](03_operation/1-pickit_constants/README.md)
## 3.1. pick-it 프로세서에서 사용되는 상수

현재 페이지는 pick-it 프로세서에 요청하는 명령어와 응답 내용에 대한 것입니다.  
자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)를 참조하십시오.  

<img src="../../_assets/02_expanded.png" height=350hv> 

`Fig a` 모니터링 용 창분할 화면을 확대한 경우

<br>

<div style="max-width:fit-content;">

|속성|방향|내용|
|:---|:---|:---|
|`요청한 명령`|${cont_model} com &rightarrow; pick-it processor|요청 명령어를 나타냅니다. |
|`연결상태`|${cont_model} com &leftrightarrow; pick-it processor|${cont_model} com 과 pick-it processor 의 통신 연결 상태를 나타냅니다. |
|`페이로드 1`, `페이로드 2`|${cont_model} com &leftarrow; pick-it processor| 요청시 전달하는 [pickit 명령 요청 인자.](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-message) |
|`응답`|${cont_model} com &leftarrow; pick-it processor| 요청에 대한 응답을 나타냅니다. |
|`X,Y,Z,RX,RY,RZ`|${cont_model} com &leftarrow; pick-it processor| pick-it processor 가 판단한 사물의 위치 정보를 나타냅니다. |
|`Pick ID`|${cont_model} com &leftarrow; pick-it processor| 피킹 대상이 되는 사물의 식별자를 나타냅니다. |  
|`Remaining Object`|${cont_model} com &leftarrow; pick-it processor| 0이 아닌 경우 검색 가능한 나머지 개체 수가 포함됩니다. |  

</div>

<br><br>

### 3.1.1 pick-it 명령어 상수

다음은 pick-it 프로세서에 요청 시 사용되는 명령어 상수들입니다.  
`픽잇으로 요청한 정보`의 `요청한 명령`에 표시되는 명령어들입니다.  
자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)를 참조하십시오. 

<div style="max-width:fit-content;">

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

</div>

<br><br>

### 3.1.2 pick-it 프로세서 상태 상수

자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)를 참조하십시오. 

<div style="max-width:fit-content;">

|pick-it 프로세서 상태|값|
|:---|:---|
|`UNDEFINED`| -1|
|`ROBOT_MODE`|0|
|`CALIBRATION MODE`|1|
|`IDLE`|2|

</div>

<br><br>

### 3.1.3 pick-it 응답 상수
`픽잇이 응답한 정보`의 `요청한 명령`에 표시되는 명령어들입니다.  
자세한 내용은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/robots/robot-brands/socket_communication.html#response-status)를 참조하십시오. 

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
## 3.2. pick-it 로봇 언어 함수

현재 페이지에서는 ${cont_model} TP 에서 호출되는 pick-it 플러그인 용 job 파일의 함수들을 설명합니다.  
`Fig a` 처럼 job 파일에서 pick-it 플러그인 용 함수들을 동작시키면서 상태 모니터링이 가능합니다.  


<img src="../../_assets/01_panel.png" height=350hv> 

`Fig a` pick-it 플러그인 용 `get_result()` 함수 호출 중인 장면


<br><br>

### 3.2.1 pick-it 로봇 명령어 사용

`Fig a` 화면에서 다음 순서로 클릭 기반의 명령어 입력이 가능합니다.  

1. `명령입력` > `f-버튼` 리스트 확인 > `pickit` 클릭  
<img src="../../_assets/05_pickit_cmd_1.png" height=90hv> 

    `Fig b` pick-it f-버튼 화면

2. 입력하려는 함수 선택  
<img src="../../_assets/06_pickit_cmd_2.png" height=92hv> 

    `Fig c` pick-it 플러그인 용 명령어 리스트 화면

3. 함수 선택 시 등록된 인자 값을 설정할 수 있습니다.  
<img src="../../_assets/07_pickit_cmd_3.png" height=350hv>   

    `Fig d` pick-it 플러그인 용 명령어 호출 화면  

4. `pickit. var` 이라는 부분을 `var` 로 수정해서 사용합니다.   
<img src="../../_assets/07_pickit_cmd_4.png" height=60hv>   
수정 후   
<img src="../../_assets/07_pickit_cmd_5.png" height=62.3hv>    
   

<br><br>

### 3.2.2 pick-it 로봇 명령어 리스트
---- 
#### 1. pick-it 프로세서에 요청하는 명령어 리스트 (= pickit API)
UI 화면의 `픽잇으로 요청한 정보`에서 `요청한 명령` 에 표시가 됩니다.

<div style="width:630px;">

<table>
  <tbody>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>process_img</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">설명</td>
      <td>픽잇 프로세서에 <code>PROCESS_IMAGE</code> 명령을 보냅니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>1</code>: 송신 성공<br><code>-1</code>: 보내는 데이터에 문제가 있음<br><code>-2</code>: 소켓이 연결되지 않음<br><code>-3</code>: 송신 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get next object</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>NEXT_OBJECT</code> 명령을 보냅니다.<br><code>get_result()</code>를 이어서 호출하여 object 찾기 결과를 받아올 수 있습니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code>(= 제한시간)<br><code>addr_on_timeout</code>(= 타임아웃 시 분기 주소, ex. 99, error)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>1</code>: 송신 성공<br><code>-1</code>: 보내는 데이터에 문제가 있음<br><code>-2</code>: 소켓이 연결되지 않음<br><code>-3</code>: 송신 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>configure</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>CONFIGURE</code> 명령을 보냅니다. 정상 응답 시 <code>40(CONFIG_OK)</code>을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>setup_id</code>(1~500)<br><code>product_id</code>(1~500)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>40</code>: CONFIG_OK<br><code>41</code>: CONFIG_FAILED<br><code>0</code>: 응답 대기중<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>is running</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>CHECK_MODE</code> 명령을 보냅니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>0</code>: ROBOT_MODE<br><code>1</code>: IDLE_MODE<br><code>0</code>: 응답 대기중<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find calib plate</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>FIND_CALIB_PLATE</code> 명령을 보냅니다. 정상 응답 시 <code>10(FIND_CALIB_PLATE_OK)</code>을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>10</code>: FIND_CALIB_OK<br><code>11</code>: FIND_CALIB_FAILED<br><code>0</code>: 응답 대기중<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>config calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>CONFIGURE_CALIB</code> 명령을 보냅니다. 정상 응답 시 <code>12(CONFIGURE_CALIB_OK)</code>을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>method</code>(0: 싱글포즈, 1: 멀티포즈)<br><code>camera_mount</code>(1: 로봇 부착, 0: 그 외)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>12</code>: CONFIGURE_CALIB_OK<br><code>13</code>: CONFIGURE_CALIB_FAILED<br><code>0</code>: 응답 대기<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패<br><code>-6</code>: <code>method</code> 또는 <code>camera_mount</code> 미입력</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>compute calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>COMPUTE_CALIB</code> 명령을 보냅니다. 정상 응답 시 <code>14(COMPUTE_CALIB_OK)</code>을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>14</code>: COMPUTE_CALIB_OK<br><code>15</code>: COMPUTE_CALIB_FAILED<br><code>0</code>: 응답 대기<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>validate calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>VALIDATE_CALIB</code> 명령을 보냅니다. 정상 응답 시 <code>16(VALIDATE_CALIB_OK)</code>을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>16</code>: VALIDATE_CALIB_OK<br><code>17</code>: VALIDATE_CALIB_FAILED<br><code>0</code>: 응답 대기<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find objects</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>retries가 0일 때는 <code>LOOK_FOR_OBJECTS</code>를 보내고, 0 아닐 때는 <code>LOOK_FOR_OBJECTS_WITH_RETRIES</code>을 보냅니다.<br><code>get_result()</code>를 이어서 호출하여 object 찾기 결과를 받아올 수 있습니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>retries</code>(= 반복 횟수)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>1</code>: 송신 성공<br><code>-1</code>: 유효하지 않은 데이터 타입<br><code>-2</code>: 소켓 연결 실패<br><code>3</code>: 송신 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>capture image</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>CAPTURE_IMAGE</code> 명령을 보냅니다. 정상 응답 시 <code>IMAGE_CAPTURED</code>를 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>26</code>: IMAGE_CAPTURED<br><code>22</code>: NO_IMAGE_CAPTURED<br><code>0</code>: 응답 대기<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get pick point</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>GET_PICK_POINT_DATA</code> 명령을 보냅니다. 정상 응답 시 <code>GET_PICK_POINT_DATA_OK</code>를 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>70</code>: GET_PICK_POINT_DATA_OK<br><code>71</code>: GET_PICK_POINT_DATA_FAILED<br><code>0</code>: 응답 대기<br><code>-2</code>: 소켓 에러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-4</code>: 타임아웃<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get result</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서로부터 <code>OBJECT_FOUND</code> 응답을 기다립니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>20</code>: OBJECT_FOUND<br><code>21</code>: NO_OBJECTS<br><code>0</code>: 응답 대기 중<br><code>-2</code>: 소켓 애러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-5</code>: 요청 실패</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>save_snapshot</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>픽잇 프로세서에 <code>SAVE_SNAPSHOT</code> 명령을 보냅니다. 정상 응답 시 <code>50(SAVE_SNAPSHOT_OK)</code>을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td><code>subfoler</code>(1~255)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>50</code>: SAVE_SNAPSHOT_OK<br><code>51</code>: SAVE_SNAPSHOT_FAILED<br><code>0</code>: 응답 대기 중<br><code>-2</code>: 소켓 애러<br><code>-3</code>: 보낼 데이터가 없음<br><code>-5</code>: 요청 실패</td>
    </tr>
  </tbody>
</table>

</div>

---- 

#### 2. ${cont_model} COM 에 요청하는 명령어 리스트 

<div style="width:630px;">

<table>
  <tbody>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
        <code>debug on</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">설명</td>
      <td>TP > <code>창조정</code> > <code>히스토리</code> 진입 시 pick-it 통신 상태와 관련된 로그를 출력합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
        <code>debug off</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>TP > <code>창조정</code> > <code>히스토리</code> 진입 시 pick-it 통신 상태와 관련된 로그를 끕니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
        <code>get pick pose</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>현재 설정된 pick pose 값을 문자열로 반환합니다. <code>Pose()</code>로 타입 변환이 가능합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td>포즈 문자열<br>ex) <code>'[574.500, 0.0, 931.000, 0.0, 90.00, 0.000, "base", "auto"]'</code></td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
        <code>get pick offset</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>현재 설정된 pick offset 값을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td>숫자 문자열<br>ex) <code>"0"</code></td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
        <code>get pick id</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>현재 설정된 pick id 값을 반환합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>없음</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td>숫자 인트형<br>ex) <code>0</code></td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
        <code>reconnect</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">설명</td>
      <td>이더넷 연결을 재시도합니다.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">인자 값</td>
      <td>시도 횟수</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">반환 값</td>
      <td><code>1</code>: 소켓 오픈 및 연결 성공<br><code>-1</code>: 소켓 오픈 실패<br><code>-2</code>: 소켓 연결 실패</td>
    </tr>
  </tbody>
</table>

</div>
