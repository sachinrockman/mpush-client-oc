### Mpush开源推送框架（OC客户端）

#### 系统结构图：

![Mpush结构图](https://github.com/mpusher/mpush-client-oc/blob/master/Mpush.png)

#### 说明
结构图分为Server、Client和Actor三部分，SDK则为Client的实现, 以下按照接收数据（1-7）和发送数据（a-d）的流程介绍。
[The structure diagram is divided into three parts: Server, Client and Actor. SDK is the realization of Client. The following is introduced according to the process of receiving data (1-7) and sending data (a-d).]
接收数据:
(Receive data:)

1. Client通过GCDAsycSocket建立并管理连接。
(Client establishes and manages connection through GCDAsycSocket)

2. 接收到的数据,经由MPDataProcesser处理有可能发生的粘包、半包情况，获得完整的包数据。
(The received data is processed by MPDataProcesser for possible sticky and semi-packet situations to obtain complete packet data.)

3. 使用MPPacketDecoder将获得的data解码为MPPacket类。
(Use MPPacketDecoder to decode the obtained data into MPPacket class.)

4. 消息调度者MPMessageDispatcher则根据MPPacket中的cmd调用相应的已注册的MessageHandler。
(The message dispatcher MPMessageDispatcher calls the corresponding registered MessageHandler according to the cmd in MPPacket)

5. MessageHandler操作对应消息的行为。
(MessageHandler operation corresponding message behavior)

6. 将消息解码为MPMessage类。
(Decode the message into MPMessage class.)

7. MPClient监听接收的消息。
(MPClient monitors received messages.)

发送数据:
(send data:)

a. Client通过GCDAsycSocket建立并管理连接。
(Client establishes and manages the connection through GCDAsycSocket.)

b. MPClient的数据操作: 连接、断开、绑定用户、解绑用户、发送数据、通过HttpProxy发送push数据。
(Data operations of MPClient: connect, disconnect, bind users, unbind users, send data, and send push data through HttpProxy.)

c. 将要发送的Message打包为MPPacket并转为data。
(Pack the Message to be sent into MPPacket and convert it to data.)

d. 通过socket发送数据。
(Send data through socket.)

#### 使用注意
1. MPConfig为配置文件。
2. iOS10以上需要打开keychain Sharing的开关 -->在xcode的Target中选中Capabilities找到keychain Sharing选项 打开开关即可。
[#### Use Note
1. MPConfig is the configuration file.
2. For iOS10 and above, you need to turn on the keychain Sharing switch --> select Capabilities in the xcode Target and find the keychain Sharing option. Turn on the switch.]
