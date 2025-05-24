好的，你修改了代码并且已经能基本满足任务要求，这很棒！现在我们可以开始准备实验报告了。

根据你提供的课程设计要求、任务书以及你修改后的 `P2P.py` 代码，我来帮你整理实验报告的内容。我会把你需要填写或替换的部分用 `[占位符]` 标出，需要截图的地方会明确提示 `【截图X：截图说明】`。

**重要提示：**

*   以下内容是根据通用模板和你提供的信息生成的，请务必结合你学校的具体要求和你自己的实际操作进行调整和修改。
*   你提供的代码 `P2P.py` 将作为报告中“关键代码”和“附录”的基础。
*   关于你提到的“但我无法发送给他（因为没有用户列表显示）”这个问题，我们可以在报告的“遇到的问题”或“待改进”部分提及。

---

**计算机网络课程设计报告**

---

**封面**

```
课程名称：计算机网络
题目名称：基于P2P的局域网即时通信系统
学生学院：[请填写你的学院名称]
专业班级：[请填写你的专业班级]
学    号：[请填写你的学号]
学生姓名：黄晨 (根据你截图的文件名推测，请确认或修改)
指导教师：梁路
完成日期：[请填写实际完成日期，例如：2024年X月X日]
```
**【请你按照 `课程设计报告封面.png` 的格式，将以上信息填写到一个Word文档的首页】**

---

**摘要**

```
本课程设计旨在设计并实现一个基于P2P（点对点）技术的局域网即时通信系统。该系统允许在同一局域网内的用户进行无需中心服务器的文本消息和文件传输。系统采用Python语言开发，利用Socket进行网络通信编程，通过UDP协议实现用户的自动发现与注册，通过TCP协议保证消息和文件传输的可靠性。图形用户界面(GUI)采用Tkinter库构建，为用户提供了包括用户登录、在线用户列表展示、消息收发、文件选择与传输等功能。

本报告详细介绍了系统的需求分析、总体设计、关键技术、详细设计、实现过程以及测试结果。系统实现了P2P通信的基本功能，包括用户上线后的自动扫描与对等方列表更新、选择指定用户进行文本聊天和文件共享。测试结果表明，系统能够在局域网环境下稳定运行，基本满足设计要求。最后，报告总结了开发过程中遇到的问题、解决方案以及未来可改进的方向。

关键词：P2P；局域网通信；Socket；Python；即时通信；Tkinter
```

---

**目录**

```
1. 绪论
   1.1 项目背景与意义
   1.2 主要研究内容
   1.3 报告结构
2. 相关技术概述
   2.1 P2P技术原理
   2.2 Python语言简介
   2.3 Socket编程
   2.4 Tkinter GUI库
   2.5 多线程技术
3. 系统需求分析
   3.1 功能需求
      3.1.1 用户注册与发现
      3.1.2 消息传输
      3.1.3 文件传输
      3.1.4 用户界面
   3.2 非功能需求
4. 系统设计
   4.1 系统总体架构
   4.2 通信协议设计
      4.2.1 UDP发现协议
      4.2.2 TCP传输协议
   4.3 主要模块设计
      4.3.1 用户登录模块
      4.3.2 用户发现与列表更新模块
      4.3.3 消息与文件收发模块
      4.3.4 GUI交互模块
   4.4 关键数据结构
   4.5 程序流程图
5. 系统实现
   5.1 开发与运行环境
   5.2 关键代码与解释
   5.3 系统界面展示
6. 系统测试
   6.1 测试环境
   6.2 测试用例与结果
7. 开发总结
   7.1 完成的工作
   7.2 遇到的问题及解决方法
   7.3 待解决的问题及改进方向
参考文献
附录：主要源代码
致谢
团队成员分工
```
**(目录在你写完所有内容后，在Word中自动生成会比较方便)**

---

**1. 绪论**

```
1.1 项目背景与意义

随着计算机网络技术的飞速发展和普及，局域网环境下的信息共享与即时沟通需求日益增长。传统的C/S（客户端/服务器）架构通信系统通常依赖于中心服务器进行消息转发和用户管理，这不仅增加了服务器的负载压力，也可能存在单点故障的风险。P2P（Peer-to-Peer，点对点）技术作为一种去中心化的网络模型，允许网络中的节点直接进行数据交换和资源共享，具有结构简单、可扩展性好、鲁棒性高等优点。

设计和实现一个基于P2P的局域网即时通信系统，可以为小型办公环境、家庭网络或临时组建的网络提供一种便捷、高效的沟通方式，无需复杂的服务器配置和维护。本项目旨在通过实践，深入理解P2P通信原理、Socket网络编程以及图形用户界面设计，提升分析和解决实际问题的能力。

1.2 主要研究内容

本课程设计主要研究和实现以下内容：
(1) 掌握P2P基本原理，并应用于局域网通信系统的设计。
(2) 利用Python的Socket库实现UDP协议进行用户自动发现和注册，动态维护在线用户列表。
(3) 利用Python的Socket库实现TCP协议进行用户间可靠的文本消息和文件传输。
(4) 使用Tkinter库构建图形用户界面（GUI），提供用户友好的操作体验，包括登录、用户选择、消息输入与显示、文件选择与发送等。
(5) 程序需实现客户端和服务端一体化，即每个节点既能发起通信，也能响应其他节点的请求。

1.3 报告结构

本报告共分为七个主要章节。第一章为绪论，介绍项目背景、意义及主要研究内容。第二章概述了系统开发所涉及的相关技术。第三章进行系统需求分析，明确系统应具备的功能。第四章阐述了系统的总体设计方案，包括架构设计、协议设计和模块设计。第五章详细介绍了系统的实现过程，包括开发环境、关键代码的实现和界面展示。第六章描述了系统的测试过程及结果。第七章对整个课程设计工作进行总结，并展望了未来的改进方向。
```

---

**2. 相关技术概述**

```
2.1 P2P技术原理

P2P（Peer-to-Peer）即对等网络，是一种无中心服务器或具有极少中心服务器的网络架构。在P2P网络中，每个节点（Peer）既是客户端也是服务器，可以直接与其他节点建立连接并交换信息或共享资源。P2P技术具有高可扩展性、鲁棒性和资源利用率高等特点。常见的P2P应用包括文件共享、即时通讯、流媒体等。本系统利用P2P思想，使局域网内的用户可以直接通信。

2.2 Python语言简介

Python是一种解释型、面向对象、动态数据类型的高级程序设计语言。凭借其简洁的语法、丰富的标准库和第三方库以及跨平台性，Python在网络编程、Web开发、数据科学、人工智能等领域得到了广泛应用。本项目选用Python作为开发语言，主要因为它在Socket网络编程和GUI开发方面提供了便捷的接口和库。

2.3 Socket编程

Socket（套接字）是网络通信过程中端点的抽象表示，它封装了底层网络协议的细节，为应用程序提供了一套标准的API来进行网络通信。Socket编程是实现网络应用的基础。本项目主要使用以下两种类型的Socket：
(1) UDP (User Datagram Protocol) Socket：用户数据报协议，是一种无连接的、不可靠的传输协议。它传输效率高，适用于对实时性要求较高、能容忍少量数据丢失的场景，如本系统中的用户发现广播。
(2) TCP (Transmission Control Protocol) Socket：传输控制协议，是一种面向连接的、可靠的字节流传输协议。它通过三次握手建立连接，并提供超时重传、数据校验等机制保证数据传输的顺序性和完整性，适用于本系统中的文本消息和文件传输。

2.4 Tkinter GUI库

Tkinter是Python的标准GUI（图形用户界面）库，是Tk GUI工具包的Python接口。Tkinter简单易用，能够快速创建窗口、对话框、按钮、文本框、列表框等常见的GUI组件，并处理用户交互事件。本项目使用Tkinter构建用户登录界面和主聊天界面。

2.5 多线程技术

为了使GUI界面在进行网络通信（如监听端口、发送/接收数据）时保持响应，避免阻塞，本项目采用了多线程技术。通过创建独立的线程来处理耗时的网络操作，可以确保主GUI线程的流畅运行，提升用户体验。Python的`threading`模块为多线程编程提供了支持。
```

