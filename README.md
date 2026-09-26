```text
amr_excellent_project/
│
├── README.md                                  # Tổng quan dự án
├── LICENSE                                    # Bản quyền mã nguồn
├── Makefile                                   # Lệnh build/run nhanh
├── .gitignore                                 # Bỏ qua build, log, map, bag nếu cần
├── .env.example                               # Mẫu biến môi trường ROS, port, domain ID
│
├── docs/                                      # Tài liệu đầy đủ của dự án
│   ├── 00_overview/
│   │   ├── system_overview.md
│   │   ├── quick_start.md
│   │   └── project_goals.md
│   │
│   ├── 01_architecture/
│   │   ├── architecture.md
│   │   ├── dataflow.md
│   │   ├── ros_graph.md
│   │   ├── tf_tree.md
│   │   └── hardware_software_interface.md
│   │
│   ├── 02_hardware/
│   │   ├── orange_pi_5.md
│   │   ├── stm32f407.md
│   │   ├── stm32f103.md
│   │   ├── lidar.md
│   │   ├── imu.md
│   │   ├── motor_encoder.md
│   │   └── power.md
│   │
│   ├── 03_firmware/
│   │   ├── firmware_overview.md
│   │   ├── encoder.md
│   │   ├── pid.md
│   │   ├── kinematics.md
│   │   ├── odometry.md
│   │   └── uart_protocol.md
│   │
│   ├── 04_ros2/
│   │   ├── topics.md
│   │   ├── nodes.md
│   │   ├── services.md
│   │   ├── tf.md
│   │   ├── launch.md
│   │   └── qos.md
│   │
│   ├── 05_protocol/
│   │   ├── packet_structure.md
│   │   ├── message_id.md
│   │   ├── crc.md
│   │   └── examples.md
│   │
│   ├── 06_slam_mapping/
│   │   ├── slam_concept.md
│   │   ├── slam_toolbox.md
│   │   ├── mapping_guide.md
│   │   └── save_map_guide.md
│   │
│   ├── 07_navigation/
│   │   ├── nav2_overview.md
│   │   ├── amcl.md
│   │   ├── costmap.md
│   │   └── waypoint_mission.md
│   │
│   ├── 08_calibration/
│   │   ├── wheel_calibration.md
│   │   ├── imu_calibration.md
│   │   └── lidar_tf_calibration.md
│   │
│   ├── 09_runbooks/
│   │   ├── startup.md
│   │   ├── mapping.md
│   │   ├── navigation.md
│   │   ├── shutdown.md
│   │   └── emergency.md
│   │
│   └── 10_troubleshooting/
│       ├── serial_issues.md
│       ├── odom_issues.md
│       ├── lidar_issues.md
│       ├── slam_issues.md
│       └── tf_issues.md
│
├── hardware/                                  # Tài liệu phần cứng
│   ├── schematics/
│   │   ├── power_schematic.pdf
│   │   ├── stm32_schematic.pdf
│   │   └── motor_driver_schematic.pdf
│   │
│   ├── wiring/
│   │   ├── wiring_diagram.md
│   │   ├── uart_wiring.md
│   │   ├── encoder_wiring.md
│   │   ├── imu_wiring.md
│   │   └── lidar_wiring.md
│   │
│   ├── bom/
│   │   └── bom.csv
│   │
│   └── cad/
│       ├── chassis.step
│       ├── lidar_mount.stl
│       └── wheel_layout.md
│
├── common/                                    # Phần dùng chung giữa firmware và ROS
│   └── amr_protocol/
│       ├── c/
│       │   ├── include/
│       │   │   ├── amr_protocol.h
│       │   │   ├── packet_defs.h
│       │   │   └── crc.h
│       │   └── src/
│       │       ├── packet.c
│       │       └── crc.c
│       │
│       ├── python/
│       │   ├── amr_protocol/
│       │   │   ├── __init__.py
│       │   │   ├── packet.py
│       │   │   ├── crc.py
│       │   │   └── messages.py
│       │   └── tests/
│       │       ├── test_packet.py
│       │       └── test_crc.py
│       │
│       ├── docs/
│       │   ├── protocol_spec.md
│       │   └── packet_examples.md
│       │
│       └── tests/
│           ├── test_packet_c.c
│           └── test_packet_python.py
│
├── firmware/                                  # Firmware STM32
│   ├── stm32f407_motion_controller/
│   │   ├── cube/
│   │   │   └── stm32f407_motion.ioc
│   │   │
│   │   ├── core/
│   │   │   ├── Inc/
│   │   │   │   ├── main.h
│   │   │   │   ├── gpio.h
│   │   │   │   ├── tim.h
│   │   │   │   ├── usart.h
│   │   │   │   ├── i2c.h
│   │   │   │   └── dma.h
│   │   │   └── Src/
│   │   │       ├── main.c
│   │   │       ├── gpio.c
│   │   │       ├── tim.c
│   │   │       ├── usart.c
│   │   │       ├── i2c.c
│   │   │       ├── dma.c
│   │   │       └── stm32f4xx_it.c
│   │   │
│   │   ├── app/
│   │   │   ├── app_main.c
│   │   │   ├── app_main.h
│   │   │   ├── app_control.c
│   │   │   ├── app_control.h
│   │   │   ├── app_motor.c
│   │   │   ├── app_motor.h
│   │   │   ├── app_encoder.c
│   │   │   ├── app_encoder.h
│   │   │   ├── app_pid.c
│   │   │   ├── app_pid.h
│   │   │   ├── app_kinematics.c
│   │   │   ├── app_kinematics.h
│   │   │   ├── app_odometry.c
│   │   │   ├── app_odometry.h
│   │   │   ├── app_imu.c
│   │   │   ├── app_imu.h
│   │   │   ├── app_comms.c
│   │   │   ├── app_comms.h
│   │   │   ├── app_protocol.c
│   │   │   ├── app_protocol.h
│   │   │   ├── app_safety.c
│   │   │   ├── app_safety.h
│   │   │   ├── app_calibration.c
│   │   │   └── app_calibration.h
│   │   │
│   │   ├── bsp/
│   │   │   ├── bsp_board.c
│   │   │   ├── bsp_board.h
│   │   │   ├── bsp_uart.c
│   │   │   ├── bsp_uart.h
│   │   │   ├── bsp_pwm.c
│   │   │   ├── bsp_pwm.h
│   │   │   ├── bsp_encoder.c
│   │   │   ├── bsp_encoder.h
│   │   │   ├── bsp_imu.c
│   │   │   ├── bsp_imu.h
│   │   │   ├── bsp_led.c
│   │   │   └── bsp_led.h
│   │   │
│   │   ├── config/
│   │   │   ├── robot_config.h
│   │   │   ├── motor_config.h
│   │   │   ├── encoder_config.h
│   │   │   ├── kinematics_config.h
│   │   │   └── comms_config.h
│   │   │
│   │   ├── middlewares/
│   │   │   └── README.md
│   │   │
│   │   ├── drivers/
│   │   │   └── README.md
│   │   │
│   │   ├── tests/
│   │   │   ├── test_kinematics.c
│   │   │   ├── test_pid.c
│   │   │   └── test_protocol.c
│   │   │
│   │   └── build/
│   │       ├── bin/
│   │       ├── hex/
│   │       └── elf/
│   │
│   ├── stm32f103_imu_gateway/
│   │   ├── cube/
│   │   │   └── stm32f103_imu_gateway.ioc
│   │   │
│   │   ├── core/
│   │   │   ├── Inc/
│   │   │   │   ├── main.h
│   │   │   │   ├── i2c.h
│   │   │   │   └── usart.h
│   │   │   └── Src/
│   │   │       ├── main.c
│   │   │       ├── i2c.c
│   │   │       └── usart.c
│   │   │
│   │   ├── app/
│   │   │   ├── app_main.c
│   │   │   ├── app_imu_reader.c
│   │   │   ├── app_imu_reader.h
│   │   │   ├── app_imu_calibration.c
│   │   │   ├── app_imu_calibration.h
│   │   │   ├── app_uart_gateway.c
│   │   │   ├── app_uart_gateway.h
│   │   │   ├── app_protocol.c
│   │   │   └── app_protocol.h
│   │   │
│   │   ├── bsp/
│   │   │   ├── bsp_uart.c
│   │   │   ├── bsp_uart.h
│   │   │   ├── bsp_i2c.c
│   │   │   ├── bsp_i2c.h
│   │   │   └── bsp_led.h
│   │   │
│   │   ├── config/
│   │   │   ├── imu_config.h
│   │   │   ├── uart_config.h
│   │   │   └── calibration_config.h
│   │   │
│   │   └── build/
│   │       ├── bin/
│   │       ├── hex/
│   │       └── elf/
│   │
│   └── tools/
│       ├── flash.sh
│       ├── serial_monitor.py
│       ├── send_cmd_vel.py
│       ├── read_odom.py
│       └── parse_protocol_log.py
│
├── external/                                  # Driver/thư viện bên thứ ba
│   ├── lidar_drivers/
│   │   └── README.md
│   ├── imu_drivers/
│   │   └── README.md
│   └── third_party/
│       └── README.md
│
├── ros2_ws/                                   # ROS 2 workspace
│   ├── README.md
│   │
│   ├── src/
│   │   │
│   │   ├── amr_description/                   # URDF, TF tĩnh, mô tả robot
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── urdf/
│   │   │   │   ├── amr.urdf.xacro
│   │   │   │   ├── amr_base.urdf.xacro
│   │   │   │   ├── amr_wheels.urdf.xacro
│   │   │   │   ├── amr_sensors.urdf.xacro
│   │   │   │   └── materials.xacro
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── robot_dimensions.yaml
│   │   │   │   ├── sensor_poses.yaml
│   │   │   │   └── wheel_params.yaml
│   │   │   │
│   │   │   ├── meshes/
│   │   │   │   ├── base_link.stl
│   │   │   │   ├── wheel.stl
│   │   │   │   ├── lidar.stl
│   │   │   │   └── imu.stl
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── description.launch.py
│   │   │   │   └── display.launch.py
│   │   │   │
│   │   │   ├── rviz/
│   │   │   │   └── amr_description.rviz
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_urdf.py
│   │   │
│   │   ├── amr_bringup/                       # Launch/config khởi động toàn hệ thống
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── robot.launch.py
│   │   │   │   ├── lidar.launch.py
│   │   │   │   ├── serial.launch.py
│   │   │   │   ├── localization.launch.py
│   │   │   │   ├── slam.launch.py
│   │   │   │   ├── navigation.launch.py
│   │   │   │   ├── full_mapping.launch.py
│   │   │   │   ├── full_navigation.launch.py
│   │   │   │   └── diagnostics.launch.py
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── robot.yaml
│   │   │   │   ├── serial.yaml
│   │   │   │   ├── lidar.yaml
│   │   │   │   ├── ekf.yaml
│   │   │   │   ├── slam_toolbox.yaml
│   │   │   │   ├── nav2_params.yaml
│   │   │   │   ├── safety.yaml
│   │   │   │   ├── diagnostics.yaml
│   │   │   │   └── teleop.yaml
│   │   │   │
│   │   │   ├── params/
│   │   │   │   ├── limits.yaml
│   │   │   │   ├── modes.yaml
│   │   │   │   └── startup.yaml
│   │   │   │
│   │   │   ├── scripts/
│   │   │   │   ├── preflight_check.py
│   │   │   │   └── env_check.sh
│   │   │   │
│   │   │   ├── rviz/
│   │   │   │   ├── mapping.rviz
│   │   │   │   └── navigation.rviz
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_launch_files.py
│   │   │
│   │   ├── amr_serial/                        # Node giao tiếp UART/USB với STM32
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── include/
│   │   │   │   └── amr_serial/
│   │   │   │       ├── serial_node.hpp
│   │   │   │       ├── serial_port.hpp
│   │   │   │       ├── protocol_parser.hpp
│   │   │   │       ├── packet_builder.hpp
│   │   │   │       ├── odom_builder.hpp
│   │   │   │       ├── imu_builder.hpp
│   │   │   │       └── status_builder.hpp
│   │   │   │
│   │   │   ├── src/
│   │   │   │   ├── serial_node.cpp
│   │   │   │   ├── serial_port.cpp
│   │   │   │   ├── protocol_parser.cpp
│   │   │   │   ├── packet_builder.cpp
│   │   │   │   ├── odom_builder.cpp
│   │   │   │   ├── imu_builder.cpp
│   │   │   │   └── status_builder.cpp
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── serial.yaml
│   │   │   │   ├── topics.yaml
│   │   │   │   └── protocol.yaml
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── serial.launch.py
│   │   │   │   └── serial_test.launch.py
│   │   │   │
│   │   │   └── test/
│   │   │       ├── test_protocol_parser.cpp
│   │   │       ├── test_packet_builder.cpp
│   │   │       └── test_serial_node.cpp
│   │   │
│   │   ├── amr_msgs/                          # Message/service tùy chỉnh
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── msg/
│   │   │   │   ├── WheelOdom.msg
│   │   │   │   ├── WheelCommands.msg
│   │   │   │   ├── McuStatus.msg
│   │   │   │   ├── PacketStatus.msg
│   │   │   │   ├── BatteryStatus.msg
│   │   │   │   └── SafetyStatus.msg
│   │   │   │
│   │   │   └── srv/
│   │   │       ├── ResetOdometry.srv
│   │   │       ├── CalibrateImu.srv
│   │   │       └── SetMaxSpeed.srv
│   │   │
│   │   ├── amr_localization/                  # EKF/fusion odometry
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── ekf.launch.py
│   │   │   │   └── ekf_debug.launch.py
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── ekf_odom_imu.yaml
│   │   │   │   ├── ekf_raw_only.yaml
│   │   │   │   └── covariance_defaults.yaml
│   │   │   │
│   │   │   ├── rviz/
│   │   │   │   └── localization_debug.rviz
│   │   │   │
│   │   │   ├── scripts/
│   │   │   │   └── check_ekf_tf.py
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_ekf_config.py
│   │   │
│   │   ├── amr_slam/                          # SLAM/mapping
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── slam_toolbox_async.launch.py
│   │   │   │   ├── slam_toolbox_sync.launch.py
│   │   │   │   ├── slam_toolbox_localization.launch.py
│   │   │   │   └── save_map.launch.py
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── slam_toolbox.yaml
│   │   │   │   ├── slam_toolbox_async.yaml
│   │   │   │   ├── slam_toolbox_sync.yaml
│   │   │   │   └── map_saver.yaml
│   │   │   │
│   │   │   ├── rviz/
│   │   │   │   └── slam.rviz
│   │   │   │
│   │   │   ├── scripts/
│   │   │   │   ├── save_map.sh
│   │   │   │   └── check_slam_tf.py
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_slam_config.py
│   │   │
│   │   ├── amr_navigation/                    # Nav2/AMCL/navigation
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── localization.launch.py
│   │   │   │   ├── navigation.launch.py
│   │   │   │   ├── nav2_full.launch.py
│   │   │   │   └── waypoint_following.launch.py
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── amcl_params.yaml
│   │   │   │   ├── nav2_params.yaml
│   │   │   │   ├── controller_server.yaml
│   │   │   │   ├── planner_server.yaml
│   │   │   │   ├── bt_navigator.yaml
│   │   │   │   ├── behavior_server.yaml
│   │   │   │   ├── recovery_server.yaml
│   │   │   │   ├── costmap_common_params.yaml
│   │   │   │   ├── global_costmap.yaml
│   │   │   │   └── local_costmap.yaml
│   │   │   │
│   │   │   ├── params/
│   │   │   │   └── navigation_modes.yaml
│   │   │   │
│   │   │   ├── scripts/
│   │   │   │   ├── send_goal.py
│   │   │   │   └── waypoint_follow.py
│   │   │   │
│   │   │   ├── rviz/
│   │   │   │   └── nav2.rviz
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_nav2_config.py
│   │   │
│   │   ├── amr_teleop/                        # Điều khiển bàn phím/gamepad
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── include/
│   │   │   │   └── amr_teleop/
│   │   │   │       ├── keyboard_teleop_node.hpp
│   │   │   │       ├── joy_teleop_node.hpp
│   │   │   │       └── teleop_limiter.hpp
│   │   │   │
│   │   │   ├── src/
│   │   │   │   ├── keyboard_teleop_node.cpp
│   │   │   │   ├── joy_teleop_node.cpp
│   │   │   │   └── teleop_limiter.cpp
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── keyboard_teleop.yaml
│   │   │   │   ├── joy_teleop.yaml
│   │   │   │   └── speed_limits.yaml
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── keyboard_teleop.launch.py
│   │   │   │   └── joy_teleop.launch.py
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_teleop_limiter.cpp
│   │   │
│   │   ├── amr_safety/                        # Node an toàn, giới hạn, watchdog
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── include/
│   │   │   │   └── amr_safety/
│   │   │   │       ├── safety_node.hpp
│   │   │   │       ├── cmd_vel_limiter.hpp
│   │   │   │       ├── watchdog.hpp
│   │   │   │       └── safety_state.hpp
│   │   │   │
│   │   │   ├── src/
│   │   │   │   ├── safety_node.cpp
│   │   │   │   ├── cmd_vel_limiter.cpp
│   │   │   │   ├── watchdog.cpp
│   │   │   │   └── safety_state.cpp
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── safety.yaml
│   │   │   │   └── limits.yaml
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   └── safety.launch.py
│   │   │   │
│   │   │   └── test/
│   │   │       ├── test_cmd_vel_limiter.cpp
│   │   │       └── test_watchdog.cpp
│   │   │
│   │   ├── amr_diagnostics/                   # Chẩn đoán hệ thống
│   │   │   ├── CMakeLists.txt
│   │   │   ├── package.xml
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── include/
│   │   │   │   └── amr_diagnostics/
│   │   │   │       ├── diagnostics_node.hpp
│   │   │   │       ├── topic_rate_checker.hpp
│   │   │   │       ├── tf_checker.hpp
│   │   │   │       └── system_checker.hpp
│   │   │   │
│   │   │   ├── src/
│   │   │   │   ├── diagnostics_node.cpp
│   │   │   │   ├── topic_rate_checker.cpp
│   │   │   │   ├── tf_checker.cpp
│   │   │   │   └── system_checker.cpp
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── diagnostics.yaml
│   │   │   │   └── thresholds.yaml
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   └── diagnostics.launch.py
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_topic_rate_checker.cpp
│   │   │
│   │   ├── amr_tools/                         # Tool tiện ích, script, checker
│   │   │   ├── package.xml
│   │   │   ├── setup.py
│   │   │   ├── setup.cfg
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── resource/
│   │   │   │   └── amr_tools
│   │   │   │
│   │   │   ├── amr_tools/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── save_map.py
│   │   │   │   ├── check_topics.py
│   │   │   │   ├── check_tf.py
│   │   │   │   ├── check_serial.py
│   │   │   │   ├── record_bag.py
│   │   │   │   └── health_check.py
│   │   │   │
│   │   │   ├── scripts/
│   │   │   │   ├── save_map.sh
│   │   │   │   ├── check_topics.sh
│   │   │   │   ├── check_tf.sh
│   │   │   │   └── health_check.sh
│   │   │   │
│   │   │   ├── config/
│   │   │   │   └── tools.yaml
│   │   │   │
│   │   │   └── test/
│   │   │       ├── test_check_topics.py
│   │   │       └── test_check_tf.py
│   │   │
│   │   ├── amr_simulation/                    # Mock/simulation khi chưa có phần cứng
│   │   │   ├── package.xml
│   │   │   ├── setup.py
│   │   │   ├── setup.cfg
│   │   │   ├── README.md
│   │   │   │
│   │   │   ├── resource/
│   │   │   │   └── amr_simulation
│   │   │   │
│   │   │   ├── amr_simulation/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── mock_mcu_node.py
│   │   │   │   ├── fake_lidar_node.py
│   │   │   │   ├── fake_imu_node.py
│   │   │   │   └── odom_noise_model.py
│   │   │   │
│   │   │   ├── launch/
│   │   │   │   ├── mock_robot.launch.py
│   │   │   │   └── replay_bag.launch.py
│   │   │   │
│   │   │   ├── config/
│   │   │   │   ├── mock_mcu.yaml
│   │   │   │   ├── fake_lidar.yaml
│   │   │   │   └── fake_imu.yaml
│   │   │   │
│   │   │   └── test/
│   │   │       └── test_mock_odom.py
│   │   │
│   │   └── amr_tests/                         # Test tích hợp/unit test ROS
│   │       ├── CMakeLists.txt
│   │       ├── package.xml
│   │       ├── README.md
│   │       │
│   │       ├── test/
│   │       │   ├── test_kinematics.cpp
│   │       │   ├── test_protocol.cpp
│   │       │   ├── test_odom_topics.py
│   │       │   ├── test_tf_tree.py
│   │       │   ├── test_scan_topic.py
│   │       │   └── test_cmd_vel_pipeline.py
│   │       │
│   │       ├── launch/
│   │       │   ├── integration_tests.launch.py
│   │       │   └── hardware_in_loop_tests.launch.py
│   │       │
│   │       ├── config/
│   │       │   └── test_params.yaml
│   │       │
│   │       └── scripts/
│   │           └── run_all_tests.sh
│   │
│   ├── build/                                 # colcon build tạo ra, không chỉnh tay
│   │   └── README.md
│   │
│   ├── install/                               # colcon install tạo ra, không chỉnh tay
│   │   ├── setup.bash
│   │   ├── lib/
│   │   └── share/
│   │
│   └── log/                                   # Log build ROS 2
│       └── README.md
│
├── deploy/                                    # Triển khai chạy thật trên Orange Pi
│   ├── systemd/
│   │   ├── amr-robot.service
│   │   ├── amr-slam.service
│   │   ├── amr-navigation.service
│   │   └── amr-diagnostics.service
│   │
│   ├── udev/
│   │   ├── 99-amr-mcu.rules
│   │   ├── 99-amr-lidar.rules
│   │   └── 99-amr-imu.rules
│   │
│   ├── scripts/
│   │   ├── start_robot.sh
│   │   ├── stop_robot.sh
│   │   ├── restart_robot.sh
│   │   ├── enable_services.sh
│   │   └── check_services.sh
│   │
│   ├── config/
│   │   ├── ros_env.sh
│   │   ├── dds_profile.xml
│   │   └── network.env
│   │
│   └── docker/
│       ├── Dockerfile
│       ├── docker-compose.yml
│       └── README.md
│
├── calibrations/                              # Hiệu chỉnh robot
│   ├── scripts/
│   │   ├── calibrate_wheel_radius.py
│   │   ├── calibrate_wheel_base.py
│   │   ├── calibrate_imu_bias.py
│   │   └── calibrate_lidar_tf.py
│   │
│   ├── profiles/
│   │   ├── robot_v1.yaml
│   │   └── robot_v2.yaml
│   │
│   └── results/
│       ├── wheel_calibration.yaml
│       ├── imu_calibration.yaml
│       └── lidar_calibration.yaml
│
├── maps/                                      # Bản đồ SLAM
│   ├── raw/
│   │   └── .gitkeep
│   ├── final/
│   │   └── .gitkeep
│   └── versions/
│       └── .gitkeep
│
├── missions/                                  # Waypoint/route cho navigation
│   ├── waypoints/
│   │   ├── example_waypoints.yaml
│   │   └── .gitkeep
│   └── routes/
│       ├── example_route.yaml
│       └── .gitkeep
│
├── bags/                                      # Dữ liệu rosbag để debug
│   ├── control_tests/
│   │   └── .gitkeep
│   ├── odom_tests/
│   │   └── .gitkeep
│   ├── slam_tests/
│   │   └── .gitkeep
│   └── navigation_tests/
│       └── .gitkeep
│
├── logs/                                      # Log runtime
│   ├── robot/
│   │   └── .gitkeep
│   ├── slam/
│   │   └── .gitkeep
│   ├── navigation/
│   │   └── .gitkeep
│   └── system/
│       └── .gitkeep
│
├── scripts/                                   # Script tiện ích mức dự án
│   ├── setup.sh
│   ├── build.sh
│   ├── run_mapping.sh
│   ├── run_navigation.sh
│   ├── save_map.sh
│   └── health_check.sh
│
└── ci/                                        # CI/CD nếu muốn chuyên nghiệp
    ├── lint.sh
    ├── build.sh
    └── test.sh
```
