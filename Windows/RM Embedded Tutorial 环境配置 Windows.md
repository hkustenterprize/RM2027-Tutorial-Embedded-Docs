# RM Embedded Tutorial：环境配置 - Windows

> **适用系统：** Windows 11 x64

## 1. 打开管理员终端

- 在开始菜单按钮处 `右键`。
- 在右键菜单中选择 `终端（管理员）`。

  ![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831165320.png)

- 在弹出的权限请求窗口中选择 `是`，给予管理员权限。

  ![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831144508.jpg)

- 之后，你将看到以下窗口，第一行应为 `Windows PowerShell`：

  ![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831144014.png)

这便是 PowerShell 终端。接下来的大部分安装操作都将在终端中进行。

## 2. 配置 Git

### 2.1 安装 Git 与 GitHub CLI

- 在 PowerShell 中输入以下命令：

```powershell
winget install -e Git.Git GitHub.cli --accept-package-agreements --accept-source-agreements
```

- 按 `Enter`。

安装过程中可能会弹出几个窗口。在进度条完成之前，**不要进行任何操作**。

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831144905.png)

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831214837.png)

安装成功后，终端输出应如下：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831215136.png)

### 2.2 使用 HTTPS 登录 GitHub

**终端操作**

- 点击终端窗口上方标签栏右侧的 `+` 按钮，新建一个 PowerShell 标签页。
- 输入以下指令：

```powershell
gh auth login
```

- 按 `Enter`。

依次出现以下 4 个界面时，按 `Enter` 接受默认选项：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831160937.png)

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831160955.png)

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161038.png)

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161050.png)

随后终端会显示一次性代码：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161156.png)

- **复制此时显示的 `one-time code`**，按 `Enter`。

**浏览器验证**

随后浏览器会自动打开 GitHub 验证页面：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161230.png)

- 点击 `Continue`。

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161257.png)

- 输入**终端中显示的** 8 位一次性代码，点击 `Continue`。

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161355.png)

- 点击 `Authorize GitHub`，并按照网页指示验证你的账户。

**验证结果**

验证成功后，网页和终端应显示如下。

网页：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161627.png)

终端：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831161550.png)

### 2.3 设置 Git 用户信息

在终端中分别执行以下命令，将姓名和邮箱**替换为自己的信息**：

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

> **Git 用户信息说明**
>
> - `user.name` 不必与 GitHub 用户名相同，它只是提交记录中显示的作者名称。
> - Git 对提交邮箱没有格式要求。若希望提交记录关联到 GitHub 账号并计入贡献统计，请使用已关联到该账号的邮箱。
> - 提交邮箱会写入 Git 历史并可能公开。如不想公开真实邮箱，可使用 GitHub 提供的 `noreply` 邮箱。
>
> 详情请参阅 [GitHub 贡献归属说明](https://docs.github.com/en/account-and-profile/how-tos/contribution-settings/troubleshooting-missing-contributions) 和 [设置提交邮箱](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address)。

执行以下命令确认配置：

```powershell
git config --global --get user.name
git config --global --get user.email

```

配置与检查结果应如下：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Screenshot%202026-09-01%20000233.png)

## 3. 配置 C/C++ 嵌入式编译工具链

### 3.1 安装工具链

- 点击终端窗口上方标签栏右侧的 `+` 按钮，新建一个 PowerShell 标签页。
- 输入：

```powershell
winget install -e ezwinports.make Kitware.CMake Ninja-build.Ninja Arm.GnuArmEmbeddedToolchain --accept-package-agreements --accept-source-agreements
```

- 按 `Enter`。

安装过程中可能会弹出几个窗口。在进度条完成之前，**不要进行任何操作**。

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831170722.png)

若中途弹出以下 CMD 窗口，直接关闭即可：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831171007.png)

若安装成功，PowerShell 最终输出应类似以下内容，并出现 4 次 `Successfully installed`：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831171055.png)

安装完成后，关闭管理员终端的所有标签页。

### 3.2 验证工具链

打开一个新的终端窗口（**非**管理员），依次执行以下指令：

```powershell
make --version
cmake --version
ninja --version
arm-none-eabi-gcc --version
arm-none-eabi-g++ --version

```

执行结果若如下，说明安装成功：

![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831204335.png)

验证完成后，可以关闭终端窗口。

## 4. 安装开发软件

### 4.1 安装 VS Code

若已安装 VS Code，可跳过本节。

- 从 [Visual Studio Code](https://code.visualstudio.com/) 下载最新的 VS Code 安装包。
- 运行下载的 `VSCodeUserSetup-xxx-x.xxx.x.exe`。
- 点击 `Next`，**直到见到此页**。请确保以下 **4 个选项全部勾选**。

  ![](RM%20Embedded%20Tutorial%20环境配置%20Windows.assets/Pasted%20image%2020260831210220.png)

- 点击 `Next` 并同意必要的协议，直到安装结束。

### 4.2 下载嵌入式开发软件安装包

- 下载全部 4 个 EXE 文件：[Windows Installer - Google Drive](https://drive.google.com/drive/folders/1EOInHq8uI7IkX7qAfVduWJLmwroviRnI?usp=sharing)

> **官方下载页面**
>
> - [STM32CubeMX - STMicroelectronics](https://www.st.com/en/development-tools/stm32cubemx.html)
> - [J-Link / J-Trace - SEGGER](https://www.segger.com/downloads/jlink)

### 4.3 安装 STM32CubeMX

- 运行 `SetupSTM32CubeMX-6.18.1.exe`。
- 点击 `Next` 并同意必要的协议，直到安装结束。

### 4.4 安装 J-Link Driver

- 运行 `JLink_Windows_V792c_x86_64.exe`。
- 点击 `Next` 并同意必要的协议，直到安装结束。

### 4.5 安装 Ozone

- 运行 `Ozone_Windows_V330b_x64.exe`。
- 点击 `Next` 并同意必要的协议，直到安装结束。

### 4.6 安装 SystemView

- 运行 `SystemView_Windows_V410b_x64.exe`。
- 点击 `Next` 并同意必要的协议，直到安装结束。

## 5. 下一步

环境配置完成。接下来请继续进行 [环境验证](<../Verify/RM Embedded Tutorial 环境验证.md>)。
