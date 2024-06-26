# AV4EV_Sim

## Overview

This is the build version of AV4EV Simulator for Linux and should run without installing other dependencies. This simulator is based on SODA.Sim and integrated by Po-Jen Wang (pojen.wang@autoware.org) and Alexander Kalmykov (alex.kalm.dev@gmail.com).

## System Overview

The go-kart mechatronics system is designed as a modular system, consisting of several subsystems responsible for different tasks. There are seven major subsystems:
1. Power Distribution (PD)
2. Main Control (MC)
3. User Interface (UI)
4. Throttle-by-Wire (TBW)
5. Brake-by-Wire (BBW)
6. Steer-by-Wire (SBW)
7. Rear-Shelf Design (RSD)

In our go-kart drive-by-wire design, all subsystems except the PD and the RSD use an STM32 Nucleo development board on a standalone PCB as the electronic control unit (ECU). Communication is achieved using the controller area network (CAN) to allow efficient information exchange between nodes. These modular control systems are integrated with the original go-kart chassis in a non-intrusive manner and are easy to understand, build, and modify.

## Instructions to Run AV4EV Sim

### Download and Setup

1. Download `AV4EV_Sim.zip` from [this link](https://github.com/AlexanderRex/SodaAV4EV/releases/tag/v1.1.0).

2. If the machine has previously installed Autoware, edit the `.bashrc` file (under home, and `ctrl+h` to un-hide the hidden files) and comment out the following line toward the bottom:
    ```sh
    RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
    ```
3. Save and reboot. Autoware should run normally without this line. However, this line would need to be enabled before running AWSIM.

4. Extract the `AV4EV_Sim` folder from the compressed zip file.

5. Navigate to the directory:
    ```sh
    cd AV4EV_Sim/Linux/AV4EV/Binaries/Linux
    ```

6. Run the simulator:
    ```sh
    ./AV4EV
    ```

### Simulator Usage

- Hit `F11` to switch between window and full-screen modes.

#### To Spawn the Go-Kart in the Environment

1. On the top left corner, select `Free` and then `Editor Mode`.
2. Select the drop-down menu to the right (cube with green plus sign). Under `SODA Vehicles`, select and drag `Kart Full` into the scene where you’d like to place the vehicle.
3. You may hit `X` (top right corner) to close the Editor Mode window after placing the go-kart to show the full UI. Editor Mode is used to edit component properties.
4. Hit the green triangle `Run` button to start the simulation.
5. Hit `X` (keyboard) to pose the vehicle (third-person mode) and enable UI, you’d be able to drive the go-kart with the keyboard’s `W`, `S`, `A`, and `D` keys, `X` will stop the vehicle immediately.

### ROS2 Interface

The vehicle currently has the following topics set up for sensor and control ROS2 interface:
- Camera: `/kart/camera`
- Lidar: `/kart/lidar`
- GNSS: `/kart/gnss`
- IMU: `/kart/imu`
- Odom: `/kart/odom`
- Control: `/kart/ackermann_cmd`

After the `ackermann_msg` is being published by your planner, Hit `M` to toggle between the keyboard manual control and autonomous mode (ROS2 `ackermann_cmd`).

AD Allowed on the right will be enabled when the go-kart is controlled via ROS2.

You may use `rviz2` and `rqt` to test sensor output through ROS2 interface.

### Testing Obstacle Avoidance

Similar to spawning the go-kart, you can spawn boxes in the environment under `Tools -> Boxes` to test obstacle avoidance. Under the editor mode window, rotate the boxes along the z-axis (blue) by 33° to face the race track.

### Switching Modes

- Hit `Enter` to exit the 3rd-person mode and go back to Spectator mode.
- Hit `ctrl` and use the mouse scroll to zoom in/out of the camera view.

### Changing the Map

You can change the map to Pennovation and have a sneak peek of the Pennovation environment we built:
1. Select the first icon (three horizontal lines) on the top left corner -> Open Level -> select Pennovation map.
2. The default camera position is off so you need to fly around with the keyboard and go above ground level before placing the go-kart on the ground.
3. Note: This is still under development and there are some collision errors so the go-kart may not run correctly on all of the surfaces.

## Source Code

To use the source code of the plugin, you need to have an Unreal Engine project with SODA.Sim and SODA.Sim ROS2 plugins installed. You can find more information and download the plugins from the following repositories:
- [SODA.Sim GitHub Repository](https://github.com/soda-auto/soda-sim)
- [SODA.Sim ROS2 GitHub Repository](https://github.com/soda-auto/soda-sim-ros2)

## Authors

- Po-Jen Wang ([LinkedIn](https://www.linkedin.com/in/pojen-wang/))
- Alexander Kalmykov ([LinkedIn](https://www.linkedin.com/in/alexander-kalmykov-26379a1b4/))
