安装Qt5开发包（最推荐）

这是最常见的原因，尤其是在全新或最小化安装的Ubuntu系统上。你需要安装 qtbase5-dev 包，它包含了 Qt5Config.cmake 文件。

打开终端，执行以下命令：


sudo apt update
sudo apt install qtbase5-dev

安装完成后，Qt5Config.cmake 文件通常会被放置在 /usr/lib/x86_64-linux-gnu/cmake/Qt5/ 目录下。之后，重新运行你的CMake命令即可。
方案二：手动指定Qt5的安装路径

如果你已经自行编译或安装了Qt5到非标准路径（例如 /home/oleksiy/Qt/5.15.2/wasm_32/），你需要告诉CMake去哪里找。

方法A：通过CMake命令行参数指定

在运行 cmake 时，通过 -DCMAKE_PREFIX_PATH 参数指定Qt5的安装根目录。注意，这个路径是Qt5的安装根目录，而不是 lib/cmake/Qt5 子目录。


cmake .. -DCMAKE_PREFIX_PATH=/path/to/your/Qt5/installation

例如，如果你的Qt5安装在 /home/user/Qt/5.15.2/gcc_64，命令就是：


cmake .. -DCMAKE_PREFIX_PATH=/home/user/Qt/5.15.2/gcc_64

方法B：通过CMake命令行参数直接指定 Qt5_DIR

直接设置 Qt5_DIR 变量为包含 Qt5Config.cmake 文件的目录。注意，这个路径需要精确到 Qt5 文件夹。


cmake .. -DQt5_DIR=/path/to/your/Qt5/installation/lib/cmake/Qt5

例如，如果你通过 apt 安装，路径通常是：


cmake .. -DQt5_DIR=/usr/lib/x86_64-linux-gnu/cmake/Qt5