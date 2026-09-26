ros2_ws/
│
├── src/
│   │
│   ├── amr_description/               # Mô tả robot: URDF, TF static, mesh
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── urdf/
│   │   │   ├── amr.urdf.xacro        # File URDF chính
│   │   │   └── amr.ros2_control.xacro # Nếu sau này dùng ros2_control
│   │   ├── config/
│   │   │   ├── robot_dimensions.xacro # Kích thước xe, vị trí lidar, imu
│   │   │   └── materials.xacro        # Màu sắc nếu hiển thị RViz
│   │   ├── meshes/
│   │   │   ├── base_link.stl
│   │   │   ├── wheel.stl
│   │   │   └── lidar.stl
│   │   ├── launch/
│   │   │   └── description.launch.py  # Chạy robot_state_publisher
│   │   └── rviz/
│   │       └── amr_default.rviz       # Cấu hình RViz mặc định
│   │
│   ├── amr_bringup/                   # Package khởi động toàn bộ robot
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── launch/
│   │   │   ├── robot.launch.py        # Chạy serial, lidar, EKF, TF
│   │   │   ├── slam.launch.py         # Chạy SLAM
│   │   │   ├── localization.launch.py # Chạy EKF/robot_localization
│   │   │   ├── teleop.launch.py       # Chạy điều khiển tay
│   │   │   └── full.launch.py         # Chạy tất cả: robot + slam
│   │   ├── config/
│   │   │   ├── robot.yaml             # Thông số chung của robot
│   │   │   ├── serial.yaml            # Cấu hình cổng UART/USB STM32
│   │   │   ├── lidar.yaml             # Cấu hình LiDAR
│   │   │   ├── ekf.yaml               # Cấu hình robot_localization
│   │   │   ├── slam_toolbox.yaml      # Cấu hình SLAM
│   │   │   └── teleop.yaml            # Cấu hình teleop
│   │   └── params/
│   │       ├── robot_params.yaml      # Tham số runtime khác
│   │       └── safety_params.yaml     # Giới hạn vận tốc, timeout
│   │
│   ├── amr_serial/                    # Node giao tiếp UART/USB với STM32
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── include/
│   │   │   └── amr_serial/
│   │   │       ├── serial_node.hpp    # Class node ROS chính
│   │   │       ├── mcu_interface.hpp  # Giao tiếp MCU
│   │   │       ├── protocol_parser.hpp# Parse packet từ STM32
│   │   │       ├── odom_builder.hpp   # Dựng nav_msgs/Odometry
│   │   │       └── imu_builder.hpp    # Dựng sensor_msgs/Imu
│   │   ├── src/
│   │   │   ├── serial_node.cpp        # Node ROS chính
│   │   │   ├── mcu_interface.cpp      # Mở port, đọc/ghi serial
│   │   │   ├── protocol_parser.cpp    # Parse frame, CRC
│   │   │   ├── odom_builder.cpp       # Chuyển raw odom -> Odometry msg
│   │   │   └── imu_builder.cpp        # Chuyển raw IMU -> Imu msg
│   │   ├── launch/
│   │   │   └── serial.launch.py       # Launch riêng node serial
│   │   ├── config/
│   │   │   └── serial.yaml            # port, baudrate, topic name
│   │   └── test/
│   │       ├── test_parser.cpp        # Test parse packet
│   │       └── test_serial_node.py    # Test node nếu dùng Python
│   │
│   ├── amr_msgs/                      # Message tùy chọn, không bắt buộc
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── msg/
│   │   │   ├── WheelOdom.msg          # Odom từng bánh
│   │   │   ├── WheelCommands.msg     # Lệnh vận tốc 4 bánh
│   │   │   ├── McuStatus.msg          # Trạng thái MCU, lỗi, pin
│   │   │   └── PacketStatus.msg       # Trạng thái mất gói, CRC lỗi
│   │   └── srv/
│   │       ├── CalibrateImu.srv       # Service hiệu chỉnh IMU
│   │       └── ResetOdometry.srv      # Reset odom về 0
│   │
│   ├── amr_localization/              # Package chuyên cho EKF/fusion
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── launch/
│   │   │   └── ekf.launch.py          # Chạy robot_localization EKF
│   │   ├── config/
│   │   │   ├── ekf_odom_imu.yaml      # EKF wheel odom + IMU
│   │   │   └── ekf_debug.yaml         # EKF chế độ debug/log
│   │   └── rviz/
│   │       └── ekf_debug.rviz         # RViz xem odom raw/filtered
│   │
│   ├── amr_slam/                      # Package SLAM
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── launch/
│   │   │   ├── slam_toolbox.launch.py # Launch slam_toolbox
│   │   │   └── cartographer.launch.py # Nếu sau này dùng Cartographer
│   │   ├── config/
│   │   │   ├── slam_toolbox.yaml      # Tham số slam_toolbox
│   │   │   └── cartographer.lua       # Nếu dùng Cartographer
│   │   ├── rviz/
│   │   │   └── slam.rviz              # RViz cho SLAM
│   │   └── maps/
│   │       └── .gitkeep               # Giữ thư mục nếu dùng git
│   │
│   ├── amr_navigation/                # Package Nav2, dùng sau khi có map
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── launch/
│   │   │   ├── localization.launch.py # AMCL localization
│   │   │   ├── navigation.launch.py   # Nav2 navigation stack
│   │   │   └── nav2_full.launch.py    # Full navigation
│   │   ├── config/
│   │   │   ├── nav2_params.yaml       # Tham số Nav2
│   │   │   ├── amcl_params.yaml       # Tham số AMCL
│   │   │   └── costmap_common.yaml    # Cấu hình costmap
│   │   └── rviz/
│   │       └── nav2.rviz              # RViz cho navigation
│   │
│   ├── amr_teleop/                    # Điều khiển tay, đặc biệt cho omni
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── src/
│   │   │   └── omni_teleop_node.cpp   # Node điều khiển omni vx, vy, wz
│   │   ├── launch/
│   │   │   └── teleop.launch.py
│   │   └── config/
│   │       └── teleop.yaml            # Phím, max speed
│   │
│   ├── amr_tools/                     # Công cụ phụ trợ
│   │   ├── CMakeLists.txt
│   │   ├── package.xml
│   │   ├── scripts/
│   │   │   ├── save_map.py            # Script lưu bản đồ
│   │   │   ├── check_topics.py        # Kiểm tra topic cần thiết
│   │   │   ├── check_tf.py            # Kiểm tra TF tree
│   │   │   └── record_bag.sh          # Ghi bag để debug
│   │   └── launch/
│   │       └── diagnostics.launch.py  # Launch công cụ chẩn đoán
│   │
│   └── amr_tests/                     # Package test riêng
│       ├── CMakeLists.txt
│       ├── package.xml
│       ├── test/
│       │   ├── test_kinematics.cpp    # Test động học
│       │   ├── test_protocol.cpp      # Test packet/CRC
│       │   ├── test_odom_topics.py    # Test topic odom
│       │   └── test_tf_tree.py        # Test TF
│       └── launch/
│           └── run_tests.launch.py
│
├── build/                             # colcon tạo ra, không chỉnh tay
├── install/                           # colcon tạo ra, không chỉnh tay
└── log/                               # colcon tạo ra, không chỉnh ta
