---
layout: post
title: How msg send
author: Kujisa
categories: Other
tags: Other
---

## 消息如何发送和接收

### 用户端消息处理

#### 1. 用户输入消息并点击发送
    ```java
    String userId; // 用户id
    String friendId; // 好友id
    String msgText; // 消息内容
    Integer msgType; // 消息类型（0文字消息、1固定表情）
    java.util.Date msgDate; // 消息时间
    ```

#### 2. 渲染对话框
    消息会通过`org.itstack.naive.chat.ui.view.chat.ChatController`渲染
    该方法会将消息添加到对话框

#### 3. 发送消息
    消息接着会被传入到`org.itstack.naive.chat.client.event.ChatEvent`中的`doSendMsg`方法中
    该方法会先判断消息是好友类型（1v1）还是群组类型（1vn），然后将消息序列化为`org.itstack.naive.chat.protocol.msg.MsgRequest`对象,紧接着调用netty中的`writeAndFlush`方法，将消息数据写入并推送到通道channel中

### 服务端消息处理
#### 4. 写入数据库
    在服务器的netty的通道中收到了这个消息会调用`org.itstack.naive.chat.socket.handler.MsgHandler`中的`channelRead`方法将这条消息异步写入数据库

#### 5. 添加对话框
    如果对方没有你的对话框则添加。
    通过`org.itstack.naive.chat.domain.user.service.UserServiceImpl`方法在对方的消息列表中添加对话框
    
    // 所有的聊天数据都是存在服务端数据库的，所以即使好友没有登录也可以先把对话框添加到消息列表

#### 6. 获取好友的通信管道
    如果没有获取到则返回用户未登录的提示

#### . 如果用户已登录则发送消息
    将消息序列化为`org.itstack.naive.chat.protocol.msg.MsgResponse`对象
    然后通过调用netty服务写入并推送消息到好友的通信管道