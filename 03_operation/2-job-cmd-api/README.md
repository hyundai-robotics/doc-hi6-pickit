## 3.2. Pick-it robot language function

The current page explains the functions of the job file for the pick-it plugin.  
As shown in `Figure a`, functional operation and status monitoring of the job file are possible at the same time.


<img src="../../_assets/01_panel.png" height=350hv> 

`Fig a` Image of the `is_running()` function is executed

<br>

### 3.2.1 pick-it f-button commands

In the screen shown in `Fig a`, you can enter commands using a click-based interface by following these steps:

1. Click `cmd.input` > check the f-button list > click `pickit`.
<img src="../../_assets/05_pickit_cmd_1.png" style="width: 400px;">  
`Fig b` pick-it f-button screen

2. Select the function you wish to enter.
<img src="../../_assets/06_pickit_cmd_2.png" style="width: 400px;">  
`Fig c` Command list screen for the pick-it plugin

3. When a function is selected, you can configure its registered parameter values.  
<img src="../../_assets/07_pickit_cmd_3.png" style="width: fit-content;">  
`Fig d` Command invocation screen for the Pick-it plugin

4. Modify the `pickit. var` part to `var` before use.  
Before modification  
<img src="../../_assets/07_pickit_cmd_4.png" style="width: fit-content;">  
After modification  
<img src="../../_assets/07_pickit_cmd_5.png" style="width: fit-content;">  

<br>

### 3.2.2 pick-it function for the command
#### 1. List of commands sent to the Pick-it processor (= Pick-it API)
This is displayed in Requested command under Information requested to Pick-it on the UI screen.

<div style="width:630px;">

<table>
  <tbody>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>process_img</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">Description</td>
      <td>Sends the <code>PROCESS_IMAGE</code> command to the Pick-it processor.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td>None</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>1</code>: Send success<br><code>-1</code>: Problem with the sent data<br><code>-2</code>: Socket not connected<br><code>-3</code>: Send failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get next object</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>NEXT_OBJECT</code> command to the Pick-it processor.<br>You can subsequently call <code>get_result()</code> to receive the object detection result.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code> (= Time limit)<br><code>addr_on_timeout</code> (= Branch address on timeout, ex. 99, error)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>1</code>: Send success<br><code>-1</code>: Problem with the sent data<br><code>-2</code>: Socket not connected<br><code>-3</code>: Send failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>configure</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>CONFIGURE</code> command to the Pick-it processor. Returns <code>40(CONFIG_OK)</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>setup_id</code>(1~500)<br><code>product_id</code>(1~500)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>40</code>: CONFIG_OK<br><code>41</code>: CONFIG_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>is running</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>CHECK_MODE</code> command to the Pick-it processor.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>0</code>: ROBOT_MODE<br><code>1</code>: IDLE_MODE<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find calib plate</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>FIND_CALIB_PLATE</code> command to the Pick-it processor. Returns <code>10(FIND_CALIB_PLATE_OK)</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>10</code>: FIND_CALIB_OK<br><code>11</code>: FIND_CALIB_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>config calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>CONFIGURE_CALIB</code> command to the Pick-it processor. Returns <code>12(CONFIGURE_CALIB_OK)</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>method</code>(0: Single pose, 1: Multi pose)<br><code>camera_mount</code>(1: Robot-mounted, 0: Others)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>12</code>: CONFIGURE_CALIB_OK<br><code>13</code>: CONFIGURE_CALIB_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed<br><code>-6</code>: <code>method</code> or <code>camera_mount</code> missing</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>compute calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>COMPUTE_CALIB</code> command to the Pick-it processor. Returns <code>14(COMPUTE_CALIB_OK)</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>14</code>: COMPUTE_CALIB_OK<br><code>15</code>: COMPUTE_CALIB_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>validate calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>VALIDATE_CALIB</code> command to the Pick-it processor. Returns <code>16(VALIDATE_CALIB_OK)</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>16</code>: VALIDATE_CALIB_OK<br><code>17</code>: VALIDATE_CALIB_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find objects</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends <code>LOOK_FOR_OBJECTS</code> if retries is 0, otherwise sends <code>LOOK_FOR_OBJECTS_WITH_RETRIES</code>.<br>You can subsequently call <code>get_result()</code> to receive the object detection result.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>retries</code> (= Number of retries)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>1</code>: Send success<br><code>-1</code>: Invalid data type<br><code>-2</code>: Socket connection failed<br><code>3</code>: Send failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>capture image</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>CAPTURE_IMAGE</code> command to the Pick-it processor. Returns <code>IMAGE_CAPTURED</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>26</code>: IMAGE_CAPTURED<br><code>22</code>: NO_IMAGE_CAPTURED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get pick point</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>GET_PICK_POINT_DATA</code> command to the Pick-it processor. Returns <code>GET_PICK_POINT_DATA_OK</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>70</code>: GET_PICK_POINT_DATA_OK<br><code>71</code>: GET_PICK_POINT_DATA_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-4</code>: Timeout<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get result</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Waits for the <code>OBJECT_FOUND</code> response from the Pick-it processor.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>20</code>: OBJECT_FOUND<br><code>21</code>: NO_OBJECTS<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-5</code>: Request failed</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>save_snapshot</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
      <td>Sends the <code>SAVE_SNAPSHOT</code> command to the Pick-it processor. Returns <code>50(SAVE_SNAPSHOT_OK)</code> upon successful response.</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
      <td><code>subfoler</code>(1~255)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
      <td><code>50</code>: SAVE_SNAPSHOT_OK<br><code>51</code>: SAVE_SNAPSHOT_FAILED<br><code>0</code>: Waiting for response<br><code>-2</code>: Socket error<br><code>-3</code>: No data to send<br><code>-5</code>: Request failed</td>
    </tr>
  </tbody>
</table>

</div>

<br>

#### 2. List of commands sent to ${cont_model} COM

<div style="max-width:630px;">
<table>
    <tbody>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>debug on</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">Description</td>
        <td>Prints logs related to the pick-it communication status when entering TP > <code>pane layout</code> > <code>history</code>.</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
        <td>None</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
        <td>None</td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>debug off</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
        <td>Turns off logs related to the pick-it communication status when entering TP > <code>pane layout</code> > <code>history</code>.</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
        <td>None</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
        <td>None</td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick pose</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
        <td>Returns the currently set pick pose value as a string. It can be type-cast to <code>Pose()</code>.</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
        <td>None</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
        <td>Pose string<br>ex) <code>'[574.500, 0.0, 931.000, 0.0, 90.00, 0.000, "base", "auto"]'</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick offset</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
        <td>Returns the currently set pick offset value.</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
        <td>None</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
        <td>Number string<br>ex) <code>"0"</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick id</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
        <td>Returns the currently set pick id value.</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
        <td>None</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
        <td>Integer<br>ex) <code>0</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>reconnect</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Description</td>
        <td>Retries the Ethernet connection.</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Arguments</td>
        <td>Number of retries</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">Return Value</td>
        <td><code>1</code>: Socket open & connection success<br><code>-1</code>: Socket open failed<br><code>-2</code>: Socket connection failed</td>
      </tr>
    </tbody>
</table>

</div>