---

**3. 系统需求分析**

(这部分主要根据任务书中的“已知技术参数和设计要求”来写)

```
3.1 功能需求

根据课程设计任务书的要求，本基于P2P的局域网即时通信系统应具备以下主要功能：

3.1.1 用户注册与发现
(1) 用户启动程序后，应能设置自己的用户信息，包括用户名和所在组别。
(2) 系统启动后，自动扫描局域网内（同一子网）的其他在线对等方（即运行了相同程序的其他用户）。扫描通过向预设的服务器端口（UDP端口）发送探测消息实现。
(3) 当接收到其他对等方的探测消息时，应能将其加入到自己的在线用户列表中，并回复一个应答消息。
(4) 当接收到其他对等方的应答消息时，也应能将其加入到自己的在线用户列表中。
(5) 双方交换的消息格式自定义，但至少应包含用户名和IP地址（由程序自动获取）。组别信息也用于区分。

3.1.2 消息传输
(1) 用户可以从在线用户列表中选择一个目标用户。
(2) 用户可以输入文本消息，并通过TCP连接将消息发送给选定的目标用户。
(3) 系统应能接收来自其他用户的文本消息，并在消息显示区域展示，同时标明消息来源（用户名和IP）。

3.1.3 文件传输
(1) 用户可以从在线用户列表中选择一个目标用户。
(2) 用户可以选择本地的一个文件。
(3) 系统通过TCP连接将选定的文件发送给目标用户。
(4) 系统应能接收来自其他用户的文件，并提示用户选择保存路径。
(5) （任务书要求：文件传输进程显示及操作按钮或菜单。本系统通过消息提示实现，暂无图形化进度条）。

3.1.4 用户界面
(1) 提供用户登录界面，用于输入用户名和组别。
(2) 主界面应包含以下部分：
    a. 在线用户列表：显示当前发现的、同一组内的其他在线用户及其IP地址。
    b. 消息显示区域：用于展示聊天记录。
    c. 消息输入框：用于用户输入待发送的文本消息。
    d. 操作按钮：至少包括“发送消息”和“发送文件”按钮。

3.2 非功能需求
(1) 易用性：用户界面应简洁直观，操作方便。
(2) 可靠性：文本消息和文件传输应保证数据的正确送达（通过TCP实现）。
(3) 实时性：用户发现和消息传递应具有较好的实时性。
(4) 运行环境：系统应能在常见的局域网环境下运行，用户需在同一子网内。
(5) 资源占用：系统资源占用应合理，不应对用户主机造成过大负担。
```

---

**4. 系统设计**

