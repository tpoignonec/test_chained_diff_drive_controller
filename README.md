# test_chained_diff_drive_controller

## Installation

```bash

mkdir ws_test_chained_diff_drive_controller
cd ws_test_chained_diff_drive_controller

git clone https://github.com/tpoignonec/test_chained_diff_drive_controller.git

mkdir external
vcs import external < test_chained_diff_drive_controller/test_chained_diff_drive_controller.repos

export EXTERNAL_DEPS=$(colcon list --base-paths ./external -n)
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Debug --allow-overriding $EXTERNAL_DEPS --packages-up-to test_chained_diff_drive_controller

source install/setup.bash
```

## Test chained diff drive


```bash
source install/setup.bash

ros2 launch test_chained_diff_drive_controller launch.py
ros2 control list_hardware_interfaces

ros2 control load_controller velocity_controller
ros2 control set_controller_state velocity_controller inactive
ros2 control set_controller_state velocity_controller active
ros2 control list_hardware_interfaces
```
