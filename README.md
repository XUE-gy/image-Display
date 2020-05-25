框架层由一个会话管理器组成，它负责创建和协调其他几个模块：
状态管理器、RTP发送器、RTP接收器、RTCP发送器、RTCP接收器。
- 状态管理器是会话的核心，它维护了会话的状态信息（目标地址列表、参与会话的发送者的信息、接收者的信息等）。
- RTP发送/接收器负责响应用户的请求，发送或者接收媒体数据。
- RTP数据管理器的维护来自各个源的RTP数据，它之前的解包器会对数据进行前面所说的分流，以区分不同数据类型和不同的源。
- RTCP发送/接收器，支撑了整个系统的后台服务，它们从网络接收其他会话成员的通告信息，
并按照RFC3550标准算法进行统计，使得用户可以进行流量与拥塞控制。




RTCP数据包格式

   该规范定义了几种RTCP数据包类型，以承载
   各种控制信息：

   SR：发送者报告，用于来自
         处于活动发送方的参与者的发送和接收统计信息

   RR：接收者报告，用于来自接受非活动发送者的参与者的接收统计信息，
   与主动发送者的SR，报告超过31个源

   SDES：源描述项，包括CNAME 

   BYE：表示参与结束

   APP：特定于应用的功能
   
   每个RTCP数据包都以类似于RTP数据
      包的固定部分开头，后跟结构化元素那可能是可变的
      长度取决于数据包类型，但必须以32位
      边界结尾。
      
      
音视频编码格式
```
    name of                              sampling              default
   encoding  sample/frame  bits/sample      rate  ms/frame  ms/packet
   __________________________________________________________________
   DVI4      sample        4                var.                   20
   G722      sample        8              16,000                   20
   G723      frame         N/A             8,000        30         30
   G726-40   sample        5               8,000                   20
   G726-32   sample        4               8,000                   20
   G726-24   sample        3               8,000                   20
   G726-16   sample        2               8,000                   20
   G728      frame         N/A             8,000       2.5         20
   G729      frame         N/A             8,000        10         20
   G729D     frame         N/A             8,000        10         20
   G729E     frame         N/A             8,000        10         20
   GSM       frame         N/A             8,000        20         20
   GSM-EFR   frame         N/A             8,000        20         20
   L8        sample        8                var.                   20
   L16       sample        16               var.                   20
   LPC       frame         N/A             8,000        20         20
   MPA       frame         N/A              var.      var.
   PCMA      sample        8                var.                   20
   PCMU      sample        8                var.                   20
   QCELP     frame         N/A             8,000        20         20
   VDVI      sample        var.             var.                   20
   ```
   
SSRC标识符：
RTCP数据包的各个字段中携带的SSRC标识符是32位随机数，
在RTP会话中必须是全局唯一的，用来标记参会者.通过ip或random不能唯一确定。
采用附录a.6算法随机生成
   
![Image text]( https://github.com/XUE-gy/image-Display/blob/master/png/%E6%9E%B6%E6%9E%84%E5%9B%BE.png)