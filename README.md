## 🧬 Zygisk Frida Gadget 模块使用指南

- 一个基于 Zygisk 的 Frida 注入模块，绕过传统 `frida-server` 的检测方式，仅支持arm64
- Inject gadget.so into target app via Zygisk. Only supports arm64

---

### ⚙️ 功能简介

- ⚡ 本模块可通过注入 `gadget.so` 实现 Frida 脚本注入，避免 `frida-server` 进程被直接识别或检测。
- 📱 适用于已 **Root** 的 Android 设备，要求已启用 **Magisk** 或 **KernelSU** 的 **Zygisk 环境**。
- 🎬 视频教程：[点击观看](https://b23.tv/pZk4AUi)

---

### 🍽️ 安装与使用步骤

```bash
1. 前往项目仓库：https://github.com/sucsand/sucsand，进入 Release 页面下载最新的 ZIP 安装包。

2. 将 ZIP 文件推送到手机，在 Magisk 或 KernelSU 中刷入该模块。
   - 💡 若使用 KernelSU，建议启用 LKM 模式以获得更高的稳定性。

3. 刷入完成后重启手机，系统将自动安装 `sucsand.apk`。
   - 打开 App，勾选你需要注入的目标 App；
   - 第1个框不填默认为模块自带的libgadget.so,可以填写你自己本地的libgadget.so文件路径，
     例如：/data/local/tmp/libgadget.so(你也可以直接解压缩模块后替换该文件，重新压缩后刷入即可)

   - 第2个框,不填默认为配置的listen模式.可以填写你自己的libgadget.config.so文件路径，
     例如：/data/local/tmp/libgadget.config.so(你也可以直接解压缩模块后替换该文件，重新压缩后刷入即可)

   - 第3个框,建议设置启动延迟为 100ms以上 以提升注入稳定性。


4. 勾选后，启动目标 App。此时目标 App 将保持挂起状态，等待 Gadget 注入。

5. 确保手机和电脑处于同一局域网内，使用以下命令注入脚本：
   frida -H <yourPhoneIp>:9999 -F -l yourScript.js

   👉 若你希望使用本地连接，可通过端口转发：
   adb forward tcp:9999 tcp:9999

   然后运行：
   frida -H 127.0.0.1:9999 -F -l yourScript.js
```

### ⚙️ Gadget 配置说明
默认配置为 listen 模式，监听端口 9999，你也可以根据需要修改模式或端口。

更多详细说明请参考 Frida 官方文档
```
{

  "interaction": {
    "type": "listen",
    "address": "0.0.0.0",
    "port": 9999,
    "on_port_conflict": "fail",
    "on_load": "wait"
  }
}
```

### ☕️ 加我微信(备注来意)、加入微信群聊、请我一杯咖啡(如果你觉得对你有帮助thanks)

<img src="https://github.com/user-attachments/assets/240deabc-1f0d-4a21-bebb-0947d8169326" width="210px">
<img src="https://github.com/user-attachments/assets/1549eead-0b1f-4013-800d-cec3a332b3ec" width="210px">
<img src="https://github.com/user-attachments/assets/d1cdac40-01ce-4669-ad8d-55ff814a1e24" width="210px">


### ⚠️ 注意事项
- ❗ 使用风险请自行承担
本模块仅供研究与安全分析用途，禁止用于非法活动。


