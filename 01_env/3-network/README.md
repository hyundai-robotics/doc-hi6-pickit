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


pick-it 카메라 설정은 [pick-it 공식 문서](https://docs.pickit3d.com/en/latest/documentation/web-interface/index.html)를 참조하십시오.  