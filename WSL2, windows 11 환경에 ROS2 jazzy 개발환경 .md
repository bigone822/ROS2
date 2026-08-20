
## 1. Windows 11 & WSL2 Ubuntu 24.04 설치
``` PowerShell
# Ubuntu 24.04 설치
wsl --install -d Ubuntu-24.04

# 버전 확인
wsl -l -v
```
2. ROS 2 Jazzy 코어 설치 (docs.ros.org 기준)

``` bash
# 1. 로케일 설정
sudo apt update && sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

# 2. Universe 저장소 및 키 등록
sudo apt install software-properties-common curl -y
sudo add-apt-repository universe -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# 3. Jazzy Desktop 및 빌드 툴 설치
sudo apt update
sudo apt install ros-jazzy-desktop ros-dev-tools python3-colcon-common-extensions -y

# 4. rosdep 초기화
sudo rosdep init
rosdep update
```
