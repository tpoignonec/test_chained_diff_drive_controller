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

In a first terminal:

```bash
source install/setup.bash

ros2 launch test_chained_diff_drive_controller launch.py
```

In a second terminal:

```bash
source install/setup.bash
ros2 control list_hardware_interfaces

ros2 control load_controller velocity_controller
ros2 control set_controller_state velocity_controller inactive
ros2 control set_controller_state velocity_controller active
ros2 control list_hardware_interfaces
```

### Result with upstream master branch

```bash
# Do steps above
# Force cleanup ("CTRL + C" in first terminal)

[robot_state_publisher-2] [INFO] [1738844324.022658239] [rclcpp]: signal_handler(signum=2)
[ros2_control_node-1] [INFO] [1738844324.022919671] [controller_manager]: Shutting down controller 'velocity_controller'
[ros2_control_node-1] [INFO] [1738844324.023023885] [controller_manager]: Deactivating controller 'diff_drive_controller'
[ros2_control_node-1] [INFO] [1738844324.023093600] [controller_manager]: Shutting down controller 'diff_drive_controller'
[ros2_control_node-1] [INFO] [1738844324.023120345] [controller_manager]: Deactivating controller 'joint_state_broadcaster'
[ros2_control_node-1] [INFO] [1738844324.023224005] [controller_manager]: Shutting down controller 'joint_state_broadcaster'
[ros2_control_node-1] [INFO] [1738844324.023295506] [resource_manager]: 'deactivate' hardware 'DiffBot'
[ros2_control_node-1] [INFO] [1738844324.023306502] [resource_manager]: Successful 'deactivate' of hardware 'DiffBot'
[ros2_control_node-1] [INFO] [1738844324.023311607] [resource_manager]: 'shutdown' hardware 'DiffBot'
[ros2_control_node-1] [INFO] [1738844324.023314929] [resource_manager]: Successful 'shutdown' of hardware 'DiffBot'
[INFO] [robot_state_publisher-2]: process has finished cleanly [pid 21614]
[ros2_control_node-1] [INFO] [1738844324.023341414] [controller_manager]: Shutting down the controller manager.
[ros2_control_node-1] tcache_thread_shutdown(): unaligned tcache chunk detected
[ros2_control_node-1] Stack trace (most recent call last) in thread 21649:
[ros2_control_node-1] #8    Object "", at 0xffffffffffffffff, in
[ros2_control_node-1] #7    Source "../sysdeps/unix/sysv/linux/x86_64/clone3.S", line 78, in clone3 [0x7fda96e33c3b]
[ros2_control_node-1] #6    Source "./nptl/pthread_create.c", line 458, in start_thread [0x7fda96da6884]
[ros2_control_node-1] #5  | Source "./malloc/arena.c", line 897, in tcache_thread_shutdown
[ros2_control_node-1]       Source "./malloc/malloc.c", line 3231, in __malloc_arena_thread_freeres [0x7fda96db800b]
[ros2_control_node-1] #4    Source "./malloc/malloc.c", line 5772, in malloc_printerr [0x7fda96db2fe4]
[ros2_control_node-1] #3    Source "../sysdeps/posix/libc_fatal.c", line 132, in __libc_message_impl [0x7fda96d337b5]
[ros2_control_node-1] #2    Source "./stdlib/abort.c", line 79, in abort [0x7fda96d328fe]
[ros2_control_node-1] #1    Source "../sysdeps/posix/raise.c", line 26, in raise [0x7fda96d4f26d]
[ros2_control_node-1] #0  | Source "./nptl/pthread_kill.c", line 89, in __pthread_kill_internal
[ros2_control_node-1]     | Source "./nptl/pthread_kill.c", line 78, in __pthread_kill_implementation
[ros2_control_node-1]       Source "./nptl/pthread_kill.c", line 44, in __pthread_kill [0x7fda96da8b1c]
[ros2_control_node-1] Aborted (Signal sent by tkill() 21613 1000)
[ERROR] [ros2_control_node-1]: process has died [pid 21613, exit code -6, cmd '/home/tpo/dev/ros2_workspaces/ws_fix_chained_diff_drive/install/controller_manager/lib/controller_manager/ros2_control_node --ros-args --params-file /home/tpo/dev/ros2_workspaces/ws_fix_chained_diff_drive/install/test_chained_diff_drive_controller/share/test_chained_diff_drive_controller/config/controllers.yaml'].
```

### Result with branch tpo/fix_reference_chained_diff_drive

```bash
# Do steps above
# Force cleanup ("CTRL + C" in first terminal)

```
