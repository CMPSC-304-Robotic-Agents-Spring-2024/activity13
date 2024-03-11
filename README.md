# Activity 13: Turtlebot Teleop

## Turtlebot 4

You can learn about the hardware specifications of this robot in the [turtlebot4-hardware GitHub repository](https://github.com/turtlebot/turtlebot4-hardware). Please also review the features of this robot on [its website](https://turtlebot.github.io/turtlebot4-user-manual/overview/features.html).

### Teleop

In this activity, we will try to get connected and drive the robot using remote control, `teleop`. Please follow the steps below. Document your achievements and/or challenges in the `report.md`.

#### Getting Started

Get the turtlebot and the dock out of its box. Plug in the dock and place the turtlebot on the dock so that the two metal pieces on the bottom of the robot are connected to the two metal pieces on the charger. The robot should turn on with a flashing white light around the center power button. Once you hear two chimes (the second one will sound a little bit after the first) you are ready for the next steps!

While you are waiting for the robot to start up, get the router out and plug it in. Find a linux laptop for the turtlebot and connect the laptop to the router (name and password are on the router). Turtlebot should automatically connect to the router.

Now, either follow instructions on [Turtlebot Lite Section](#turtlebot-lite) or [Turtlebot Standard Section](#turtlebot-standard), depending on the robot your team has.

#### Turtlebot Lite

Follow instructions on [Driving your Turtlebot 4](https://turtlebot.github.io/turtlebot4-user-manual/tutorials/driving.html), which are also summarized below.

Please note that Turtlebot 4 Lite does not include Bluetooth Controller. So, in order to move your robot using remote control, you are going to use a keyboard application on your PC! `teleop` package should already be installed on turtlebot laptops, if not, run the following commands:

```
sudo apt update
sudo apt install ros-humble-teleop-twist-keyboard
```

Before doing the next part, you need to connect to the right robot by running the following command (`ROS_DOMAIN_ID` is noted on the robot): 

`export ROS_DOMAIN_ID={ROS_DOMAIN_ID}` 

Example:
`export ROS_DOMAIN_ID=1`

Now you should be able to set up your `teleop` keyboard and drive the turtlebot as follows:

```
source /opt/ros/humble/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

If this does not work, try the following command instead: `ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r __ns:=/tb2`

When you do this, you should see the following messages:

```
This node takes keypresses from the keyboard and publishes them
as Twist messages. It works best with a US keyboard layout.
---------------------------
Moving around:
   u    i    o
   j    k    l
   m    ,    .

For Holonomic mode (strafing), hold down the shift key:
---------------------------
   U    I    O
   J    K    L
   M    <    >

t : up (+z)
b : down (-z)

anything else : stop

q/z : increase/decrease max speeds by 10%
w/x : increase/decrease only linear speed by 10%
e/c : increase/decrease only angular speed by 10%

CTRL-C to quit

currently:	speed 0.5	turn 1.0 
```

As you can see above you use the following commands to move around:

```
U = Forward Left
I = Straight Forward
O = Forward Right
J = Rotate Left
K = Center # This doesn't really do anything
L = Rotate Right
M = Left Backwards
, = Straight Backwards
. = Right Backwards
```

#### Turtlebot Standard

Turtlebot Standard comes with a Bluetooth Controller. First, try to connect your controller to the robot. Press the home button on the controller and check that the controller's light turns blue. If the controller is not connecting, it is likely not paired. In that case:

1. Run the start up commands in the Linux laptop's terminal, replacing X with the correct domain id number:
```
source /opt/ros/humble/setup.bash
export ROS_DOMAIN_ID=X
```
2. Make sure you are connected to the wifi of the router on the laptop. To find the ip of the turtlebot, run:
`ros2 topic echo /ip`
3. Now, ssh into the turtlebot, replacing X's with the correct IP numbers (password is `turtlebot4`): 
`ssh ubuntu@192.168.1.XX`
4. Now, follow instructions in the [Controller Set Up Section](https://turtlebot.github.io/turtlebot4-user-manual/setup/basic.html#turtlebot-4-controller-setup)

To drive the robot with a controller, press and hold either `L1` or `R1`, and move the left joystick. By default, `L1` will drive the robot at "normal" speeds, and `R1` will drive the robot at "turbo" speeds. The buttons can be changed in the configuration file as described in the [Joystick Teleoperation Section](https://turtlebot.github.io/turtlebot4-user-manual/tutorials/driving.html).