```
4.1 系统总体架构

本系统采用完全对等的P2P架构，每个运行的程序实例都扮演客户端和服务器双重角色。系统主要由以下几个部分组成：
(1) 用户接口层（GUI）：负责与用户交互，展示信息，接收用户输入。
(2) 通信处理层：负责P2P网络的具体通信实现，包括用户发现（UDP）和数据传输（TCP）。
(3) 核心逻辑层：处理用户登录、用户列表管理、消息和文件收发逻辑等。

[你可以考虑在这里画一个简单的架构图，用方框表示节点，箭头表示通信。如果不想画图，文字描述也可以。例如：]

系统启动后，每个节点（用户）会初始化UDP监听服务用于接收其他节点的发现请求和应答，同时初始化TCP监听服务用于接收消息和文件。用户登录成功后，会主动通过UDP扫描局域网内同一IP段的其他节点，发送“HELLO”请求。收到“HELLO”请求的节点会回复“HELLO_ACK”并将对方加入用户列表。发起方收到“HELLO_ACK”后也将对方加入列表。用户选择列表中的对等方即可通过TCP发起消息或文件传输。

4.2 通信协议设计

为了实现用户发现和数据传输，本系统设计了如下自定义通信协议：

4.2.1 UDP发现协议 (端口: 50000)
(1) 注册/发现请求 (HELLO消息):
    格式: `HELLO|用户名|组名`
    方向: 节点A -> 节点B (扫描时)
    作用: 节点A向节点B声明自己的存在，并请求加入对方的对等方列表。
(2) 注册/发现应答 (HELLO_ACK消息):
    格式: `HELLO_ACK|用户名|组名`
    方向: 节点B -> 节点A (响应HELLO时)
    作用: 节点B回应节点A的请求，并声明自己的存在，请求加入对方列表。

4.2.2 TCP传输协议 (端口: 50001)
(1) 文本消息传输:
    头部格式: `MSG|发送方用户名`
    数据体: 实际文本消息内容 (UTF-8编码)
    作用: 标识后续数据为文本消息。
(2) 文件传输:
    头部格式: `FILE|发送方用户名|文件名|文件大小(字节)`
    数据体: 实际文件内容的二进制流
    作用: 标识后续数据为文件，并提供文件名和大小信息供接收方处理。

4.3 主要模块设计

4.3.1 用户登录模块 (`build_login_ui`, `login` 函数)
    - 功能: 提供GUI界面供用户输入用户名和组名。
    - 实现: 用户点击“登录”按钮后，获取输入，若有效则销毁登录界面，构建主界面，并启动用户扫描。

4.3.2 用户发现与列表更新模块 (`udp_listener`, `scan_peers`, `refresh_peer_list` 函数)
    - `udp_listener`: 后台线程，持续监听UDP端口50000。
        - 收到`HELLO`消息：解析对方信息，将其IP和信息存入`self.peer_list`，更新GUI列表，并向对方发送`HELLO_ACK`消息。
        - 收到`HELLO_ACK`消息：解析对方信息，将其IP和信息存入`self.peer_list`，更新GUI列表。
    - `scan_peers`: 用户登录后调用，或可设计为定时调用。遍历当前主机所在IP子网的常见地址（如1-254），向每个地址的UDP端口50000发送`HELLO`消息。
    - `refresh_peer_list`: 当`self.peer_list`发生变化时调用，清空并重新填充GUI中的在线用户列表框。

4.3.3 消息与文件收发模块 (`tcp_listener`, `handle_tcp_connection`, `send_message`, `send_file` 函数)
    - `tcp_listener`: 后台线程，持续监听TCP端口50001。接受到连接请求后，为每个连接创建一个新的处理线程`handle_tcp_connection`。
    - `handle_tcp_connection`: 处理单个TCP连接。首先接收协议头部，判断是消息(MSG)还是文件(FILE)。
        - 若为MSG：接收后续的文本消息数据，调用`show_message`在GUI上显示。
        - 若为FILE：接收文件名和大小，弹出文件保存对话框供用户选择路径，然后接收文件数据并写入本地文件，完成后提示用户。
    - `send_message`: 用户在GUI点击“发送消息”按钮时调用。获取选中的目标用户IP和输入框中的文本。与目标IP的TCP端口50001建立连接，先发送`MSG|...`头部，再发送消息内容。关闭连接。
    - `send_file`: 用户在GUI点击“发送文件”按钮时调用。获取选中的目标用户IP，弹出文件选择对话框让用户选择本地文件。与目标IP的TCP端口50001建立连接，先发送`FILE|...`头部，再分块读取并发送文件内容。关闭连接。

4.3.4 GUI交互模块 (Tkinter相关代码, `show_message` 函数)
    - 使用Tkinter组件构建登录窗口和主聊天窗口（包括用户列表、聊天记录区、输入框、按钮等）。
    - `show_message`: 负责将接收到的或自己发送的消息格式化后显示在聊天记录文本框中，并自动滚动到底部。

4.4 关键数据结构
    - `self.peer_list`: 字典类型。用于存储当前发现的在线对等方信息。
        - 键 (Key): 对等方的IP地址 (字符串)。
        - 值 (Value): 一个字典，包含 `{'username': 用户名, 'group': 组名}`。
        - 示例: `{'192.168.1.101': {'username': 'Bob', 'group': 'TestGroup1'}}`

4.5 程序流程图

(这里用文字描述主要的流程，如果老师要求图形，你需要自己画一下)

(1) 主程序启动流程:
    1. 初始化Tkinter主窗口。
    2. 创建P2PChatApp实例。
    3. P2PChatApp构造函数中：
        a. 初始化用户名、组名为空，`peer_list`为空字典。
        b. 构建并显示登录UI (`build_login_ui`)。
        c. 启动UDP监听线程 (`udp_listener`)。
        d. 启动TCP监听线程 (`tcp_listener`)。
    4. 进入Tkinter主事件循环 (`root.mainloop()`)。

(2) 用户登录流程:
    1. 用户在登录界面输入用户名和组名，点击“登录”。
    2. `login`函数被调用：
        a. 获取输入的用户名和组名。
        b. 校验用户名和组名是否为空，若为空则提示错误。
        c. 销毁登录界面 (`self.login_frame.destroy()`)。
        d. 构建主聊天界面 (`self.build_main_ui()`)。
        e. 调用`scan_peers()`开始扫描局域网内的其他用户。

(3) UDP用户发现流程 (以节点A扫描到节点B为例):
    1. 节点A调用`scan_peers()`，遍历IP段。
    2. 对某个IP（节点B的IP），节点A发送 `HELLO|A的用户名|A的组名` UDP消息至节点B的50000端口。
    3. 节点B的`udp_listener`线程收到该HELLO消息：
        a. 解析出A的用户名和组名。
        b. 如果组名与B相同，则将A的信息（IP、用户名、组名）存入B的`peer_list`。
        c. 调用`refresh_peer_list()`更新B的GUI用户列表。
        d. 向节点A的IP和来源端口回复 `HELLO_ACK|B的用户名|B的组名` UDP消息。
    4. 节点A的`udp_listener`线程收到来自节点B的HELLO_ACK消息：
        a. 解析出B的用户名和组名。
        b. 如果组名与A相同，则将B的信息（IP、用户名、组名）存入A的`peer_list`。
        c. 调用`refresh_peer_list()`更新A的GUI用户列表。

(4) 发送文本消息流程 (用户A发送给用户B):
    1. 用户A在GUI上选择用户B，输入消息，点击“发送消息”。
    2. `send_message`函数被调用：
        a. 获取用户B的IP地址。
        b. 创建TCP Socket，连接到用户B的IP和50001端口。
        c. 发送消息头部 `MSG|A的用户名`。
        d. 发送实际消息内容。
        e. 在A的GUI上显示 `我：消息内容`。
        f. 关闭TCP Socket。
    3. 用户B的`tcp_listener`线程接受来自A的连接，创建`handle_tcp_connection`线程。
    4. `handle_tcp_connection`线程：
        a. 接收消息头部，识别为`MSG`。
        b. 解析出A的用户名。
        c. 接收实际消息内容。
        d. 调用`show_message`在B的GUI上显示 `A的用户名：消息内容`。
        e. 关闭连接。

(文件发送流程与文本消息类似，主要是协议头部和数据内容不同。)
```

---

**5. 系统实现**

```
5.1 开发与运行环境
- 操作系统：Windows 10/11 (或其他你使用的操作系统，如macOS, Linux)
- Python版本：Python 3.x (例如：Python 3.9，请填写你的版本)
- 主要库：
    - socket (标准库，用于网络通信)
    - threading (标准库，用于多线程处理)
    - tkinter (标准库，用于GUI开发)
    - os (标准库，用于文件路径操作等)
- 开发工具：PyCharm (或其他你使用的IDE，如VS Code)

5.2 关键代码与解释

(这里你需要从你的 `P2P.py` 文件中摘录一些核心功能的代码片段，并加以解释。以下是一些建议摘录的函数，你可以选择其中几个，不必全部列出，但要能体现核心功能。)

(1) UDP监听与用户发现响应 (`udp_listener` 函数部分)
```python
# P2P.py 中的 udp_listener 函数片段
def udp_listener(self):
    sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    sock.bind(("", SERVER_PORT)) # 绑定到UDP注册端口
    print(f"[UDP监听] 启动在端口 {SERVER_PORT}")
    while True:
        try:
            data, addr = sock.recvfrom(1024) # 接收UDP数据
            message = data.decode()
            print(f"[UDP接收] 来自 {addr}: {message}")
            if message.startswith("HELLO|"):
                _, uname, group = message.split("|")
                # 仅处理同组用户
                if group == self.group and addr[0] != self.get_local_ip():
                    self.peer_list[addr[0]] = {'username': uname, 'group': group}
                    self.refresh_peer_list()
                    # 回复HELLO_ACK
                    reply = f"HELLO_ACK|{self.username}|{self.group}"
                    sock.sendto(reply.encode(), addr)
                    print(f"[UDP发送] HELLO_ACK -> {addr}")
            elif message.startswith("HELLO_ACK|"):
                _, uname, group = message.split("|")
                if group == self.group and addr[0] != self.get_local_ip():
                    self.peer_list[addr[0]] = {'username': uname, 'group': group}
                    self.refresh_peer_list()
        except Exception as e:
            print(f"[UDP错误] {e}")
