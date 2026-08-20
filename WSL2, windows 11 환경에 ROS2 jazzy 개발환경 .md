
## 1. Windows 11 & WSL2 Ubuntu 24.04 설치
``` PowerShell
# Ubuntu 24.04 설치
wsl --install -d Ubuntu-24.04

# 버전 확인
wsl -l -v
```
# 2. ROS 2 Jazzy 코어 설치 (docs.ros.org 기준)

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
# 3. Gazebo Harmonic 및 SLAM/Nav2 패키지 설치
- Jazzy에서는 기존 Gazebo 대신 ros-gz(Gazebo Harmonic 브리지) 패키지를 설치합니다.

``` bash
sudo apt install -y \
  ros-jazzy-ros-gz \
  ros-jazzy-navigation2 \
  ros-jazzy-nav2-bringup \
  ros-jazzy-cartographer \
  ros-jazzy-cartographer-ros
```
# 4. 터틀봇3 워크스페이스 빌드 (Jazzy 브랜치)

``` bash
# 1. 워크스페이스 생성
mkdir -p ~/turtlebot3_ws/src
cd ~/turtlebot3_ws/src

# 2. Jazzy/최신 지원 브랜치 클론
git clone -b jazzy https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b jazzy https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b jazzy https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone -b jazzy https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

# 3. 의존성 설치 및 빌드
cd ~/turtlebot3_ws
rosdep install -i --from-path src --rosdistro jazzy -y
colcon build --symlink-install
```

# 5. 환경 변수 등록 (~/.bashrc)

``` bash
source /opt/ros/jazzy/setup.bash
```

``` bash
nano ~/.bashrc
```

- 맨 아래 다음 내용을 확인
``` bash
# ROS2 Jazzy Setup
source /opt/ros/jazzy/setup.bash
source ~/turtlebot3_ws/install/setup.bash

# TurtleBot3 Parameters
export TURTLEBOT3_MODEL=burger
export ROS_DOMAIN_ID=30
export LDS_MODEL=LDS-01
```

- 확인 차 다시 한번 더 적용
``` bash
source ~/.bashrc
```





















