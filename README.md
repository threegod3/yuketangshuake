# 雨课堂高速刷课

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/threegod3/yueketangshuake
)](https://github.com/threegod3/yueketangshuake/releases)
[![GitHub stars](https://img.shields.io/github/stars/threegod3/yueketangshuake
)](https://github.com/threegod3/yueketangshuake/stargazers)
[![GitHub license](https://img.shields.io/github/license/threegod3/yueketangshuake)](https://github.com/threegod3/yueketangshuake/blob/main/LICENSE)

## 📖 项目简介

这是一个用于**雨课堂**视频课程的自动播放脚本。它通过模拟浏览器的“心跳包”行为，与雨课堂服务器进行通信，从而实现视频课件理论上可以以任意大的速率播放。

本项目的核心思路受启发于 [Cat1007/yuketangHelperSCUTLite](https://github.com/Cat1007/yuketangHelperSCUTLite) 项目。由于原项目发布时间较早，雨课堂平台已经更新了其心跳包的格式，导致原脚本无法正常工作。因此，本项目针对当前版本的雨课堂进行了适配和重构。


> ## ⚠️ 免责声明

本项目仅用于：

- 学习研究
- 技术交流
- 网络协议分析

**严禁用于：**

- 商业用途
- 违反学校规定的行为
- 任何违规或不当用途

使用本项目造成的任何后果 **由使用者自行承担**。

---


## ✨ 功能特点

- ✅ 支持正式课程和旁听课程
- ✅ 自动获取视频列表
- ✅ 模拟真实播放行为  
  `loadstart → seeking → loadeddata → play → playing → heartbeat`
- ✅ 可调节播放速度
- ✅ 支持批量处理多个视频
- ✅ 自动检测已完成视频并跳过

---

# 🔧 使用方法

## 1. 安装依赖

```bash
pip install requests
```
或者根据代码中的 import 内容安装对应库。

## 2. 获取必要信息

首先 登录自己的雨课堂账号，然后需要手动收集 8个关键参数。

需要进行 两个操作：

**1. 获取 Cookies 信息**

- 在浏览器中登录您的雨课堂（或长江雨课堂）账号，并打开任意一个课程页面。
- 按下 F12 键打开开发者工具。
- 切换到 Application (应用程序) 标签页。
- 在左侧菜单中找到 Cookies，并点击其下的雨课堂域名（例如：.yuketang.cn）。
- 在右侧的列表中，找到并记录下 **csrftoken、sessionid 和 university_id** 的值。可以参考 https://blog.csdn.net/lenfranky/article/details/90316262

**2. 从“心跳包”中获取信息**

- 在雨课堂中打开一个您需要学习的视频课件。
- 按下 F12 打开开发者工具，并切换到 Network (网络) 标签页。
- 刷新页面，然后手动点击视频播放几秒钟。
- 在 Network 标签页的筛选框中输入 heartbeat 进行搜索，找到名为 heartbeat/ 的请求。
- 点击该请求，在右侧的 Payload (负载) 或 Params (参数) 标签页中，找到以下字段的值并记录：
**u：对应 user_id
  classroomid：对应 classroom_id
  skuid：对应 skuid
  c：对应 course_id**

| 参数            | 来源        |
| ------------- | --------- |
| csrftoken     | Cookies   |
| sessionid     | Cookies   |
| university_id | Cookies   |
| user_id       | heartbeat/ |
| classroom_id  | heartbeat/ |
| skuid         | heartbeat/ |
| course_id     | heartbeat/ |
| name          | 自己填写课程名称  |

## 3. 速度调节

播放速度由以下两个参数控制：

```python
INCREMENT = (15, 20)   # 每次增加 15-20 秒
DELAY = (2, 4)         # 每次等待 2-4 秒
```
含义：

| 参数        | 作用       |
| --------- | -------- |
| INCREMENT | 每次视频时间跳跃 |
| DELAY     | 心跳包发送间隔  |

默认约 5–8倍速。

⚠️ 注意：

如果速度过快，可能导致：单次时间跳跃超过视频长度，刷课异常
建议根据实际情况适当调整。

## 4.  平台适配

当前版本在：

**华南理工大学的长江雨课堂测试通过**
**其他学校的雨课堂不清楚，但应该也适用**

如果你使用的是**其他雨课堂平台**，需要修改：

```python
url_root = "https://changjiang.yuketang.cn/"
```

替换为你学校对应的雨课堂域名，例如：

```python
https://xxx.yuketang.cn/
```


## 📊 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=threegod3/yueketangshuake&type=Date)](https://star-history.com/#threegod3/yueketangshuake&Date)

## 📜 License

本项目仅供**学习交流使用**。

如果本项目对你有帮助，欢迎点一个 ⭐ Star 支持！