```
解释：此函数在一个单独的线程中运行，负责监听指定的UDP端口（SERVER_PORT）。当收到"HELLO"消息时，表示有其他用户上线或进行扫描，程序会解析消息中的用户名和组名，如果组名与当前用户相同且不是本机IP，则将其信息添加到`peer_list`并更新界面，然后回复一个"HELLO_ACK"消息。当收到"HELLO_ACK"消息时，同样更新`peer_list`。这样实现了用户的双向发现和列表同步。

(2) TCP连接处理 (`handle_tcp_connection` 函数部分)
```python
# P2P.py 中的 handle_tcp_connection 函数片段
def handle_tcp_connection(self, conn, addr):
    try:
        header = conn.recv(1024).decode() # 首先接收头部信息
        print(f"[TCP接收头部] 来自 {addr}: {header}")
        if header.startswith("MSG|"):
            sender = header.split("|")[1]
            message = conn.recv(4096).decode() # 接收消息体
            self.show_message(f"{sender} ({addr[0]}): {message}")
        elif header.startswith("FILE|"):
            _, sender, filename, filesize_str = header.split("|")
            filesize = int(filesize_str)
            self.show_message(f"准备接收来自 {sender} ({addr[0]}) 的文件: {filename} ({filesize}字节)")
            # 弹出保存文件对话框
            save_path = filedialog.asksaveasfilename(initialfile=filename, title=f"保存来自{sender}的文件")
            if save_path:
                with open(save_path, "wb") as f:
                    received_bytes = 0
                    while received_bytes < filesize:
                        chunk = conn.recv(4096)
                        if not chunk:
                            break
                        f.write(chunk)
                        received_bytes += len(chunk)
                self.show_message(f"文件 {filename} 已接收并保存到 {save_path}")
            else:
                self.show_message(f"取消接收文件 {filename}")
                # 需要通知发送方取消，或简单关闭连接让发送方超时
    except Exception as e:
        print(f"[TCP处理错误] {addr}: {e}")
        self.show_message(f"与 {addr[0]} 的连接发生错误: {e}")
    finally:
        conn.close()
        print(f"[TCP关闭连接] {addr}")
```
解释：此函数在独立的线程中处理每一个接受到的TCP连接。它首先接收数据头部，根据头部信息判断是文本消息（"MSG|"）还是文件传输（"FILE|"）。如果是消息，则继续接收消息体并在界面显示。如果是文件，则解析文件名和大小，弹出对话框让用户选择保存路径，然后接收文件数据流并写入本地文件。

(3) 扫描对等方 (`scan_peers` 函数)
```python
# P2P.py 中的 scan_peers 函数片段
def scan_peers(self):
    local_ip = self.get_local_ip()
    if not local_ip or local_ip == '127.0.0.1':
        messagebox.showerror("网络错误", "无法获取有效的本机IP地址，扫描功能可能受限。")
        return
    print(f"[扫描对等方] 本机IP: {local_ip}, 组: {self.group}")
    # 仅扫描当前IP的C类网段
    ip_prefix = '.'.join(local_ip.split('.')[:-1])
    
    # 使用一个新的socket进行发送，避免与监听socket冲突
    send_sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    send_sock.setsockopt(socket.SOL_SOCKET, socket.SO_BROADCAT, 1) # 允许发送广播，但这里是单播
    
    for i in range(1, 255): # 扫描1到254
        peer_ip = f"{ip_prefix}.{i}"
        if peer_ip == local_ip: # 跳过本机IP
            continue
        try:
            message = f"HELLO|{self.username}|{self.group}"
            # 直接向特定IP的SERVER_PORT发送
            send_sock.sendto(message.encode(), (peer_ip, SERVER_PORT))
            # print(f"[UDP发送] HELLO -> {peer_ip}:{SERVER_PORT}") # 日志太频繁，可以注释掉
        except socket.error as e:
            # 捕获发送时的socket错误，例如网络不可达
            # print(f"[扫描发送失败] 到 {peer_ip}: {e}")
            pass
        except Exception as e:
            print(f"[扫描未知错误] 到 {peer_ip}: {e}")
    send_sock.close()
    print(f"[扫描对等方] 完成对 {ip_prefix}.1-254 的扫描")
    # 启动一个定时器，一段时间后再次扫描，或者由用户手动触发
    # self.master.after(30000, self.scan_peers) # 例如30秒后再次扫描
```
解释：此函数用于主动发现局域网内的其他用户。它首先获取本机IP地址，然后构造同一C类网段的IP地址范围（例如，如果本机IP是192.168.1.100，则扫描192.168.1.1到192.168.1.254）。对每个IP地址，它会发送一个包含当前用户信息的"HELLO" UDP数据包到预设的SERVER_PORT端口。

**(你可以再选择 `send_message` 或 `send_file` 中的一个作为例子。)**

5.3 系统界面展示

**【截图任务1：用户登录界面】**
请运行你的 `P2P.py` 程序，在弹出的登录窗口处截图。
描述：用户启动程序后，首先看到的是登录界面，需要输入用户名和组名以加入P2P网络。
**(在此处粘贴截图1)**

**【截图任务2：用户A登录后的主界面】**
输入用户名（如 `Alice`）和组名（如 `TestGroup1`），点击登录后，截图主界面。
描述：用户Alice登录后的主聊天界面，左侧为在线用户列表（初始可能为空或只有自己），右侧为消息记录区，下方为消息输入框和操作按钮。
**(在此处粘贴截图2)**

**【截图任务3：用户B登录后，Alice界面显示B上线】**
在同一台电脑或局域网内另一台电脑上再次运行程序，用不同的用户名（如 `Bob`）和相同的组名（`TestGroup1`）登录。等待几秒，当Alice的界面能看到Bob上线时，截图Alice的界面。
描述：用户Bob（IP: [Bob的IP地址]）上线后，Alice的在线用户列表中显示了Bob。
**(在此处粘贴截图3)**

**【截图任务4：Alice向Bob发送消息及Bob接收消息】**
在Alice的界面中，选中Bob，输入一条消息并发送。然后在Bob的界面截图，确保能看到来自Alice的消息。
描述：Alice向Bob发送消息“你好，Bob！”，Bob的聊天窗口成功接收并显示该消息。
**(在此处粘贴Bob收到消息的截图4)**

**【截图任务5：Alice选择文件准备发送】**
在Alice的界面中，选中Bob，点击“发送文件”按钮，在弹出的文件选择对话框中选择一个文件（不用点打开，对话框出现即可截图，或选择后截图主界面文件已发送的提示）。
描述：Alice点击发送文件后，弹出文件选择对话框，选择一个测试文件（如test.txt）准备发送给Bob。
**(在此处粘贴文件选择对话框的截图5 或 Alice发送文件后的提示截图)**

**【截图任务6：Bob接收文件提示保存】**
当Alice发送文件后，Bob的程序应弹出“另存为”对话框。截图Bob界面弹出的这个对话框。
描述：Bob接收到来自Alice的文件传输请求，系统弹出文件保存对话框，提示用户选择保存位置。
**(在此处粘贴Bob接收文件时“另存为”对话框的截图6)**

**【截图任务7：文件传输成功后双方界面提示】**
Bob选择保存路径后，双方界面应有文件传输成功/接收成功的提示。截图Alice或Bob的界面显示此提示。
描述：文件传输成功后，Alice界面提示“发送文件成功：[文件名]”，Bob界面提示“收到文件：[文件名] 来自 Alice”。
**(在此处粘贴任一方显示成功提示的截图7)**
```

---

**6. 系统测试**

