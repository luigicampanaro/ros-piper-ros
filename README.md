# Dockerized piper_ros ROS 2 package for the AgileX Piper

## Usage

On host:
```
./build.sh #Builds and tags Docker image
./run.sh   #Runs Docker image with correct options 
```
    
Inside container:
```
build   #Alias to build colcon_ws as root user
run     #Alias to run ROS package as correct user
```


# Piper deployment instructions (working 15/07/25)

## ✅ Host Setup (on the host machine)

- [ ] `sudo modprobe can`
- [ ] `sudo modprobe can_raw`
- [ ] `sudo modprobe can_dev`
- [ ] `sudo ip link set can0 up type can bitrate 1000000`  

## 🚀 Preparatory Steps to Control the Real Robot

- [ ] Connect the arm via USB–CAN adapter to your laptop  
- [ ] In the container: `cd src/piper_ros/`  
- [ ] In the container: `chmod +x can_activate.sh`  
- [ ] In the container: `./can_activate.sh can0 1000000`  

### 🤖 MoveIt (Real Robot)

- [ ] In the container:  
  ```bash
  ros2 launch piper start_single_piper.launch.py can_port:=can0 auto_enable:=true gripper_exist:=false

- [ ] In the container:  
  ```bash
  ros2 launch piper_no_gripper_moveit demo.launch.py


### ⚙️ Joint Control via Sliders (Real Robot)

- [ ] In the container:  
  ```bash
  ros2 launch piper start_single_piper_rviz.launch.py can_port:=can0 auto_enable:=true gripper_exist:=false


### 🛠 If Motors Not Yet Enabled
- [ ] In the container:  
  ```bash
  ros2 service call /enable_srv piper_msgs/srv/Enable "{enable_request: true}"