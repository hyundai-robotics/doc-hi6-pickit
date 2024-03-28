## 3.2. pick-it 로봇 언어 함수

현재 페이지에서는 Hi6 TP 에서 호출되는 pick-it 플러그인 용 job 파일의 함수들을 설명합니다.  
`Fig a` 처럼 job 파일에서 pick-it 플러그인 용 함수들을 동작시키면서 상태 모니터링이 가능합니다.  


<img src="../../_assets/01_panel.png" height=350hv> 

`Fig a` pick-it 플러그인 용 `get_result()` 함수 호출 중인 장면


<br>

### 3.2.1 pick-it 로봇 명령어 사용

`Fig a` 화면에서 다음 순서로 클릭 기반의 명령어 입력이 가능합니다.  

1. `명령입력` > `f-버튼` 리스트 확인 > `pickit` 클릭  
<img src="../../_assets/05_pickit_cmd_1.png" height=90hv> 

    `Fig b` pick-it f-버튼 화면

2. 입력하려는 함수 선택  
<img src="../../_assets/06_pickit_cmd_2.png" height=90hv> 

    `Fig c` pick-it 플러그인 용 명령어 리스트 화면

3. 함수 선택 시 등록된 인자 값을 설정할 수 있습니다.  
<img src="../../_assets/07_pickit_cmd_3.png" height=350hv>   

    `Fig d` pick-it 플러그인 용 명령어 호출 화면

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