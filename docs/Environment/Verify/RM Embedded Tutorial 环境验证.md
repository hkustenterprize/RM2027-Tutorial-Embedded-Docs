# RM Embedded Tutorial：环境验证

## 1. macOS：创建并编译 STM32CubeMX 工程

### 1.1 创建 STM32CubeMX 工程

1. 打开 STM32CubeMX。
2. 点击 `ACCESS TO MCU SELECTOR`。

![打开 MCU Selector](RM%20Embedded%20Tutorial%20环境验证.assets/page-18-image-01.jpg)

搜索 `STM32F103C8T6`，然后选择对应芯片。

![选择 STM32F103C8T6](RM%20Embedded%20Tutorial%20环境验证.assets/page-19-image-01.jpg)

进入 `Project Manager`，将 `Toolchain / IDE` 设置为 `Makefile`。

![将 Toolchain IDE 设置为 Makefile](RM%20Embedded%20Tutorial%20环境验证.assets/page-20-image-01.png)

保存 STM32CubeMX 工程，然后点击 `GENERATE CODE`。

![生成代码](RM%20Embedded%20Tutorial%20环境验证.assets/page-21-image-01.png)

### 1.2 使用 Visual Studio Code 编译工程

在 Finder 中右键工程代码所在的文件夹，选择 `服务` → `新建位于文件夹位置的终端窗口`。

![在工程目录打开终端](RM%20Embedded%20Tutorial%20环境验证.assets/page-22-image-01.png)

在终端中执行：

```bash
code .
```

![使用 VS Code 打开工程](RM%20Embedded%20Tutorial%20环境验证.assets/page-22-image-02.jpg)

在 Visual Studio Code 中按 `` Control + ` `` 打开集成终端，然后执行：

```bash
make -j
```

![在 VS Code 中编译工程](RM%20Embedded%20Tutorial%20环境验证.assets/page-23-image-01.png)

如果终端输出与下图类似且没有编译错误，说明环境配置完成。

![编译成功](RM%20Embedded%20Tutorial%20环境验证.assets/page-24-image-01.png)

## 2. 克隆、编译并烧录嵌入式项目