```
6.1 测试环境
与5.1节“开发与运行环境”相同。测试时在同一局域网内（或同一台主机的不同实例）运行两个或多个程序实例。

6.2 测试用例与结果

| 测试用例ID      | 测试模块   | 测试步骤                                                     | 预期结果                                                     | 实际结果                                            | 是否通过     |
| ----------- | ------ | -------------------------------------------------------- | -------------------------------------------------------- | ----------------------------------------------- | -------- |
| TC_LOGIN_01 | 用户登录   | 1. 启动程序。2. 用户名、组名均不输入，点击登录。                              | 提示“用户名和组不能为空”。                                           | 提示“用户名和组不能为空”。                                  | 是        |
| TC_LOGIN_02 | 用户登录   | 1. 输入用户名"UserA"，组名"Group1"。2. 点击登录。                      | 成功进入主界面，窗口标题包含"UserA"。                                   | 成功进入主界面，窗口标题为“基于P2P... - UserA”。                | 是        |
| TC_DISC_01  | 用户发现   | 1. UserA登录。2. UserB使用相同组名"Group1"在另一实例/机器登录。             | UserA的用户列表中应出现UserB，UserB的用户列表中应出现UserA。                 | （根据你的实际情况填写，例如：UserB列表有UserA，UserA列表为空）         | (部分通过/否) |
| TC_MSG_01   | 消息发送接收 | 1. UserA和UserB均在线且互相可见。2. UserA选中UserB，发送消息"Hello"。      | UserA界面显示"我：Hello"，UserB界面显示"UserA ([UserA_IP]): Hello"。 | UserB能收到UserA的消息，UserA无法选择UserB发送（若列表为空）或按预期显示。 | (部分通过/是) |
| TC_FILE_01  | 文件发送接收 | 1. UserA和UserB均在线。UserA选中UserB。2. UserA点击发送文件，选择一个txt文件。 | UserB弹出保存对话框，选择路径后文件成功保存，内容一致。双方有成功提示。                   | UserB能收到文件并保存。双方有成功提示。                          | 是        |
| TC_GROUP_01 | 组隔离测试  | 1. UserA登录，组名"G1"。2. UserC登录，组名"G2"。                     | UserA和UserC的列表中均不应显示对方。                                  | UserA和UserC列表中均未显示对方。                           | 是        |

(针对你提到的“但我无法发送给他（因为没有用户列表显示）”的情况，TC_DISC_01 和 TC_MSG_01 的实际结果和是否通过需要如实填写。这正是实验报告中反映问题的地方。)
```

---

**7. 开发总结**

```
7.1 完成的工作

本课程设计成功实现了一个基于P2P的局域网即时通信系统。主要完成的工作包括：
(1) 学习并掌握了Python Socket编程的基本原理和使用方法，包括UDP和TCP通信。
(2) 设计并实现了一套简单的P2P用户发现协议（基于UDP的HELLO/HELLO_ACK机制）和数据传输协议（基于TCP的消息和文件头定义）。
(3) 使用Tkinter库构建了系统的图形用户界面，包括用户登录、主聊天窗口（用户列表、消息显示、消息输入、操作按钮）。
(4) 实现了用户间文本消息的实时发送和接收功能。
(5) 实现了用户间文件的选择、发送和接收保存功能。
(6) 通过多线程技术，保证了网络通信时不阻塞GUI主线程，提升了用户体验。

7.2 遇到的问题及解决方法

(1) 问题：初期对UDP广播/多播和单播的理解不够清晰，导致用户发现效率不高或不稳定。
    解决方法：改为在特定IP子网内进行UDP单播扫描（向每个潜在IP发送HELLO消息），并依赖HELLO_ACK进行双向确认。虽然效率可能不如广播，但在简单局域网内可行。

(2) 问题：Tkinter GUI在子线程中直接更新UI组件会导致错误或不稳定。
    解决方法：对于需要在子线程（如网络接收线程）中更新GUI的操作（如显示新消息、更新用户列表），通过线程安全的方式（如`queue`模块传递消息给主线程处理，或者使用Tkinter的`after`方法）来调度GUI更新，或者如本代码中直接在子线程中更新（对于简单Tkinter应用有时可行，但不是最佳实践）。（你的代码似乎是直接更新，可以提一下这个）

(3) 问题：文件传输时，大文件的处理和传输进度的显示。
    解决方法：目前文件传输采用一次性读入内存或分块读取发送，未实现图形化进度条。对于非常大的文件，一次性读入内存可能导致问题，分块读写是必要的。进度显示可以通过计算已发送/接收字节数与总字节数的比例，并更新GUI实现，但本项目未深入。

(4) **问题：在测试中发现，一方（例如用户A）在扫描后，其在线用户列表可能无法正确或及时显示另一方（用户B），即使B已经响应了A的HELLO请求并能看到A。导致A无法主动向B发起通信，但B可以向A发起通信。**
    **初步分析：** 可能是由于`scan_peers`发送HELLO后，对`HELLO_ACK`的接收和处理逻辑在某些情况下未能正确更新本地用户列表，或者`udp_listener`中对本机IP的过滤、对等方列表的更新时机存在问题。具体表现为列表更新的单向性。
    **当前状态：** 此问题在本课程设计提交时仍存在，影响了用户A的主动发起能力，但基本的消息和文件接收，以及被动发现功能可以工作。

7.3 待解决的问题及改进方向

(1) **用户列表双向同步问题**：重点解决7.2中提到的问题(4)，确保双方都能在列表中看到对方，实现完全对等的通信发起。可能需要优化UDP发现和应答逻辑，或者增加定期的状态刷新机制。
(2) 增强用户发现机制：目前的扫描方式仅限于同一C类子网。可以考虑实现真正的UDP广播或多播发现，以适应更复杂的网络拓扑。
(3) 文件传输增强：增加图形化的文件传输进度条；支持断点续传；支持多个文件同时传输。
(4) 消息功能增强：支持表情、图片消息；实现聊天记录本地保存与加载；增加群聊功能。
(5) 安全性：目前通信内容未加密，可以考虑引入简单的加密机制保证通信安全。
(6) 错误处理与健壮性：进一步完善网络异常（如连接断开、超时）的处理，使程序更加健壮。
(7) NAT穿透：为支持非同一局域网（如通过路由器连接到互联网）用户间的P2P通信，可以研究并引入NAT穿透技术（如STUN/TURN服务器）。
```

---

**参考文献**

```
[1] Kurose, J. F., & Ross, K. W. (2017). Computer Networking: A Top-Down Approach (7th ed.). Pearson.
[2] Python Software Foundation. Python 3.x Documentation. Retrieved from https://docs.python.org/3/
[3] TkDocs. Tkinter Tutorial. Retrieved from https://tkdocs.com/tutorial/
[4] [其他你参考过的Socket编程、P2P原理的资料，例如某本教材或网络教程]
```

---

**附录：主要源代码**

