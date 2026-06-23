先安装 dlib，再安装 face_recognition
这是最关键的步骤，dlib 是 face_recognition 的核心依赖。

    1. 直接安装 dlib（成功率较低）

    sudo pip install dlib-bin --break-system-packages
    2. 接着安装 face_recognition：

    sudo pip install face_recognition --break-system-packages
    sudo pip3 install face_recognition --break-system-packages
