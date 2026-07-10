## Manus Gloves ROS2 Driver

This is a basic ROS2 driver for [Manus Glove](https://www.manus-meta.com/products/quantum-metagloves). It broadcasts raw skeleton data as ROS2 messages.

![manus](https://github.com/user-attachments/assets/953ddc6b-aaf9-43a9-b369-875bac770406)

### How to Use

We tested the driver on Ubuntu 22.04 and ROS2 Humble. It should work with similar environments as well. Here's things you need to do before using it:

1. Install Manus Core on a Windows machine and upload your license to the dongle. A "Feature" license is required, otherwise you won't get message from Manus SDK.
2. Clone the repo into a ROS2 workspace, e.g. you should have a folders like this `~/ros2_ws/src/manus_ros2` and `~/ros2_ws/src/manus_ros2_msgs`.
3. Download [Manus SDK 2.4.0](https://docs.manus-meta.com/2.4.0/Resources/) and put it under the `manus_ros2` folder and rename it as ManusSDK. You should have a folders like this `~/ros2_ws/src/manus_ros2/ManusSDK/include` and `~/ros2_ws/src/manus_ros2/ManusSDK/lib`.
4. Follow [this guide](https://docs.manus-meta.com/2.4.0/Plugins/SDK/Linux/#installation) to install dependencies for Manus SDK. You should follow instructions for the "core Integrated" mode.
5. Build packages with `colcon build` and source the environment `source ~/ros2_ws/install/setup.bash`. Then run `ros2 run manus_ros2 rawdata_publisher`. Now you should see topics like `/manus_node_poses_0` and `manus_node_hierarchy_0`. There should be a pair of such topics for each glove.

We also include an example client program (in Python) that subscribes to topics of a single glove and controls a Shadow Hand in mujoco in the folder `client_scripts`. Note that only one glove should be connected. To use this, first source the ROS2 environment. Then install dependencies `pip install mujoco open3d mink`. We modified the example from [mink](https://github.com/kevinzakka/mink), a copy of which is already included. When running `python manus_data_viz.py`, it should open a open3d window and mujoco simulator window. Note that the client program uses inverse kinematics for retargetting. To get better results, you could try setting up a skeleton with Manus SDK directly.

Author: Qihao Yuan\
Email: qihao.yuan@rug.nl