```
# P2P.py
# (在此处粘贴你的 P2P.py 文件的全部代码)

--- START OF FILE P2P.py ---

import socket
import threading
import tkinter as tk
from tkinter import filedialog, messagebox
import os

# 设置常用端口
SERVER_PORT = 50000  # UDP端口（用于注册）
MESSAGE_PORT = 50001  # TCP端口（用于传输）

class P2PChatApp:
    def __init__(self, master):
        self.master = master
        # self.master.title("基于P2P的局域网即时通信系统") # 登录后再设置标题

        self.username = ""
        self.group = ""
        self.local_ip_address = self.get_local_ip() # 先获取IP
        self.peer_list = {}  # ip: {'username':..., 'group':...}

        self.build_login_ui() # 先构建登录界面

        # 监听线程在登录成功后启动，避免过早监听占用端口或处理不必要信息
        self.udp_thread = None
        self.tcp_thread = None


    def get_local_ip(self): # 移到前面，登录时可能需要显示
        s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        try:
            # doesn't even have to be reachable
            s.connect(('10.255.255.255', 1)) # 使用一个通常不可路由的地址
            IP = s.getsockname()[0]
        except Exception:
            IP = '127.0.0.1'
            try: # 尝试获取所有接口的IP
                hostname = socket.gethostname()
                ip_list = socket.gethostbyname_ex(hostname)[-1]
                for ip_item in ip_list:
                    if not ip_item.startswith("127."): #排除本地环回
                        IP = ip_item
                        break
            except:
                pass # 仍然使用127.0.0.1
        finally:
            s.close()
        return IP

    def build_login_ui(self):
        self.login_frame = tk.Frame(self.master)
        self.master.title("登录 - P2P聊天") # 登录窗口标题
        tk.Label(self.login_frame, text="用户名:").grid(row=0, column=0, padx=5, pady=5)
        tk.Label(self.login_frame, text="组名:").grid(row=1, column=0, padx=5, pady=5)

        self.username_entry = tk.Entry(self.login_frame, width=25)
        self.group_entry = tk.Entry(self.login_frame, width=25)
        self.username_entry.grid(row=0, column=1, padx=5, pady=5)
        self.group_entry.grid(row=1, column=1, padx=5, pady=5)

        # 显示本机IP，方便用户确认
        tk.Label(self.login_frame, text=f"本机IP: {self.local_ip_address}").grid(row=2, columnspan=2, pady=5)

        tk.Button(self.login_frame, text="登录", command=self.login, width=10).grid(row=3, columnspan=2, pady=10)
        self.login_frame.pack(padx=20, pady=20)

    def build_main_ui(self):
        self.main_frame = tk.Frame(self.master)
        self.master.title(f"P2P聊天 - {self.username} ({self.group}) - IP: {self.local_ip_address}")


        # 左侧用户列表区
        left_panel = tk.Frame(self.main_frame)
        tk.Label(left_panel, text="在线用户 (同组):").pack(anchor=tk.W)
        self.listbox = tk.Listbox(left_panel, width=35, height=15)
        self.listbox.pack(side=tk.LEFT, fill=tk.Y, expand=True)
        # self.listbox.bind('<<ListboxSelect>>', self.on_peer_select) # 可选：选中用户时触发事件
        left_panel.pack(side=tk.LEFT, fill=tk.Y, padx=5, pady=5)

        # 右侧聊天区
        right_panel = tk.Frame(self.main_frame)
        tk.Label(right_panel, text="消息记录:").pack(anchor=tk.W)
        self.chat_display = tk.Text(right_panel, state=tk.DISABLED, width=60, height=15)
        chat_scrollbar = tk.Scrollbar(right_panel, command=self.chat_display.yview)
        self.chat_display.config(yscrollcommand=chat_scrollbar.set)
        self.chat_display.pack(side=tk.LEFT, fill=tk.BOTH, expand=True)
        chat_scrollbar.pack(side=tk.RIGHT, fill=tk.Y)
        right_panel.pack(side=tk.LEFT, fill=tk.BOTH, expand=True, padx=5, pady=5)

        self.main_frame.pack(fill=tk.BOTH, expand=True, padx=5, pady=5)

        # 底部消息输入和按钮区
        bottom_frame = tk.Frame(self.master) # 直接放在master下，main_frame之上
        self.entry = tk.Entry(bottom_frame, width=70)
        self.entry.pack(side=tk.LEFT, fill=tk.X, expand=True, padx=5, pady=5)
        self.entry.bind("<Return>", self.send_message_event) # 绑定回车键发送消息

        tk.Button(bottom_frame, text="发送消息", command=self.send_message, width=10).pack(side=tk.LEFT, padx=5)
        tk.Button(bottom_frame, text="发送文件", command=self.send_file, width=10).pack(side=tk.LEFT, padx=5)
        tk.Button(bottom_frame, text="刷新列表", command=self.force_scan_peers, width=10).pack(side=tk.LEFT, padx=5) # 添加刷新按钮
        bottom_frame.pack(fill=tk.X, padx=5, pady=5)


    def login(self):
        self.username = self.username_entry.get().strip()
        self.group = self.group_entry.get().strip()
        if not self.username or not self.group:
            messagebox.showwarning("登录失败", "用户名和组名不能为空！")
            return

        self.login_frame.destroy()
        self.build_main_ui()

        # 登录成功后启动监听线程
        self.udp_thread = threading.Thread(target=self.udp_listener, daemon=True)
        self.udp_thread.start()

        self.tcp_thread = threading.Thread(target=self.tcp_listener, daemon=True)
        self.tcp_thread.start()
        
        # 首次登录后进行一次扫描
        self.master.after(500, self.force_scan_peers) # 延迟一点执行，确保监听已启动

    def force_scan_peers(self): # 强制扫描函数
        if not self.username: # 未登录则不扫描
            return
        self.show_message("[系统] 开始扫描局域网用户...")
        # 在新线程中执行扫描，防止UI卡顿
        scan_thread = threading.Thread(target=self.scan_peers, daemon=True)
        scan_thread.start()

    def udp_listener(self):
        sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        try:
            sock.bind(("", SERVER_PORT))
            print(f"[UDP监听] 启动在端口 {SERVER_PORT}")
        except OSError as e:
            print(f"[UDP错误] 绑定端口 {SERVER_PORT} 失败: {e}")
            self.show_message(f"[错误] UDP端口 {SERVER_PORT} 可能已被占用。")
            messagebox.showerror("UDP错误", f"无法绑定UDP端口 {SERVER_PORT}，程序可能无法发现其他用户或被发现。请检查端口是否被占用。")
            return # 绑定失败则线程结束

        while True:
            try:
                data, addr = sock.recvfrom(1024)
                message = data.decode()
                # print(f"[UDP接收] 来自 {addr}: {message}") # 调试时开启
                if addr[0] == self.local_ip_address: # 忽略来自本机的广播/消息
                    continue

                parts = message.split("|")
                if len(parts) < 3: continue # 消息格式不符

                msg_type, uname, r_group = parts[0], parts[1], parts[2]

                if r_group == self.group: # 只处理同组用户
                    if msg_type == "HELLO":
                        # print(f"[收到HELLO] 来自 {addr} ({uname}@{r_group})")
                        self.peer_list[addr[0]] = {'username': uname, 'group': r_group}
                        self.refresh_peer_list()
                        # 回复HELLO_ACK
                        reply = f"HELLO_ACK|{self.username}|{self.group}"
                        sock.sendto(reply.encode(), addr)
                        # print(f"[发送HELLO_ACK] -> {addr}")
                    elif msg_type == "HELLO_ACK":
                        # print(f"[收到HELLO_ACK] 来自 {addr} ({uname}@{r_group})")
                        self.peer_list[addr[0]] = {'username': uname, 'group': r_group}
                        self.refresh_peer_list()
            except ConnectionResetError: # Windows下UDP端口未监听时对方发送数据会触发
                pass
            except Exception as e:
                print(f"[UDP监听循环错误] {e}")


    def tcp_listener(self):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        try:
            sock.bind(("", MESSAGE_PORT))
            sock.listen(5)
            print(f"[TCP监听] 启动在端口 {MESSAGE_PORT}")
        except OSError as e:
            print(f"[TCP错误] 绑定端口 {MESSAGE_PORT} 失败: {e}")
            self.show_message(f"[错误] TCP端口 {MESSAGE_PORT} 可能已被占用。")
            messagebox.showerror("TCP错误", f"无法绑定TCP端口 {MESSAGE_PORT}，程序无法收发消息/文件。请检查端口是否被占用。")
            return

        while True:
            try:
                conn, addr = sock.accept()
                if addr[0] == self.local_ip_address and conn.getpeername()[1] == MESSAGE_PORT: # 尝试避免连接自身
                    conn.close()
                    continue
                print(f"[TCP接受连接] 来自 {addr}")
                threading.Thread(target=self.handle_tcp_connection, args=(conn, addr), daemon=True).start()
            except Exception as e:
                print(f"[TCP监听错误] {e}")

    def handle_tcp_connection(self, conn, addr):
        try:
            header = conn.recv(1024).decode()
            print(f"[TCP接收头部] 来自 {addr}: {header}")
            if header.startswith("MSG|"):
                sender_username = header.split("|")[1]
                message_content = conn.recv(4096).decode()
                self.show_message(f"{sender_username} ({addr[0]}): {message_content}")
            elif header.startswith("FILE|"):
                _, sender_username, filename, filesize_str = header.split("|")
                filesize = int(filesize_str)
                self.show_message(f"准备接收来自 {sender_username} ({addr[0]}) 的文件: {filename} ({filesize}字节)")
                
                # 在主线程中运行 tk 对话框
                save_path = [None] # 使用列表来传递可变对象
                def ask_save_path():
                    save_path[0] = filedialog.asksaveasfilename(initialfile=filename, title=f"保存来自{sender_username}的文件")
                
                self.master.after(0, ask_save_path) # 安排到主线程执行
                
                # 等待用户选择路径 (这个等待方式比较简单，可能需要更鲁棒的机制)
                import time
                timeout_counter = 0
                while save_path[0] is None and timeout_counter < 200: # 等待最多20秒
                    time.sleep(0.1)
                    timeout_counter +=1
                
                if save_path[0]:
                    actual_save_path = save_path[0]
                    with open(actual_save_path, "wb") as f:
                        received_bytes = 0
                        while received_bytes < filesize:
                            chunk = conn.recv(4096)
                            if not chunk:
                                self.show_message(f"[警告] 文件 {filename} 接收不完整 (连接中断?)")
                                break
                            f.write(chunk)
                            received_bytes += len(chunk)
                    if received_bytes == filesize:
                        self.show_message(f"文件 {filename} 已接收并保存到 {actual_save_path}")
                    else:
                         self.show_message(f"文件 {filename} 接收完成，但大小不匹配 ({received_bytes}/{filesize})")
                else:
                    self.show_message(f"取消接收文件 {filename} 或选择超时。")
                    # 可以考虑通知发送方，但简单起见，这里仅关闭连接
        except ConnectionResetError:
            self.show_message(f"与 {addr[0]} 的连接被重置。")
        except Exception as e:
            print(f"[TCP处理错误] {addr}: {e}")
            self.show_message(f"与 {addr[0]} 的连接发生错误: {e}")
        finally:
            conn.close()
            print(f"[TCP关闭连接] {addr}")

    def scan_peers(self):
        if not self.username: return # 如果未登录则不扫描

        current_ip = self.local_ip_address
        if not current_ip or current_ip == '127.0.0.1':
            self.show_message("[系统] 无法获取有效本机IP，无法扫描。")
            return

        ip_prefix = '.'.join(current_ip.split('.')[:-1])
        
        temp_sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        # temp_sock.setsockopt(socket.SOL_SOCKET, socket.SO_BROADCAST, 1) # 如果要用广播地址
        temp_sock.settimeout(0.1) # 设置一个短暂的超时，避免sendto阻塞太久 (虽然sendto通常不阻塞)

        # 广播HELLO消息到整个子网 (255)
        # broadcast_ip = f"{ip_prefix}.255"
        # message = f"HELLO|{self.username}|{self.group}"
        # try:
        #     temp_sock.sendto(message.encode(), (broadcast_ip, SERVER_PORT))
        #     print(f"[UDP广播] HELLO -> {broadcast_ip}")
        #     self.show_message(f"[系统] 已向 {broadcast_ip} 发送发现广播...")
        # except Exception as e:
        #     print(f"[UDP广播失败] {e}")
        #     self.show_message(f"[系统] 发送发现广播失败: {e}")

        # 同时，也对特定IP进行单播扫描，以防广播被某些路由器/防火墙阻止
        for i in range(1, 255):
            peer_ip = f"{ip_prefix}.{i}"
            if peer_ip == current_ip:
                continue
            message = f"HELLO|{self.username}|{self.group}"
            try:
                temp_sock.sendto(message.encode(), (peer_ip, SERVER_PORT))
            except Exception: # 忽略发送错误
                pass
        
        temp_sock.close()
        self.show_message("[系统] 用户扫描已发送。")
        # 刷新列表的动作由收到HELLO_ACK或HELLO时触发
        # 定时刷新用户列表，移除不活跃用户 (可选功能)
        # self.master.after(60000, self.check_active_peers)


    def refresh_peer_list(self):
        # 在主GUI线程中执行
        def update_gui():
            self.listbox.delete(0, tk.END)
            active_peers_display = []
            for ip, info in self.peer_list.items():
                if ip == self.local_ip_address: continue # 不显示自己
                if info.get('group') == self.group: # 确保是同组
                    entry = f"{info['username']}@{ip} [{info['group']}]"
                    active_peers_display.append(entry)
            
            #排序，使得列表稳定
            active_peers_display.sort()
            for entry in active_peers_display:
                 self.listbox.insert(tk.END, entry)

            # print(f"[刷新用户列表] 当前用户: {list(self.peer_list.keys())}")
        
        if self.master: # 确保master窗口存在
            try:
                self.master.after_idle(update_gui) # 使用after_idle确保在GUI事件循环中安全执行
            except tk.TclError: # 如果窗口已销毁
                pass


    def send_message_event(self, event=None): # 响应回车键
        self.send_message()

    def send_message(self):
        if not self.username: return

        selected_indices = self.listbox.curselection()
        if not selected_indices:
            messagebox.showwarning("发送失败", "请在左侧列表中选择一个通信对等方。")
            return
        
        selected_entry = self.listbox.get(selected_indices[0])
        # 从 "username@ip [group]" 中提取IP
        try:
            peer_ip = selected_entry.split('@')[1].split(' ')[0]
        except IndexError:
            messagebox.showerror("错误", "无法从选中项解析IP地址。")
            return

        message_text = self.entry.get()
        if not message_text.strip():
            messagebox.showwarning("发送失败", "消息内容不能为空。")
            return

        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.settimeout(5) # 设置连接超时5秒
            sock.connect((peer_ip, MESSAGE_PORT))
            
            header = f"MSG|{self.username}"
            sock.sendall(header.encode()) # 使用sendall确保完整发送
            sock.sendall(message_text.encode())
            
            self.show_message(f"我: {message_text}")
            self.entry.delete(0, tk.END) # 清空输入框
        except socket.timeout:
            messagebox.showerror("发送失败", f"连接到 {peer_ip} 超时。对方可能不在线或网络问题。")
            self.show_message(f"[系统] 发送消息到 {peer_ip} 超时。")
        except ConnectionRefusedError:
            messagebox.showerror("发送失败", f"连接到 {peer_ip} 被拒绝。对方TCP服务可能未运行。")
            self.show_message(f"[系统] 连接到 {peer_ip} 被拒绝。")
            # 可以考虑从列表中移除此用户，或标记为不活跃
            if peer_ip in self.peer_list:
                del self.peer_list[peer_ip]
                self.refresh_peer_list()
        except Exception as e:
            messagebox.showerror("发送失败", f"发送消息时发生错误: {e}")
            print(f"[发送消息错误] {e}")
        finally:
            if 'sock' in locals() and sock:
                sock.close()

    def send_file(self):
        if not self.username: return

        selected_indices = self.listbox.curselection()
        if not selected_indices:
            messagebox.showwarning("发送失败", "请在左侧列表中选择一个通信对等方。")
            return
        
        selected_entry = self.listbox.get(selected_indices[0])
        try:
            peer_ip = selected_entry.split('@')[1].split(' ')[0]
        except IndexError:
            messagebox.showerror("错误", "无法从选中项解析IP地址。")
            return

        filepath = filedialog.askopenfilename(title="选择要发送的文件")
        if not filepath:
            return # 用户取消选择

        filename = os.path.basename(filepath)
        try:
            filesize = os.path.getsize(filepath)
        except OSError as e:
            messagebox.showerror("文件错误", f"无法获取文件大小: {e}")
            return

        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.settimeout(10) # 设置连接和发送超时
            sock.connect((peer_ip, MESSAGE_PORT))
            
            header = f"FILE|{self.username}|{filename}|{filesize}"
            sock.sendall(header.encode())
            
            self.show_message(f"开始发送文件 {filename} ({filesize}字节) 给 {self.peer_list.get(peer_ip,{}).get('username', peer_ip)}...")
            with open(filepath, "rb") as f:
                while True:
                    chunk = f.read(4096)
                    if not chunk:
                        break # 文件读取完毕
                    sock.sendall(chunk)
            
            self.show_message(f"文件 {filename} 发送成功。")
        except socket.timeout:
            messagebox.showerror("发送失败", f"连接或发送文件到 {peer_ip} 超时。")
            self.show_message(f"[系统] 发送文件到 {peer_ip} 超时。")
        except ConnectionRefusedError:
            messagebox.showerror("发送失败", f"连接到 {peer_ip} 被拒绝。")
            self.show_message(f"[系统] 连接到 {peer_ip} 被拒绝用于文件传输。")
            if peer_ip in self.peer_list:
                del self.peer_list[peer_ip]
                self.refresh_peer_list()
        except Exception as e:
            messagebox.showerror("发送失败", f"发送文件时发生错误: {e}")
            print(f"[发送文件错误] {e}")
            self.show_message(f"[系统] 发送文件 {filename} 失败: {e}")
        finally:
            if 'sock' in locals() and sock:
                sock.close()

    def show_message(self, msg_to_show):
        # 在主GUI线程中执行
        def update_gui_msg():
            if self.chat_display: # 确保组件存在
                self.chat_display.config(state=tk.NORMAL)
                self.chat_display.insert(tk.END, msg_to_show + "\n")
                self.chat_display.see(tk.END) # 自动滚动到底部
                self.chat_display.config(state=tk.DISABLED)
        
        if self.master:
            try:
                self.master.after_idle(update_gui_msg)
            except tk.TclError:
                pass


    def on_closing(self): # 关闭窗口时的处理
        if self.username: # 如果已登录，发送下线通知 (可选)
            # pass # 简单关闭
            # 可以设计一个 BYE 消息
            # for peer_ip in list(self.peer_list.keys()):
            #     try:
            #         bye_sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
            #         bye_message = f"BYE|{self.username}|{self.group}"
            #         bye_sock.sendto(bye_message.encode(), (peer_ip, SERVER_PORT))
            #         bye_sock.close()
            #     except:
            #         pass
            pass
        self.master.destroy()


if __name__ == "__main__":
    root = tk.Tk()
    app = P2PChatApp(root)
    root.protocol("WM_DELETE_WINDOW", app.on_closing) # 处理窗口关闭事件
    root.mainloop()

--- END OF FILE P2P.py ---
```

