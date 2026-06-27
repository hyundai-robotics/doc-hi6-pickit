## 1.3 网络配置

${cont_model} 主处理器和 pick-it 处理器使用以太网通信方法。  
${cont_model} 主处理器和 pick-it 处理器的 IP 子网掩码是 1 带。  
${cont_model} TP 和 pick-it 相机的 IP 子网掩码是双带。    
有关更多详细信息，请参阅 [pick-it 官方文档](https://docs.pickit3d.com/zh/latest/robots/robot-brands/socket_communication.html#pickit-socket-interface)。

<div style="max-width:fit-content;">

|Property|Contents|
|:----|:----|
|`连接类型 (Connection Type)`| `TCP/IP Socket` |
|` (Port)`| 5001(TCP) |
|`字节顺序`| 网络顺序 (大端) |

</div>

要设置 pick-it 相机，您可以使用 pick-it 网络界面。  
请参阅 [pick-it 的官方文档](https://docs.pickit3d.com/zh/latest/documentation/web-interface/index.html)。