# micro_rtps_orangecube_ros2
Prerequisites : Fastrtps_gen 1.0.4 installed, PX4 manual compile enviroment
\
PX4 software : 1.13.2 (manual compile) for orangecube
\
System : Raspberry pi 4 Ubuntu 22.04
\
ROS2 : humble
\

Configured px4 micrortps <-> ROS2

RTPS serial port : Telem2

PX4 Parameter :  RTPS_CONFIG = TELEM 2 (can be set using QGroundControl parameters)

Port connection :  Telem2 <- FTDI cable -> USB
FIDI cable can be purchased at 
\
\
\
\
\
PX4 sw compile for orangecube
\
1.Download PX4 software from PX4 official github      (This repository should be v1.13.2!!)
2.Copy the .board file in my github (PX4-Autopilot/boards/cubepilot/cubeorange)  and paste it to the same directory in PX4 software
3.Copy the .yaml file in my github (PX4-Autopilot/msg/tools) and paste it to the same directory in PX4 software
4.run bleow command
\
make cubepilot_cubeorange_default



micrortps client start (orangecube):
1. Open QGroundControl (QGC)
2. Connect oragnecube to QGC using debug port
3. Open Mavlink console
4. run the below command
\
micrortps_client start -t UART -d /dev/ttyS1 -b 921600

5. client status check (optional)
\
micrortps_client status


6. firmware version check (optional)
\
ver --all
\
\
\
Downlaod the soruce code (run below command)
\
cd ~
\
git clone https://github.com/KangneoungLee/micro_rtps_orangecube_ros2.git px4_com_13_2_ws
\
\
micrortps agent start (rpi 4):
1. Build the ros workspace using px4_ros_com/scripts/build_ros2_workspace.bash (run the below command)   
\
cd ~/px4_com_1_13_2_ws/px4_ros_com/scripts
\
source build_ros2_workspace.bash
\
2. run the below commands
\
cd ~/px4_com_1_13_2_ws
source install/setup.bash
micrortps_agent -t UART -d /dev/ttyUSB0 -b 921600
ros2launch px4_ros_com sensor_combined_listener.launch.py
