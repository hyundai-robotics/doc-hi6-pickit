## 1.1 硬件配置

插件操作所需的主要组件是：  
`${cont_model} COM`，`${cont_model} TP`，`pick-it processor`，`pick-it camera`，`hub` 或 `router`  

<br>

### a. 在 192.168.2.XX 范围内连接时
- 192.168.2 网络范围用于 TP 和 COM 之间的通信。因此，插件无法通过 2.x 范围接收图像。
- 然而，如果绝对需要使用 2.x 范围，您仍然可以通过如下所示配置网络与 hub 来接收图像。
<img src="../../_assets/04_hardware_net.png" height=310hv>

### b. 对于其他网络范围
- 您可以使用 ${cont_model} COM 的通用 LAN 端口进行连接。
- 示例）如果视频服务器主机地址为 192.168.1.100，通信端口为 8070：

#### b-1. 配置视频服务器的网关
- 设置视频服务器的网关以匹配您要连接的控制器的 IP 地址。  
  例如）通过 LAN1 连接时，视频服务器的网关必须设置为 192.168.1.150。

{% hint style="info" %}
在 Windows 10 中配置  

1. 开始 → 查看网络连接
2. 右键单击已连接的以太网 → 属性
3. 选择 Internet 协议版本 4 (TCP/IPv4) → 属性
4. 选择“使用以下 IP 地址”
5. 输入 IP 地址 / 子网掩码 / 网关

{% endhint %}

#### b-2. TP 网络配置

- 进入工程模式（R314），然后导航到 `[F1: 服务] - 13: Teach Pendant Network ([F1: Service] - 13: Teach Pendant Network)`。确认协议并进行以下设置：

{% hint style="warning" %}

[注意] 选择以下选项以外的任何选项将更改 TP IP 地址，
导致控制器之间的通信丧失。由于现场恢复非常困难，
您必须严格按照以下说明进行配置。

- IP: 192.168.2.77  
- 子网掩码: 24  
- 网关: 192.168.2.150  

{% endhint %}

- 重启控制器

#### b-3. 修改插件 URL

- 导航到：pickit 文件夹 > ui 文件夹 > js 文件夹 > display.js  
  相应更新视频流服务 URL。

<div style="border:1px solid #ccc; background-color:#f9f9f9; color:#333; padding:6px 10px; border-radius:4px; max-width:fit-content; font-size:13px; line-height:1.5;">
目前，插件仅提供给已获得使用批准的客户。<br>
联系方式：HD 现代机器人研究工程师，Donghyeong Lee (<a href="mailto:donghyeong.lee@hd.com">donghyeong.lee@hd.com</a>)
</div>

<div style="max-width:fit-content;">

```python
# 示例：主机 IP = 192.168.1.100，端口 = 8070，根据服务构建查询
var url = "http://192.168.1.100:8070/stream?topic=/pickit/viewer/image_out"
```
</div>

#### b-4. 安装插件  
- 请参考 [安装指南](../2-sw_install/README.md) 在控制器上安装第 3 步修改后的插件。