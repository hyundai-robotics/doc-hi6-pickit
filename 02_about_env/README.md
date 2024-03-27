# 2. 환경 구성

해당 페이지는 pick-it 플러그인을 실행하는데 필요한 HW 및 SW 구성을 설명합니다.

## 2.1 하드웨어 구성

플러그인 동작에 필요한 주요 부품은 다음과 같습니다.  
`Hi6 COM`, `Hi6 TP`, `pick-it 프로세서`, `pick-it 카메라`,`HUB`  

연결은 다음과 같이 이루어집니다.

<img src="../_assets/04_hardware_net.png" width="45%">


<br>


## 2.2 플러그인 설치

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


<br>


## 2.3 네트워크 통신

Hi6 Main 과 pick-it 프로세서는 이더넷 통신 방식을 사용합니다.  
Hi6 Main 과 pick-it 프로세서의 ip 서브넷 마스크는 1대역 입니다.   
Hi6 TP 와 pick-it 카메라 의 ip 서브넷 마스크는 2대역 입니다.  

|속성|내용|
|:----|:----|
|`통신 방식`| `Ethernet` (TCP/IP) |
|`Hi6 Main` - `Pickit Processor`| 192.168.1.100 |
|`Hi6 TP` - `Pickit Processor`| 192.168.2.100 |

pick-it 카메라 설정은 하기 픽잇 공식 문서를 참조하십시오.  
링크 : [pickit web interface document](https://docs.pickit3d.com/en/latest/documentation/web-interface/index.html)