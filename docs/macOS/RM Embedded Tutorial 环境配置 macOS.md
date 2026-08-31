# RM Embedded Tutorial：环境配置 - macOS

> **适用系统：** macOS（Intel 或 Apple Silicon）

## 1. 准备安装包

从以下 Google Drive 文件夹下载 `Packages-MacOS`：

[Packages-MacOS - Google Drive](https://drive.google.com/drive/folders/14r4TiqKxl6bIqSqmbTKAaHJJGJwpHtlJ?usp=sharing)

> **官方下载页面**
>
> - [STM32CubeMX - STMicroelectronics](https://www.st.com/en/development-tools/stm32cubemx.html)
> - [J-Link / J-Trace - SEGGER](https://www.segger.com/downloads/jlink)

## 2. 安装 Visual Studio Code

根据 Mac 的芯片类型选择对应的安装包：

- Intel 芯片：`VSCode-darwin-intel.zip`
- Apple Silicon 芯片（例如 M1、M2）：`VSCode-darwin-apple-silicon.zip`

解压对应的安装包并安装 Visual Studio Code。

> **官方下载页面**
>
> - [Visual Studio Code](https://code.visualstudio.com/)

## 3. 安装 Homebrew

### 3.1 打开终端

1. 按 `Command + Space` 打开 Spotlight。
2. 输入 `terminal`，然后打开“终端”。

![通过 Spotlight 搜索终端](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-04-image-01.png)

### 3.2 执行安装命令

在终端中执行：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

如果终端要求输入密码，请输入当前用户的登录密码。输入密码时终端不会显示任何字符，这是正常现象。

![安装 Homebrew](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-05-image-01.png)

出现确认提示时按 `Enter`。之后如果安装程序再次等待输入，继续按 `Enter`，直到安装完成。

![Homebrew 安装完成](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-06-image-01.png)

## 4. 配置 Git 与 GitHub

### 4.1 安装 Git

在终端中执行：

```bash
brew install git
```

Git 安装完成后，终端输出应与下图类似：

![Git 安装完成](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-07-image-01.png)

### 4.2 使用 SSH 连接 GitHub

如果还没有 GitHub 账号，请先前往 [GitHub Sign Up](https://github.com/signup) 注册并登录。

打开 [GitHub SSH keys 设置](https://github.com/settings/keys)，点击 `New SSH key`。

![新建 GitHub SSH key](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-08-image-01.png)

在终端中执行以下命令，将 `youremail@example.com` 替换为 GitHub 账号使用的邮箱：

```bash
ssh-keygen -t ed25519 -C youremail@example.com
```

出现输入提示时按 `Enter` 接受默认设置，直到生成完成。终端显示的内容不必与下图完全相同，但整体格式应相似。

![生成 SSH key](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-09-image-01.png)

在输出中找到 `Your public key has been saved in` 后面的公钥文件路径。该路径通常以 `.pub` 结尾，将其复制下来。

![找到 SSH 公钥路径](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-10-image-01.png)

在终端中输入 `cat`、一个空格，再粘贴刚才复制的路径，然后按 `Enter`。例如：

```bash
cat /Users/yourname/.ssh/id_ed25519.pub
```

终端将显示一行以 `ssh-ed25519` 开头的内容。复制整行公钥。

![查看并复制 SSH 公钥](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-11-image-01.png)

回到 GitHub 的 `Add new SSH Key` 页面：

1. 在 `Title` 中输入任意便于识别的名称。
2. 将刚才复制的公钥粘贴到 `Key` 中。
3. 点击 `Add SSH key`。

![添加 SSH key](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-12-image-01.png)

添加成功后，SSH key 将出现在账号设置页面中：

![SSH key 添加成功](RM%20Embedded%20Tutorial%20环境配置%20macOS.assets/page-13-image-01.png)

在终端中测试连接：

```bash
ssh -T git@github.com
```

第一次连接时，终端可能要求确认主机身份。输入 `yes` 并按 `Enter`。

如果看到以下信息，说明 SSH 连接配置成功：

```text
Hi xxxxx! You've successfully authenticated, but GitHub does not provide shell access.
```

### 4.3 设置 Git 用户信息

在终端中分别执行以下命令，将姓名和邮箱替换为自己的信息：

```bash
git config --global user.name "Your Name"
git config --global user.email youremail@example.com
```

> **Git 用户信息说明**
>
> - `user.name` 不必与 GitHub 用户名相同，它只是提交记录中显示的作者名称。
> - Git 对提交邮箱没有格式要求。若希望提交记录关联到 GitHub 账号并计入贡献统计，请使用已关联到该账号的邮箱。
> - 提交邮箱会写入 Git 历史并可能公开。如不想公开真实邮箱，可使用 GitHub 提供的 `noreply` 邮箱。
>
> 详情请参阅 [GitHub 贡献归属说明](https://docs.github.com/en/account-and-profile/how-tos/contribution-settings/troubleshooting-missing-contributions) 和 [设置提交邮箱](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address)。

执行以下命令确认配置：

```bash
git config --global --get user.name
git config --global --get user.email
```

## 5. 安装编译工具链

在终端中依次执行以下命令：

```bash
brew install make
brew install cmake
brew install ninja
brew install gcc
brew install --cask gcc-arm-embedded
```

安装完成后，执行以下命令验证编译工具链：

```bash
make --version
cmake --version
ninja --version
arm-none-eabi-gcc --version
arm-none-eabi-g++ --version
```

如果终端能够显示版本信息，说明工具链已经安装成功。

## 6. 安装嵌入式开发软件

### 6.1 STM32CubeMX

解压 `SetupSTM32CubeMX-6.15.0.app.tar.gz`，然后打开安装程序并按照提示完成安装。

### 6.2 SEGGER J-Link

根据 Mac 的芯片类型选择对应的安装包：

- Intel 芯片：`JLink_MacOSX_V792c_x86_64.pkg`
- Apple Silicon 芯片：`JLink_MacOSX_V792c_arm64.pkg`

打开安装包并按照提示完成安装。

### 6.3 SEGGER Ozone

打开 `Ozone_MacOSX_V330b_x86_64.pkg`，按照提示完成安装。

## 7. 使用提示

- 在 macOS 上建议使用 STM32CubeMX 的 `Load Project` 功能打开 `.ioc` 工程。部分情况下，双击 `.ioc` 文件无法正确加载工程。
- 某些 Mac 需要在系统设置中为 STM32CubeMX 开启“完全磁盘访问权限”，否则可能无法找到 `.ioc` 工程文件。
- 需要从工程目录打开 Visual Studio Code 时，可以在 Finder 中右键文件夹，选择 `服务` → `新建位于文件夹位置的终端窗口`，再执行 `code .`。

## 8. 下一步

环境配置完成。接下来请继续进行 [环境验证](<../Verify/RM Embedded Tutorial 环境验证.md>)。