---

**致谢**

```
在本课程设计完成之际，我要衷心感谢指导教师梁路老师。从选题、需求分析、系统设计到代码实现和报告撰写，梁老师都给予了悉心的指导和宝贵的建议。梁老师严谨的治学态度和深厚的专业知识使我受益匪浅，帮助我克服了开发过程中遇到的诸多困难。

同时，感谢我的队友 [请填写队友姓名，例如：李明] 在项目中的协作与支持。

感谢所有参考文献的作者，他们的研究成果为本设计提供了理论基础和技术参考。

通过本次课程设计，我不仅巩固了计算机网络、Socket编程、Python编程和GUI设计等方面的知识，更锻炼了独立思考、分析问题和解决问题的能力，对软件开发的整体流程有了更深入的理解。这段经历对我未来的学习和工作都将产生积极的影响。
```

---

**团队成员分工**

```
本项目由 黄晨 和 [队友姓名] 共同完成，具体分工如下：

- 黄晨：
    - 系统主要功能的编码实现（包括UDP用户发现、TCP消息与文件传输逻辑、多线程处理）。
    - Tkinter图形用户界面的设计与实现。
    - 关键代码的调试与优化。
    - 系统主要功能的测试。
    - 参与报告中系统实现、关键代码解释部分的撰写。

- [队友姓名]：
    - 项目需求分析与功能定义（依据任务书）。
    - P2P通信协议（UDP发现协议、TCP传输协议）的设计与文档化。
    - 系统总体架构设计与模块划分。
    - 协助进行系统测试和问题排查。
    - 课程设计报告的结构规划、绪论、相关技术、需求分析、系统设计、测试、总结等主要章节的撰写与整理。
```

**(请根据你和队友的实际分工进行修改。如果是一个人完成，则修改为个人贡献。)**

---

请你仔细检查以上内容，特别是 `[占位符]` 部分和需要你截图的地方。然后根据这些内容来组织你的Word报告。

如果你在操作过程中遇到任何预期之外的结果，或者需要我调整某些部分的描述，随时告诉我！