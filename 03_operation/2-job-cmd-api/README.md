## 3.2. Pick-it 机器人语言功能

当前页面解释了 pick-it 插件的工作文件的功能。  
如 `图 a` 所示，可以同时进行工作文件的功能操作和状态监控。

<img src="../../_assets/01_panel.png" height=350hv> 

`图 a` 执行 `is_running()` 函数的图像

<br>

### 3.2.1 pick-it f-button 命令

在 `图 a` 中显示的屏幕上，可以通过以下步骤使用基于点击的接口输入命令：

1. 点击 `指令输入 (cmd.input)` > 检查 f-button 列表 > 点击 `pickit`。
<img src="../../_assets/05_pickit_cmd_1.png" style="width: 400px;">  
`图 b` pick-it f-button 屏幕

2. 选择您希望输入的功能。
<img src="../../_assets/06_pickit_cmd_2.png" style="width: 400px;">  
`图 c` pick-it 插件的命令列表屏幕

3. 选择功能后，可以配置其注册的参数值。  
<img src="../../_assets/07_pickit_cmd_3.png" style="width: fit-content;">  
`图 d` Pick-it 插件的命令调用屏幕

4. 在使用之前，将 `pickit. var` 部分修改为 `var`。  
修改前  
<img src="../../_assets/07_pickit_cmd_4.png" style="width: fit-content;">  
修改后  
<img src="../../_assets/07_pickit_cmd_5.png" style="width: fit-content;">  

<br>

### 3.2.2 pick-it 命令的功能
#### 1. 发送到 Pick-it 处理器的命令列表 (= Pick-it API)
这在 UI 屏幕的向 Pick-it 请求的信息下显示为请求的命令。

<div style="width:630px;">

<table>
  <tbody>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>process_img</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">描述</td>
      <td>将 <code>PROCESS_IMAGE</code> 命令发送到 Pick-it 处理器。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td>无</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>1</code>：发送成功<br><code>-1</code>：发送数据有问题<br><code>-2</code>：套接字未连接<br><code>-3</code>：发送失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get next object</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>NEXT_OBJECT</code> 命令发送到 Pick-it 处理器。<br>您可以随后调用 <code>get_result()</code> 来接收物体检测结果。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code> (= 时间限制)<br><code>addr_on_timeout</code> (= 超时时的分支地址，如 99, 错误)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>1</code>：发送成功<br><code>-1</code>：发送数据有问题<br><code>-2</code>：套接字未连接<br><code>-3</code>：发送失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>configure</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CONFIGURE</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>40(CONFIG_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>setup_id</code>(1~500)<br><code>product_id</code>(1~500)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>40</code>：CONFIG_OK<br><code>41</code>：CONFIG_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>is running</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CHECK_MODE</code> 命令发送到 Pick-it 处理器。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>0</code>：ROBOT_MODE<br><code>1</code>：IDLE_MODE<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find calib plate</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>FIND_CALIB_PLATE</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>10(FIND_CALIB_PLATE_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>10</code>：FIND_CALIB_OK<br><code>11</code>：FIND_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>config calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CONFIGURE_CALIB</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>12(CONFIGURE_CALIB_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>method</code>(0: 单位姿，1: 多个姿势)<br><code>camera_mount</code>(1: 机器人安装，0: 其他)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>12</code>：CONFIGURE_CALIB_OK<br><code>13</code>：CONFIGURE_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败<br><code>-6</code>: <code>method</code> 或 <code>camera_mount</code> 缺失</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>compute calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>COMPUTE_CALIB</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>14(COMPUTE_CALIB_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>14</code>：COMPUTE_CALIB_OK<br><code>15</code>：COMPUTE_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>validate calibration</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>VALIDATE_CALIB</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>16(VALIDATE_CALIB_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>16</code>：VALIDATE_CALIB_OK<br><code>17</code>：VALIDATE_CALIB_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>find objects</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>如果重试为 0，则发送 <code>LOOK_FOR_OBJECTS</code>，否则发送 <code>LOOK_FOR_OBJECTS_WITH_RETRIES</code>。<br>您可以随后调用 <code>get_result()</code> 来接收物体检测结果。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>retries</code> (= 重试次数)</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>1</code>：发送成功<br><code>-1</code>：数据类型无效<br><code>-2</code>：套接字连接失败<br><code>3</code>：发送失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>capture image</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>CAPTURE_IMAGE</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>IMAGE_CAPTURED</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>26</code>：IMAGE_CAPTURED<br><code>22</code>：NO_IMAGE_CAPTURED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get pick point</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>GET_PICK_POINT_DATA</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>GET_PICK_POINT_DATA_OK</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>70</code>：GET_PICK_POINT_DATA_OK<br><code>71</code>：GET_PICK_POINT_DATA_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-4</code>：超时<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>get result</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>等待来自 Pick-it 处理器的 <code>OBJECT_FOUND</code> 响应。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>20</code>：OBJECT_FOUND<br><code>21</code>：NO_OBJECTS<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-5</code>：请求失败</td>
    </tr>
    <tr>
      <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
         <code>save_snapshot</code>
      </th>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
      <td>将 <code>SAVE_SNAPSHOT</code> 命令发送到 Pick-it 处理器。成功响应时返回 <code>50(SAVE_SNAPSHOT_OK)</code>。</td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
      <td><code>subfoler</code>(1~255)<br><code>timeout</code><br><code>addr_on_timeout</code></td>
    </tr>
    <tr>
      <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
      <td><code>50</code>：SAVE_SNAPSHOT_OK<br><code>51</code>：SAVE_SNAPSHOT_FAILED<br><code>0</code>：等待响应<br><code>-2</code>：套接字错误<br><code>-3</code>：无数据发送<br><code>-5</code>：请求失败</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 2. 发送到 ${cont_model} COM 的命令列表

<div style="max-width:630px;">
<table>
    <tbody>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>debug on</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center; width: 120px;">描述</td>
        <td>在进入 TP > <code>pane layout</code> > <code>history</code> 时打印与 pick-it 通信状态相关的日志。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>无</td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>debug off</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>在进入 TP > <code>pane layout</code> > <code>history</code> 时关闭与 pick-it 通信状态相关的日志。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>无</td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick pose</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>将当前设置的拾取姿态值作为字符串返回。可以转换为 <code>Pose()</code>。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>姿态字符串<br>例如：<code>'[574.500, 0.0, 931.000, 0.0, 90.00, 0.000, "base", "auto"]'</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick offset</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>返回当前设置的拾取偏移值。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>数字字符串<br>例如：<code>"0"</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>get pick id</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>返回当前设置的拾取 ID 值。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>无</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td>整数<br>例如：<code>0</code></td>
      </tr>
      <tr>
        <th colspan="2" style="background-color: #f1f5f9; text-align: left; padding: 10px; border-top: 3px solid #cbd5e1;">
          <code>reconnect</code>
        </th>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">描述</td>
        <td>尝试重新建立以太网连接。</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">参数</td>
        <td>重试次数</td>
      </tr>
      <tr>
        <td style="white-space: nowrap; font-weight: bold; background-color: #f8fafc; text-align: center;">返回值</td>
        <td><code>1</code>: 套接字打开 & 连接成功<br><code>-1</code>: 套接字打开失败<br><code>-2</code>: 套接字连接失败</td>
      </tr>
    </tbody>
</table>

</div>