# HW

# 10. Add/More/Del
## 1
## Screenshot of Fast_Food
<img width="607" alt="Screenshot 2024-04-18 at 9 15 02 PM" src="https://github.com/afifac/HW/assets/143447815/4146d44f-93df-42ac-8c00-704c27f6b7fe">

## 2
Add a model using rosrun gazebo_ros spawn_model. Rotate the model by 45 degrees about the z axis (yaw), and by 90 degrees about the x axis (roll)
## Screenshot of Cafe_Table
<img width="433" alt="Screenshot 2024-04-18 at 9 16 49 PM" src="https://github.com/afifac/HW/assets/143447815/85c1ec54-caab-4a5d-803a-cbbea326a182">

## Code of rotated Cafe_Table
roslaunch gazebo_ros empty_world.launch
rosrun gazebo_ros spawn_model -h
rosrun gazebo_ros spawn_model -file ~/.gazebo/models/cafe_table/model.sdf -sdf -model cafe_table_1 -R 1.57080 -Y 0.785398

## 3
Add some "snow" to gazebo, then spawn a Husky in the world. Drive the Husky through the "snow".
## Code
Terminal 1: roslaunch husky_gazebo empty_world.launch
Terminal 2: python3 ~/Desktop/snowy_husky_world.py

## Python Script snowy_husky_world.py
#!/usr/bin/env python
import rospy
import model_launcher as ml
import numpy as np

# Initialize the ROS node
rospy.init_node('snowy_husky_world', anonymous=True)

# Snow simulation parameters
num_snowflakes = 100
snowflake_spawn_height = 14  # meters above the ground

# Dictionary to store snowflake models
snowflakes = {}

for i in range(num_snowflakes):
    # Randomize size and origin of each snowflake
    dim = np.random.uniform(0.002, 0.01)  # Smaller range for more realistic snowflakes
    x = np.random.uniform(-10, 10)  # Snowflakes spawn within a 20x20 meter area
    y = np.random.uniform(-10, 10)
    
    # Launch each snowflake in Gazebo
    snowflakes[f'snowflake_{i}'] = ml.launcher(
        objectType='box',
        gazeboModelName=f'snowflake_{i}',
        namespace='snow',
        modelYawOffsetRad=0,
        x=x, y=y, z=snowflake_spawn_height,
        rollRad=0, pitchRad=0, yawRad=0,
        args={
            'color_r': 1.0, 'color_g': 1.0, 'color_b': 1.0,
            'dim_x': dim, 'dim_y': dim, 'dim_z': dim,
            'useGravity': True
        }
    )
#Launch Husky in an empty world
roslaunch_command = "roslaunch husky_gazebo husky_empty_world.launch"
rospy.loginfo("Launching Husky in a snowy environment...")
os.system(roslaunch_command)

## Screenshots of Snow & Husky
### Screenshot with Teleop
<img width="619" alt="Screenshot 2024-04-18 at 9 22 01 PM" src="https://github.com/afifac/HW/assets/143447815/c066fe8a-e745-41dc-9ead-2b7b217c0ce9">

### Screenshot up close with snow and Husky
<img width="616" alt="Screenshot 2024-04-18 at 9 23 05 PM" src="https://github.com/afifac/HW/assets/143447815/1ab4f4b2-ca91-46bf-9eae-18f5db2b5aea">

### List all of the ways that you can make the Husky move

### To move around
Manual movement: rosrun teleop_twist_keyboard teleop_twist_keyboard.py 

### In Python
rostopic pub /husky_velocity_controller/cmd_vel geometry_msgs/Twist "linear:
  x: 1.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0" -r 10

# 11 roslibjs (ROS + JavaScript/HTML)
## List of your observations (sentence, watch tutorials )
