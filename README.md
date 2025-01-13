# RealSense driver and ROS1 node

Using the [Relsense ROS wrapper (ros1 legacy branch)](https://github.com/IntelRealSense/realsense-ros/tree/ros1-legacy)

To start the camera node in ROS with default parameters:
```bash
roslaunch realsense2_camera rs_camera.launch
```

To specify parameters:
```bash
roslaunch realsense2_camera rs_camera.launch color_width:=1280 color_height:=720 color_fps:=30 depth_width:=1280 depth_height:=720 depth_fps:=30 align_depth:=true
```

Record rosbag:
```bash
rosbag record /camera/depth/image_rect_raw /camera/color/image_raw /tf /tf_static
```

# Update user permissions (to access USB)
In the dockerfile a user inheriting the host permissions is applied. <br>
Therefore, if your host computer and user does not have access to the USB (rw permission for `/dev/bus/usb/$#BUS$/$#DEVICE$`) this needs to be created. <br>
To add the group `plugdev` to have rw acess a script is made.
1. Make the script executable:
    ```bash
    chmod +x setup_usb_rules.sh
    ```
1. Run the script
    ```bash
    sudo ./setup_usb_rules.sh
    ```

# Docker (How to run docker environment)

Install docker and docker compose

Docker:
https://docs.docker.com/engine/install/

Docker compose:
https://docs.docker.com/compose/install/

Build the image:
```bash
docker compose build dev
```

Run the container add `-d` for running "detached mode" (container is running in the background):
```bash
docker compose up dev
```

Connect to the container:
```bash
docker exec -it $NAME bash
```

Remove everything, including stopped containers and all unused images (not just dangling ones):
```bash
docker system prune -a
```