## 1.1 硬件配置

插件操作所需的主要组件包括：  
`${cont_model} COM`、`${cont_model} TP`、`pick-it 处理器`、`pick-it 相机`、`集线器` 或 `路由器`  

<br>

### a. 在 192.168.2.XX 范围内连接时
- 192.168.2 网络范围用于 TP 和 COM 之间的通信。因此，插件无法通过 2.x 范围接收图像。  
- 然而，如果绝对需要使用 2.x 范围，可以通过如下所示的配置使用集线器来接收图像。  
<img src="../../_assets/04_hardware_net.png" height=310hv>

### b. 对于其他网络范围
- 可以使用 ${cont_model} COM 的通用 LAN 端口进行连接。
- 示例) 如果视频服务器主机地址是 192.168.1.100，通信端口是 8070：
#### b-1. 配置视频服务器的网关
- 将视频服务器的网关设置为与您要连接的控制器的 IP 地址匹配。  
  例如) 通过 LAN1 连接时，视频服务器的网关必须设置为 192.168.1.150。

    {% hint style="info" %}
    在 Windows 10 中配置时  

    1. 开始 → 查看网络连接
    2. 右键单击已连接的以太网 → 属性
    3. 选择互联网协议版本 4 (TCP/IPv4) → 属性
    4. 选择"使用下面的 IP 地址"
    5. 输入 IP 地址 / 子网掩码 / 网关

    {% endhint %}

#### b-2. TP 网络配置

- TP > 进入管理员模式 (R314) > 服务 > 13: 教学挂件网络 > 确认协议 > 按照以下设置进行操作：

    {% hint style="warning" %}
    [注意] 选择以下选项之外的任何选项将更改 TP IP 地址， 
    导致控制器之间的通信丢失。由于现场恢复非常困难， 
    您必须严格按照以下指示进行配置。  

    - IP: 192.168.2.77  
    - 子网掩码: 24  
    - 网关: 192.168.2.150  
    {% endhint %}

- 重启控制器



#### b-3. 修改插件 URL

- 导航到：pickit 文件夹 > ui 文件夹 > js 文件夹 > display.js  
  相应地更新视频流服务 URL。

    <div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
    目前，该插件仅提供给已获得使用批准的客户。<br>
    联系人：现代重工机器人研究工程师，李东亨 (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
    </div><br>

    <div style="max-width:fit-content;">

    ```python
    # 示例：主机 IP = 192.168.1.100，端口 = 8070，按照服务构造查询
    var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
    ```
    </div>

#### b-4. 安装插件  
- 参考 [安装指南](../2-sw_install/README.md) 在控制器上安装第 3 步中的修改插件。
