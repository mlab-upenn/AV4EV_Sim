# AV4EV_Sim_readme

This is the build version of AV4EV Simulator for Linux and should run without installing other dependencies. This simulator is based on SODA Sim and integrated by Po-Jen Wang (pojen.wang@autoware.org) and Alexander Kalmykov

This version (Ver 1.1.0) includes the Purdue Grand Prix race track (default) and Pennovation (under development) environments that we built.

Update May 15, 2024:
Updated the camera to the wide-angle NEXIGO webcam with 107 deg horizontal FOV
Now able to add AKS obstacles (boxes) to test obstacle avoidance
Increased the grass field's visible range
Increased the motor power for more responsive control
Relocated a cone that was inside the track area

Instructions to run AV4EV Sim:

1. Download `AV4EV_Sim.zip` at [https://drive.google.com/file/d/1goxswioa2MntthHZ-5inmKRmKjOJss0m/view?usp=drive_link]

2. If the machine has previously installed Autoware, edit the `.bashrc` file (under home, and ctrl+h to un-hide the hidden files) and comment out the following line toward the bottom:

   RMW_IMPLEMENTATION=rmw_cyclonedds_cpp

   Save and reboot. Autoware should run normally without this line. However, this line would need to be enabled before running AWSIM.

3. Extract the `AV4EV_Sim` folder from the compressed zip file

4. cd to `AV4EV_Sim/Linux/AV4EV/Binaries/Linux`

5. Run `./AV4EV` to launch the simulator

6. Hit `F11` to switch between `window` and `full-screen` modes

7. To spawn our go-kart in the environment

   On the top left corner, select `Free` and then `Editor Mode`

   Select the drop-down menu to the right (cube with green plus sign). Under `SODA Vehicles`, select and drag `Kart Full` into the scene where you’d like to place the vehicle

8. You may hit `X` (top right corner) to close the `Editor Mode` window after placing the go-kart to show the full UI. `Editor Mode` is used to edit component properties

9. Hit the green triangle Run button to start the simulation

10. Hit `X` (keyboard) to pose the vehicle (third-person mode) and enable UI, you’d be able to drive the go-kart with the keyboard’s `W`, `S`, `A`, and `D` keys, `X` will stop the vehicle immediately

    The vehicle currently has the following topics set up for sensor and control ROS2 interface:  
    Camera: /kart/camera  
    Lidar: /kart/lidar  
    GNSS: /kart/gnss  
    IMU: /kart/imu  
    Odom: /kart/odom  
    Control: /kart/ackermann_cmd  

    After the ackermann_msg is being published by your planner, Hit `M` to toggle between the keyboard manual control and autonomous mode (ROS2 ackermann_cmd)

    `AD Allowed` on the right will be enabled when the go-kart is controlled via ROS2

    You may use `rviz2` and `rqt` to test sensor output through ROS2 interface

11. Similar to spawning the go-kart, you can spawn boxes in the environment under `Tools` -> `Boxes` to test obstacle avoidance. Under the editor mode window, rotate the boxes along the `z-axis` (blue) by `33 deg` to face the race track

12. You can hit `Enter` to exit the 3rd-person mode and go back to `Spectator` mode 

13. You can hit `ctrl` and use the `mouse scroll` to zoom in/out of the camera view

14. You can change the map to `Pennovation` and have a sneak peek of the Pennovation environment we built. 

    Select the first icon (three horizontal lines) on the top left corner -> Open Level-> select Pennovation map

    The default camera position is off so you need to fly around with the keyboard and go above ground level before placing the go-kart on the ground

    This is still under development and there are some collision errors so the go-kart may not run correctly on all of the surfaces
