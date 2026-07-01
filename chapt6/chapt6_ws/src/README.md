
gz-rotary 是 Gazebo 机器人仿真器的一个“滚动发布”版，它不在 Ubuntu 的默认源中，需要手动添加 Gazebo 的官方软件源。

正确的安装流程如下：

    安装必要工具：
    

    sudo apt-get update
    sudo apt-get install curl lsb-release gnupg

    添加 Gazebo GPG 密钥：
    

    sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg

    添加 Gazebo 稳定版和 nightly 软件源：
    

    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null

    

    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-nightly $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-nightly.list > /dev/null

    再次更新软件源并安装：
    

    sudo apt-get update
    sudo apt-get install gz-rotary

⚠️ 重要提示

    系统版本：gz-rotary 官方支持 Ubuntu Noble (24.04) 和 Ubuntu Resolute (26.04)。请先用 lsb_release -a 检查你的系统版本，避免因版本不匹配导致安装失败。

    滚动更新：gz-rotary 是不稳定的“滚动发布”版，每天都会更新。不建议在生产环境中使用。如果是正式项目，建议安装稳定版（如 gz-jetty）。

    其他网络限制：如果你的机器在云上或企业内网，请检查防火墙或安全组的出方向规则，确保允许访问 packages.osrfoundation.org 的 80 端口。


安装好 gz-rotary 后，在终端中运行以下命令即可启动 Gazebo 仿真器：


gz sim

🚀 快速上手

安装完成后，可以运行一个示例世界来测试：


gz sim shapes.sdf

执行后，你会看到一个包含地面、太阳以及一些基本几何体（如立方体、球体）的3D仿真界面。
💡 常用选项与提示

    指定世界文件：启动时可以直接加载自己的世界文件（.sdf 格式）。
    

    gz sim 你的世界文件.sdf

    强制使用 Rotary 版本：如果系统中安装了多个 Gazebo 版本，可以用以下命令确保启动的是 Rotary 版本：
    

    gz sim --force-version 10.0.0 shapes.sdf

    查看已安装版本：运行以下命令可以查看系统中所有已安装的 Gazebo 版本：
    

    gz sim --versions

    无界面模式 (Headless)：如果不需要图形界面（例如在远程服务器上），可以安装 gz-sim-server 包，然后使用以下命令启动：
    

    /usr/libexec/gz/sim/gz-sim-server <你的世界文件.sdf>

⚠️ 重要提醒

gz-rotary 是一个滚动发布（rolling release） 版本，代码库每天都会更新，可能存在不稳定性。对于正式项目或新用户，官方更推荐安装如 gz-jetty 这样的稳定版本。