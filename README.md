# xf_platform

xf_platform 是基于 ESP-IDF 构建系统的，且兼容更多芯片的嵌入式开发平台。

## 简介

ESP-IDF 的构建系统拥有先进的理念以及完善的功能，其中包含了丰富的概念，如项目（project）、组件（components）、目标（Target）、配置菜单（menuconfig）、单元测试（Unity）等内容，且支持在 Linux、Windows、macOS 主机中交叉编译，足以满足大部分工程需求。

> [!NOTE]
> ESP-IDF 构建系统的详情请见：《[构建系统 - ESP32 - — ESP-IDF 编程指南 v5.4.1 文档](https://docs.espressif.com/projects/esp-idf/zh_CN/stable/esp32/api-guides/build-system.html)》

但 ESP-IDF 的构建系统专门适配 ESP32 系列芯片，而在以 STM32 为代表的 ARM 系列芯片上，通常使用的是 keil 工程，或是用较为简单的 CMake 或 Makefile 脚本，没有统一且完善的构建系统，跨芯片、跨工程开发通常较为繁琐。

因而，本项目希望借用 ESP-IDF 的构建系统，实现以下几个主要目标：

### 主要目标

1.  **为 XFusion 提供 Linux 或 Windows 平台上的构建支持**：

    1.  一是为了测试其中组件的可靠性。
    1.  二是为了解决嵌入式开发中常遇到的**硬件滞后（软件开发需要等待硬件）**、**目标芯片难以仿真**的问题。
        此项目通过在主机（PC）模拟器上调试开发，既可以解决软件要等待硬件才能启动的问题，也可以解决当目标机不方便调试时，难以确定应用逻辑出问题还是硬件出问题的问题。

1.  **实现支持跨平台、跨芯片的（如 STM32、AT32、nRF52 等芯片）嵌入式开发平台**：

    在以 STM32 这类 ARM 系列芯片为代表，且*没有完善的构建系统*，且*能够自行编译*（如使用`arm-none-eabi-gcc`）的情况下，本项目希望借助 ESP-IDF 的构建系统实现此跨平台、跨芯片的嵌入式开发平台。

## 使用方式

本项目目前还处在早期开发阶段，暂时只解决第 1 个主要目标，即在 Linux 上为 XFusion 提供构建支持。

### 首次安装

```bash
# 0. 确认 python 环境大于等于 3.10
mao@ubuntu:~/work/rbw/xf_platform$ python --version
Python 3.10.12
# 1. 创建 python 虚拟环境
mao@ubuntu:~/work/rbw/xf_platform$ python -m venv .venv
# 2. 激活 python 虚拟环境
# 2.1. Linux 上激活 python 虚拟环境
mao@ubuntu:~/work/rbw/xf_platform$ source .venv/bin/activate
# 2.2. Windows 上激活 python 虚拟环境
# .\.venv\Scripts\activate
# 2.3. 如果需要退出环境
# mao@ubuntu:~/work/rbw/xf_platform$ deactivate
# 3. 安装依赖
(.venv) mao@ubuntu:~/work/rbw/xf_platform$ pip install -r tools/requirements/requirements.core.txt
```

### 编译工程

对于 Linux。

```bash
# 1. 导出所需的环境变量
(.venv) mao@ubuntu:~/work/rbw/xf_platform$ export IDF_PATH=<xf_platform的实际完整路径>/xf_platform
(.venv) mao@ubuntu:~/work/rbw/xf_platform$ export IDF_TARGET=linux
# 2. 打开 hello_world 工程并编译
# 2.1. 移动
(.venv) mao@ubuntu:~/work/rbw/xf_platform$ cd examples/get-started/hello_world/
# 2.2. 创建构建文件夹
(.venv) mao@ubuntu:$ mkdir -p build
# 2.3. 生成 Unix Makefiles
(.venv) mao@ubuntu:$ cmake -S "." -B "build" -G "Unix Makefiles"
# 2.4. 打开菜单（实际上没有什么需要修改的）
(.venv) mao@ubuntu:$ make -C "build" menuconfig
# 2.5. 编译
(.venv) mao@ubuntu:$ make -C "build" -j
# 2.6. 运行（完毕）
(.venv) mao@ubuntu:$ ./build/hello_world.elf
hello_world
```

> [!NOTE]
> 1. 可以参考 ESP-IDF 的文档《[直接使用 CMake](https://docs.espressif.com/projects/esp-idf/zh_CN/stable/esp32/api-guides/build-system.html#cmake)》
> 1. 如果使用 ninja
>     ```
>     # 如果使用 ninja，2.3. ~ 2.5. 则使用以下命令
>     # $ cmake -S "." -B "build" -G "Ninja"
>     # $ ninja -C "build" menuconfig
>     # $ ninja -C "build" -j 0
>     ```

## 开源许可

本项目使用 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) 许可证开源。

## TODO

-   [ ] 完善对 XFusion 的支持。
-   [ ] 完善 Linux 模拟环境。
-   [ ] 使用 python 脚本简化 cmake 调用。
-   [ ] 使用 shell 脚本和 powershell 脚本实现在 Linux 和 Windows 环境的安装和导出。

## 第三方代码引用

详见 [NOTICE](./NOTICE)。
