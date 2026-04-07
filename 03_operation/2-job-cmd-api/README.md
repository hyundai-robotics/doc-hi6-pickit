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
