# Midterm


## Week 4

***Contents***
- Working with Turtlesim
- ROS2 & RQT
- Understanding the Basic Concepts
- Colcon
- Creating a workspace
- Creating a package

### 1. Working with Turtlesim

**1.1. Turtlesim Installation**

- To make sure the system is up-to-date
```
sudo apt update 
```
- To install the turtlesim library
```
sudo apt install ros-rolling-turtlesim
```

**1.2. Starting Turtlesim**
```
ros2 run turtlesim turtlesim_node
```

***This command opens up a simulator windows with a random turtle in the center.***

![#2](https://user-images.githubusercontent.com/113494159/192174251-2b255c6e-c634-4acd-9558-6f4a582fd2f1.png)


**1.3. Using Turtlesim**
- The following command is entered in one terminal to control the turtle. 
```
ros2 run turtlesim turtle_teleop_key
```
- Once executed, there should be 3 windows: a terminal running `turtlesim_node`, a terminal running `turtle_teleop_key` and the turtlesim windows.
- We can use the arrow keys on the keyboard to control the direction/movement of the turtle and the path of movement is visible using its attached pen. 

![Turtle](https://user-images.githubusercontent.com/113494159/192175725-eb5d828f-26ec-4c09-a78f-e56ed36dec44.png)

### 2. ROS2 & RQT

**2.1. Installing rqt**

_In the new terminal, codes for installing `rqt` and its plugins are executed:_

```
sudo apt install

sudo apt install ~nros-rolling-rqt*
```
_In order to run rqt, we simply execute `rqt` in the terminal._

```
rqt
```

**2.1.1. Starting rqt Console**

_rqt_console is a GUI tool used to introspect log messages in ROS2._
```
ros2 run rqt_console rqt_console
```

![#4](https://user-images.githubusercontent.com/113494159/192157362-ff19aa73-21f4-4dd0-8269-9eadd3180303.png)



**2.2. Use rqt**

_Once rqt command is initialized, a blank window is popped up. We have to select **Plugins > Services > Service Caller** from the menu bar at the top._

![#3](https://user-images.githubusercontent.com/113494159/192157358-b07e4bb3-2891-4b0f-8369-ff4241ee19ac.png)

_By clicking on the **Service** dropdown list, we can see the various turtlesim's services, among which we willl be doing two services here as follows:_

**2.2.1. Trying the spawn service**

First of all, we can use rqt to call the `/spawn` service which will create another turtle in the turtlesim window.

We can provide unique name to the turtle, for example here `Sudip` from the **Expression** column and also we have to provided certain coordinates for the turtle to spawn , like `x=5.9` and `y=3.0` as shown in the image below. 

![#5](https://user-images.githubusercontent.com/113494159/192176295-2c9a0cf5-2442-4835-a402-482695e1b519.png)


**2.2.2. Trying the set-pen service**

This service is used to give the turtle it's unique color and width of pen while it moves by using `/set_pen` service.

The value for `r`, `g`, `b` can be set anywhere between 0 and 255 which will set the color of the pen and the `width` gives the thickness of the line.

![image](https://user-images.githubusercontent.com/113494159/195586596-e84297f4-0d50-4e46-b481-a1d4e89ccf0e.png)

_Here in this first image, **r** is set to 255 and others are 0 so the line is **red** and in the second image its the same case but **b** is set to 255 and others are 0 so the line is **blue** instead of red. _ 

![image](https://user-images.githubusercontent.com/113494159/195586769-9f521316-cdb0-4e8d-87cc-542f3a927ea7.png)



**2.3. Remapping**

Remapping is used when we have to move the second turtle as well. We can do that by remapping turtle1's `cmd_vel` topic onto second turtle. 

In the new terminal, we have to source ROS2 and run the following command:

```
ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel
```

Now we can move second turtle when this terminal is active and turtle1 when the other terminal running the `turtle_teleop_key` is active.


**2.4. Close turtlesim**

In order to stop the simulation, `Ctrl + C` will do the task or press `q` in the teleop terminal.


### 3. Understanding the Basic concepts
- ROS2 Nodes
- ROS2 Topics
- ROS2 Services
- ROS2 Parameters
- ROS2 Actions


### 4. ROS2 Colcon

**4.1. Installing Colcon**
```
sudo apt install python3-colcon-common-extensions
```


**4.2. Breifing on ROS Workspace**


- ROS Workspace is the directory having a particular structure and by default it create the following directories : `src`, `build`, `install` and `log`.
- **build** directory stores intermediate files. 
- **install** directory is where the packages are installed.
- **log** directory stores various logging information


### 5. Creating a Workspace


**5.1. Firstly, we need to create a directory to contain our workspace and the directory is named: `ros2_ws`**


```
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

_This will create a workspace which contains a single empty directory `src`. So we need to add some sources_

```
git clone https://github.com/ros2/examples src/examples -b foxy
```
_Now the workspace have source code to the ROS 2 examples._

**5.2. Building the Workspace**


**In the root of the workspace, we run the `colcon build`. After the build is finished, we can see 3 more directories: `build`, `install`, and `log`.**

```
colcon build --symlink-install
```

**5.3. Running Tests**
```
colcon test
```

**5.4. Source the Environment**

It is a important before we can run executables built by colcon. 

```
. install/setup.bash
```


### 6. Creating a Package

**6.1. What is a ROS2 package? **

_It can be considered as a container for ROS2 codes which has their own minimum required contents. Since we are using python here, it should have `package.xml`, `setup.py`, `setup.cfg` and `/<package_name>`.


Before running package creation command, it is important to be in the `src` folder. 

```
cd ~/ros2_ws/src
```

**Package creation command:**

```
ros2 pkg create --build-type ament_python --node-name my_node my_package
```

This will create a package named `my_package`.

We can see the following message from our terminal:


```python
going to create a new package
package name: my_package
destination directory: /home/user/ros2_ws/src
package format: 3
version: 0.0.0
description: TODO: Package description
maintainer: ['<name> <email>']
licenses: ['TODO: License declaration']
build type: ament_python
dependencies: []
node_name: my_node
creating folder ./my_package
creating ./my_package/package.xml
creating source folder
creating folder ./my_package/my_package
creating ./my_package/setup.py
creating ./my_package/setup.cfg
creating folder ./my_package/resource
creating ./my_package/resource/my_package
creating ./my_package/my_package/__init__.py
creating folder ./my_package/test
creating ./my_package/test/test_copyright.py
creating ./my_package/test/test_flake8.py
creating ./my_package/test/test_pep257.py
creating ./my_package/my_package/my_node.py
```



## Week 5

***Contents***
- Writing a simple publisher and subscriber using python
- Writing a simple service and client using python
- Creating custom msg and srv files
- Implementing custom interfaces

### 1. Writing a simple publisher and subscriber

**1.1. Creating a new package**

_Initially we have to source the ros2 installation so that `ros2` commands will work._
As we know, packages should be created in the `src` directory, so we need to navigate to `ros2_ws/src` in order to run the package creation command.

```
ros2 pkg create --build-type ament_python py_pubsub
```

The verification of package `py_pubsub`creation is returned by the terminal.


**1.2. Writing the publisher node**

To write the publisher node, we navigate to `ros2_ws/src/py_pubsub/py_pubsub` and using the following command, we can download the example talker code.

```
wget https://raw.githubusercontent.com/ros2/examples/foxy/rclpy/topics/minimal_publisher/examples_rclpy_minimal_publisher/publisher_member_function.py
```

Now there will be a new file named `publisher_member_function.py` adjacent to `__init__.py`

If we open that file, we can see the following code:

```python
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello World: %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
    
 ```

**1.2.1. Adding Dependencies**

We need to add dependencies to `package.xml`, so we have to navigate to `ros2_ws/src/py_pubsub` where the `setup.py`, `setup.cfg` and `package.xml` have been created.

Firstly, we have to fill up the `<description`, `<maintainer>`, `<maintainer_email` and `<license>` as follows:
and add the following dependencies:

```python
<exec_depend>rclpy</exec_depend>
<exec_depend>std_msgs</exec_depend>
```

![image](https://user-images.githubusercontent.com/113494159/195645586-bcebf491-fc91-4cfd-bc74-6bf757647473.png)


**1.2.2. Adding an entry point**

To add the entry point, we have to open the `setup.py` file and match the `<description`, `<maintainer>`, `maintainer_email` and `<license>`.

![image](https://user-images.githubusercontent.com/113494159/195647671-d0832ac9-2b70-4241-9099-d15be0878be3.png)


After that, it is needed to add the following lines within the `console_scripts` brackets of the `entry_points` fields.

```python
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
        ],
},
```
It is important to `save` everytime you edit. 


**_The contents inside `setup.cfg` is correctly populated automatically so we dont have to change anything inside. _**


**1.3. Writing the subscriber node**

To write the subscriber node, we have to navigate to `ros2_ws/src/py_pubsub/py_pubsub` in order to create the next node. For that, we have to enter the following commands:

```
wget https://raw.githubusercontent.com/ros2/examples/foxy/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py
```

Once the code is executed, the directory should have 3 files: `__init.py__`, `publisher_member_function.py` and `subscriber_member_function.py`.

And opening `subscriber_member_function.py` gives the following code:

```python
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            String,
            'topic',
            self.listener_callback,
            10)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('I heard: "%s"' % msg.data)


def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_subscriber.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
    
 ```
 
**1.3.1. Additing an entry point**

As we did previously for publisher, this time we need to add the entry point for subscriber from `setup.py` just below the publisher's entry point.

```python
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
                'listener = py_pubsub.subscriber_member_function:main',
        ],
},
```

Click **save** after that.


**1.4. Building and running** 

*Running rosdep to check on missing dependencies if any.*

```
rosdep install -i --from-path src --rosdistro foxy -y
```

Still in the root of your workspace, ros2_ws, build your new package:

```
colcon build --packages-select py_pubsub
```

After that, navigate to `ros2_ws` and source the setup files in the new terminal. 

```
. install/setup.bash
```
Let's run the talker code now.
```
ros2 run py_pubsub talker
```

After that we need to open the new terminal and source the configuration files from `ros2_ws` once more and then launch the listener node:

```
ros2 run py_pubsub listener
```

Starting at the publisher's current message count, the listener will begin writing messages to the console as follows:

![#4TalkerNode](https://user-images.githubusercontent.com/113494159/194862438-f62e8d96-58f5-4c4d-831d-dd5463b6c027.png)

![#5ListenerNode](https://user-images.githubusercontent.com/113494159/194862451-7c83a8dc-f455-4218-ad13-fa19f0a5adc7.png)


**_Ctrl + C will stop the nodes_**


### 2. Writing a simple service and client using Python

**2.1. Creating a Package**

As we have done several times now, all the packages are created in `src` directory so we navigate there and enter the following commands:

```
ros2 pkg create --build-type ament_python py_srvcli --dependencies rclpy example_interfaces
```

**2.1.1. Updating `package.xml`**

_As always we need to add the, `<description`, `<maintainer>`, `<maintainer_email` and `<license>` informations to `package.xml`_


**2.1.2. Updating `setup.py`**

_Same informations of  `<description`, `<maintainer>`, `<maintainer_email` and `<license>` are added to `setup.py` as well._


**2.2. Writing the Service Node**

Firstly, we navigate to `ros2_ws/src/py_srvcli/py_srvcli` directory and create a new file there named `service_member_function.py` and paste the following codes:

```python
from example_interfaces.srv import AddTwoInts

import rclpy
from rclpy.node import Node


class MinimalService(Node):

    def __init__(self):
        super().__init__('minimal_service')
        self.srv = self.create_service(AddTwoInts, 'add_two_ints', self.add_two_ints_callback)

    def add_two_ints_callback(self, request, response):
        response.sum = request.a + request.b
        self.get_logger().info('Incoming request\na: %d b: %d' % (request.a, request.b))

        return response


def main(args=None):
    rclpy.init(args=args)

    minimal_service = MinimalService()

    rclpy.spin(minimal_service)

    rclpy.shutdown()


if __name__ == '__main__':
    main()
    
```

**2.2.1. Adding the entry point**
For the ros2 run command to be able to run your node, the entry point must be added to `setup.py` (located in the `ros2 ws/src/py srvcli` directory).

In between the "console scripts" brackets, the following line should be added:
```
'service = py_srvcli.service_member_function:main',
```


**2.3. Writing the Client Node**
In the `ros2_ws/src/py srvcli/py_srvcli` directory, a new file called `client_member_function.py` is needed to create and then paste the following code inside:

```python
import sys

from example_interfaces.srv import AddTwoInts
import rclpy
from rclpy.node import Node


class MinimalClientAsync(Node):

    def __init__(self):
        super().__init__('minimal_client_async')
        self.cli = self.create_client(AddTwoInts, 'add_two_ints')
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        self.req = AddTwoInts.Request()

    def send_request(self, a, b):
        self.req.a = a
        self.req.b = b
        self.future = self.cli.call_async(self.req)
        rclpy.spin_until_future_complete(self, self.future)
        return self.future.result()


def main(args=None):
    rclpy.init(args=args)

    minimal_client = MinimalClientAsync()
    response = minimal_client.send_request(int(sys.argv[1]), int(sys.argv[2]))
    minimal_client.get_logger().info(
        'Result of add_two_ints: for %d + %d = %d' %
        (int(sys.argv[1]), int(sys.argv[2]), response.sum))

    minimal_client.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
 ```

**2.3.1. Adding an entry point**

Similar to how the service node needs an entry point, the client node also needs one.

The entry points column in your `setup.py` file must be formatted as follows:

```
entry_points={
    'console_scripts': [
        'service = py_srvcli.service_member_function:main',
        'client = py_srvcli.client_member_function:main',
    ],
},
```
![image](https://user-images.githubusercontent.com/113494159/194865968-9fb3a440-7461-4547-b41b-80e4a7ad0a21.png)


**2.4. Build and Run**

*Running rosdep to check if any dependencies missing.*

```
rosdep install -i --from-path src --rosdistro foxy -y
```

Navigate back, `ros2_ws`, and build your new package: (All the new packages are built here:)

```
colcon build --packages-select py_srvcli
```
![#5Building_new_package](https://user-images.githubusercontent.com/113494159/194867315-550e45fb-149d-4690-898d-ef3bc1130c1b.png)


Open a new terminal, navigate to `ros2_ws`, and source the setup files:

```
. install/setup.bash
```

Now run the service node:

```
ros2 run py_srvcli service
```

The node will watch for the client's request.

Similarly, in another terminal, source the setupfiles inside `ros2_ws` and start the client node, any two integers, and a space between them.

```
ros2 run py_srvcli client 2 3
```
![#6ServiceNode](https://user-images.githubusercontent.com/113494159/194867406-4de23191-a13e-489e-b3f5-928245106f6c.png)


The client would get a response like this if you selected options 2 and 3 as an example:

```
[INFO] [minimal_client_async]: Result of add_two_ints: for 2 + 3 = 5
```
 As you can see, it published the following log statements after receiving the request:

```
[INFO] [minimal_service]: Incoming request
a: 2 b: 3
```
![#6ClientNode](https://user-images.githubusercontent.com/113494159/194867428-76a74465-1b61-4374-9e2f-b7835f307b70.png)


### 3. Creating custom msg and srv files

**3.1. Create a new package**

Firstly, we run the package creation command by going to `ros2_ws/src`:

```
ros2 pkg create --build-type ament_cmake tutorial_interfaces
```

_The terminal will display a message confirming the establishment of your package tutorial interfaces and every file and folder it needs._

It is best practice to keep the .msg and .srv files separated within a package. So, now we create the directories in the `ros2_ws/src/turorial_interfaces`.

```
mkdir msg

mkdir srv
```

**3.2. Create custom definitions**

**3.2.1. msg definition**

In the `tutorial_interfaces/msg` directory which is just created, we make a new file named `Num.msg`, and then add a single line of code describing the data structure in Num.msg:

```
int64 num
```

This custom message transmits the 64-bit integer num, which is one single value.

Similarly, we make a new file named `Sphere.msg` in the same directory, `tutorial_interfaces/msg`, and the following codes are added. 

```
geometry_msgs/Point center
float64 radius
```

This custom message makes use of a message from a different message package (in this case, geometry msgs/Point).

![image](https://user-images.githubusercontent.com/113494159/194868003-fcef064a-447a-4f70-8be6-389deeeecd30.png)


**3.2.2. srv definition**
Back in the `tutorial_interfaces/srv`, directory, a new file is created named: `AddThreeInts.srv` with the following request and following response structure. 

```
int64 a
int64 b
int64 c
---
int64 sum

```

This is a custom service that accepts three integers with names a, b, and c and returns an answer with the integer sum.

![image](https://user-images.githubusercontent.com/113494159/194868086-e98a6ffa-d593-4a55-a561-766f604fb2c8.png)


**3.3. `CMakeLists.txt`**

In order to convert the interfaces defined into language specific code such as C++ and Python so they may be used in those languages, we need to add the following lines to `CMakeLists.txt`:

```
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Num.msg"
  "msg/Sphere.msg"
  "srv/AddThreeInts.srv"
  DEPENDENCIES geometry_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
)
```

**3.4. `package.xml`**

To package.xml, these lines should be added.
```
<depend>geometry_msgs</depend>

<build_depend>rosidl_default_generators</build_depend>

<exec_depend>rosidl_default_runtime</exec_depend>

<member_of_group>rosidl_interface_packages</member_of_group>
```

**3.5. Build the `tutorial_interfaces` package**

Now that all of the pieces of the custom interfaces package are in place, it can be build. We can run the following command in the workspace's root directory `(/ros2 ws)`:
```
colcon build --packages-select tutorial_interfaces
```

Now, the interfaces will be discoverable by other ROS 2 programs.


**3.6. Confirm msg and srv creation**

To source it in a new terminal, we need to issue the following command from within the workspace `(ros2 ws)`:

```
. install/setup.bash
```

The ros2 interface show command can now be used to verify that your interface creation was successful:

```
ros2 interface show tutorial_interfaces/msg/Num
```

& it should return
```
int64 num
```
&
```
ros2 interface show tutorial_interfaces/msg/Sphere
```
should return
```
geometry_msgs/Point center
float64 radius
```

&
```
ros2 interface show tutorial_interfaces/srv/AddThreeInts
```

& it should return
```
int64 a
int64 b
int64 c
---
int64 sum
```
![#7ConfirmMsg](https://user-images.githubusercontent.com/113494159/194868448-413c079b-e17e-4683-9dfa-c9c384fd5068.png)


**3.6. Test the new interfaces**

For this step, we use the packages you created in the prior stages. By making a few simple adjustments to the nodes, CMakeLists, and package files, we can use the new interfaces.


**3.6.1. Testing `Num.msg` with pub/sub**

`Publisher`:

```python
import rclpy
from rclpy.node import Node

from tutorial_interfaces.msg import Num    # CHANGE


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(Num, 'topic', 10)     # CHANGE
        timer_period = 0.5
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = Num()                                           # CHANGE
        msg.num = self.i                                      # CHANGE
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%d"' % msg.num)  # CHANGE
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

`Subscriber`:

```python
import rclpy
from rclpy.node import Node

from tutorial_interfaces.msg import Num        # CHANGE


class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            Num,                                              # CHANGE
            'topic',
            self.listener_callback,
            10)
        self.subscription

    def listener_callback(self, msg):
            self.get_logger().info('I heard: "%d"' % msg.num) # CHANGE


def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    minimal_subscriber.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

`CMakeLists.txt`:


Add the following lines (C++ only):

```C++
#...

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tutorial_interfaces REQUIRED)                         # CHANGE

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp tutorial_interfaces)         # CHANGE

add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp tutorial_interfaces)     # CHANGE

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME})

ament_package()
```
`package.xml`:

_Add the following line:_

```
<exec_depend>tutorial_interfaces</exec_depend>
```

Build the package after making the aforementioned alterations and saving all the modifications:

```
colcon build --packages-select py_pubsub
```


Then we open two new terminals, source ros2_ws in each, and run:

```
ros2 run py_pubsub talker
```


Instead of broadcasting strings as Num.msg only relays an integer, the talker should only be publishing integer values:
```
[INFO] [minimal_publisher]: Publishing: '0'
[INFO] [minimal_publisher]: Publishing: '1'
[INFO] [minimal_publisher]: Publishing: '2'
```

![#8Talker](https://user-images.githubusercontent.com/113494159/194868620-addeee33-2314-45f6-888d-4269ad51e013.png)
![#8Listener](https://user-images.githubusercontent.com/113494159/194868642-8420b022-b72c-4a1c-b58d-dbd178af6370.png)


**3.6.2. Testing `AddThreeInts.srv` with service/client**

By making a few small changes to the service/client package created in a previous tutorial (in C++ or Python), we may utilize AddThreeInts.srv. Here, we will be changing from the initial two integer request srv to a three integer request srv, which will have a big impact on the result.

`Service`:

```python
from tutorial_interfaces.srv import AddThreeInts     # CHANGE

import rclpy
from rclpy.node import Node


class MinimalService(Node):

    def __init__(self):
        super().__init__('minimal_service')
        self.srv = self.create_service(AddThreeInts, 'add_three_ints', self.add_three_ints_callback)        # CHANGE

    def add_three_ints_callback(self, request, response):
        response.sum = request.a + request.b + request.c                                                  # CHANGE
        self.get_logger().info('Incoming request\na: %d b: %d c: %d' % (request.a, request.b, request.c)) # CHANGE

        return response

def main(args=None):
    rclpy.init(args=args)

    minimal_service = MinimalService()

    rclpy.spin(minimal_service)

    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

`Client`:

```python
from tutorial_interfaces.srv import AddThreeInts       # CHANGE
import sys
import rclpy
from rclpy.node import Node


class MinimalClientAsync(Node):

    def __init__(self):
        super().__init__('minimal_client_async')
        self.cli = self.create_client(AddThreeInts, 'add_three_ints')       # CHANGE
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        self.req = AddThreeInts.Request()                                   # CHANGE

    def send_request(self):
        self.req.a = int(sys.argv[1])
        self.req.b = int(sys.argv[2])
        self.req.c = int(sys.argv[3])                  # CHANGE
        self.future = self.cli.call_async(self.req)


def main(args=None):
    rclpy.init(args=args)

    minimal_client = MinimalClientAsync()
    minimal_client.send_request()

    while rclpy.ok():
        rclpy.spin_once(minimal_client)
        if minimal_client.future.done():
            try:
                response = minimal_client.future.result()
            except Exception as e:
                minimal_client.get_logger().info(
                    'Service call failed %r' % (e,))
            else:
                minimal_client.get_logger().info(
                    'Result of add_three_ints: for %d + %d + %d = %d' %                               # CHANGE
                    (minimal_client.req.a, minimal_client.req.b, minimal_client.req.c, response.sum)) # CHANGE
            break

    minimal_client.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

`Package.xml`:

Add the following line:
```
<exec_depend>tutorial_interfaces</exec_depend>
```
After making the above edits and saving all the changes, build the package:

```
colcon build --packages-select py_srvcli
```

Then open two new terminals, source ros2_ws in each, and run:

```
ros2 run py_srvcli service

```
![#9Testing2](https://user-images.githubusercontent.com/113494159/194869065-deb540af-f75c-4daa-a16f-341e0b3adae4.png)


```
ros2 run py_srvcli client 2 3 1

```
![#9Testing](https://user-images.githubusercontent.com/113494159/194869081-a2beb249-050b-4d97-a7fd-ed927e9090fe.png)



## Week 6

***Contents***
- Managing Dependencies with rosdep
- Creating an action
- Writing an action server and client
- Composing multiple nodes in a single process
- Creating a launch file
- Integrating launch files into ROS2 packages
- Using Substitutions
- Using Event Handlers

### 1.Managing Dependencies with rosdep

**What is rosdep?**

_`rosdep` is ROS's dependency management utility that can work with ROS packages and external libraries and `rosdep` is a command-line utility for identifying and installiing dependencies to build or install a package._

**Use of rosdep tool**

```
sudo rosdep init
rosdep update
```

The given command is used to initialize rosdep and update it to get the latest index.

After that, we can run `rosdep install` to install dependencies. (All)

In order to install dependencies in the root of the workspace with directory `src`, 

```
rosdep install --from-paths src -y --ignore-src
```

### 2.Creating an action

In order to create an action, we should have ROS2 and colcon installed which we already installed previosly. 

Firstly, we have to source the ROS2 installation before doing other tasks.

**2.1. Defining an action**

Actions are defined in `.action` files and is made up of three message definitions: **Request**, **Result**, and **Feedback** which are separated by `---`.

Here , lets take a situation of defining a new action **"Fibonacci"** for computing _Fibonacci sequence_. 

An `action` directory is created in `action_tutorials_interfaces` package:

```
cd action_tutorials_interfaces
mkdir action
```

After that, within `action` directory, we created a file named: `Fibonacci.action` with the following contents:

```
int32 order
---
int32[] sequence
---
int32[] partial_sequence
```

**2.2. Building an action**

We must pass the definition to the rosidl code to use the new `Fibonacci action` in our code. For that purpose, we should add the following lines to our `CMakeLists.txt` before the `ament_package()` line in the `action_tutorials_interfaces`.

```
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "action/Fibonacci.action"
)
```

And the following dependencies are added to `package.xml`:

```
<buildtool_depend>rosidl_default_generators</buildtool_depend>

<depend>action_msgs</depend>

<member_of_group>rosidl_interface_packages</member_of_group>
```

After all these, we will be able to build the package containing the `Fibonacci` action definition as follows:

```
# Change to the root of the workspace
cd ~/ros2_ws
# Build
colcon build
```

### 3.Writing an action server and client

**3.1. Writing an Action Server**

Here, were create a new file named: `fibonacci_action_server.py` in the home directory and added the following code:

```python
import rclpy
from rclpy.action import ActionServer
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionServer(Node):

    def __init__(self):
        super().__init__('fibonacci_action_server')
        self._action_server = ActionServer(
            self,
            Fibonacci,
            'fibonacci',
            self.execute_callback)

    def execute_callback(self, goal_handle):
        self.get_logger().info('Executing goal...')
        result = Fibonacci.Result()
        return result


def main(args=None):
    rclpy.init(args=args)

    fibonacci_action_server = FibonacciActionServer()

    rclpy.spin(fibonacci_action_server)


if __name__ == '__main__':
    main()
```

Once done, we **save** the file and run the action server:

```
python3 fibonacci_action_server.py
```

After that, in another terminal, we use the command line interface to send a goal as follows:
```
ros2 action send_goal fibonacci action_tutorials_interfaces/action/Fibonacci "{order: 5}"
```

**3.1.1. Publishing Feedback**

_We can make our action server publish feedback for action clients by calling the goal handle's **publsih_feedback()** method._

After replacing the `sequence` variable with a feedback message to store the sequence. After every update of the feedback message in the for-loop, we publish the feedback message:

```python
import time


import rclpy
from rclpy.action import ActionServer
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionServer(Node):

    def __init__(self):
        super().__init__('fibonacci_action_server')
        self._action_server = ActionServer(
            self,
            Fibonacci,
            'fibonacci',
            self.execute_callback)

    def execute_callback(self, goal_handle):
        self.get_logger().info('Executing goal...')


        feedback_msg = Fibonacci.Feedback()

        feedback_msg.partial_sequence = [0, 1]


        for i in range(1, goal_handle.request.order):

            feedback_msg.partial_sequence.append(

                feedback_msg.partial_sequence[i] + feedback_msg.partial_sequence[i-1])

            self.get_logger().info('Feedback: {0}'.format(feedback_msg.partial_sequence))

            goal_handle.publish_feedback(feedback_msg)

            time.sleep(1)


        goal_handle.succeed()

        result = Fibonacci.Result()

        result.sequence = feedback_msg.partial_sequence

        return result


def main(args=None):
    rclpy.init(args=args)

    fibonacci_action_server = FibonacciActionServer()

    rclpy.spin(fibonacci_action_server)


if __name__ == '__main__':
    main()
```


After restarting the action server, it is confirmed that feedback is now published by using the command line tool with the `--feedback` option:

```
ros2 action send_goal --feedback fibonacci action_tutorials_interfaces/action/Fibonacci "{order: 5}"
```

**3.2. Writing an action client**

Similarly, we also scope the action client to a new file named `fibonacci_action_client.py` and the following codes are added to the file:

```python

import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        return self._action_client.send_goal_async(goal_msg)


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    future = action_client.send_goal(10)

    rclpy.spin_until_future_complete(action_client, future)


if __name__ == '__main__':
    main()
    
```

After this step, we can run the action server built earlier using following code:

```
python3 fibonacci_action_server.py
```

And in another terminal, we run the action client:

```
python3 fibonacci_action_client.py
```

The action server executes the goal and we are able to see the messages successfully. 

The action client start up and quickly finish but we don't get any feedback. 


**3.2.1.Getting a result**

We need to set a goal handle for the goal we sent and hence here is the complete code for this:

```python
import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        self._send_goal_future = self._action_client.send_goal_async(goal_msg)

        self._send_goal_future.add_done_callback(self.goal_response_callback)

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def get_result_callback(self, future):
        result = future.result().result
        self.get_logger().info('Result: {0}'.format(result.sequence))
        rclpy.shutdown()


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    action_client.send_goal(10)

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()
    
```

With the action server running in a separate terminal, if we run Fibonacci action client, we will be able to see logged messages for the goal being accepted and the final result.

```
python3 fibonacci_action_client.py
``` 

**3.2.2.Getting feedback**

Once, action client is able to send the goals, here is the complete code for getting some feedbacks about the goals we send from the action server:

```
import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        self._send_goal_future = self._action_client.send_goal_async(goal_msg, feedback_callback=self.feedback_callback)

        self._send_goal_future.add_done_callback(self.goal_response_callback)

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def get_result_callback(self, future):
        result = future.result().result
        self.get_logger().info('Result: {0}'.format(result.sequence))
        rclpy.shutdown()

    def feedback_callback(self, feedback_msg):
        feedback = feedback_msg.feedback
        self.get_logger().info('Received feedback: {0}'.format(feedback.partial_sequence))


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    action_client.send_goal(10)

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()
    
```

### 4.Composing multiple nodes in a single process

**4.1. To discover avilable components**

_In order to check the available components in the workspace, we run the following commands._

```
ros2 component types
```

The terminal returns all the available components:

![image](https://user-images.githubusercontent.com/113494159/196020894-c021cc1d-42ba-49bc-8841-a2d11a100985.png)

**4.2. Run-time composition using ROS services with a publisher and subscriber**

Firstly, we start the component container in one terminal :

```
ros2 run rclcpp_components component_container
```

In order to verify that the container is running via `ros2` command line tools, we run following command in the second terminal which will show a name of the component as an output.

```
ros2 component list
```

After this step, in the second terminal, we load the talker component:

```
ros2 component load /ComponentManager composition composition::Talker
```

This command will return the unique ID of the loaded component as well as the name of the node:

![image](https://user-images.githubusercontent.com/113494159/196021077-03a72c40-9ed6-421a-ab57-db6edeb20712.png)

![image](https://user-images.githubusercontent.com/113494159/196021068-fa4ffe58-7d70-42e3-9d06-d3ecff8eddfd.png)

After this, we run following code in the second terminal in order to load the listener component:

```
ros2 component load /ComponentManager composition composition::Listener
```

The output is shown in the images above.


Finally we can run the `ros2` command line utility to inspect the state of the container:

```
ros2 component list
```

We can see the result as follows:

```
/ComponentManager
   1  /talker
   2  /listener
```


**4.3. Run-time composition using ROS services with a server and client**

It is very similar steps to what we did using talker and listener. 

In the first terminal, we run:

```
ros2 run rclcpp_components component_container
```

and after that, in the second terminal, we run following commands to see **server** and **client** source code:

```
ros2 component load /ComponentManager composition composition::Server
ros2 component load /ComponentManager composition composition::Client
```

We can see the output of the above commands as in the following images:

![image](https://user-images.githubusercontent.com/113494159/196021291-7cb081bf-ab97-4ebb-ac7d-1d02c01846bf.png)

![image](https://user-images.githubusercontent.com/113494159/196021325-1b981551-06f5-444e-a93e-9d5944c0a569.png)

**4.4. Compile-time composition using ROS services**

By using this demonstration, it shows that the same shared libraries can be reused to compile a single executable running multiple components. 

The executable contains all four components from above : `talker`, `listener`, `server`, and `client`.

In one terminal, 

```
ros2 run composition manual_composition
```

![image](https://user-images.githubusercontent.com/113494159/196021396-73d71513-9154-481f-a9a2-5fe903ea492b.png)


**4.5. Run-time composition using dlopen**

This demonstration shows an alternative to run-time composition by creating a generic container process an explicity passing the libraries to load without using ROS interfaces. The process will open each library and create one instance of each "rclcpp::Node" class in the library source code.


```
ros2 run composition dlopen_composition `ros2 pkg prefix composition`/lib/libtalker_component.so `ros2 pkg prefix composition`/lib/liblistener_component.so
```

![image](https://user-images.githubusercontent.com/113494159/196021502-a99852ad-36b2-47ea-904d-137d69055275.png)


**4.6. Composition using launch actions**

While the command line tools are helpful for troubleshooting and diagnosing component setups, starting a group of components at once is frequently more practical. We can make use of `ros2` launch's functionality to automate this process.

```
ros2 launch composition composition_demo.launch.py
```

![image](https://user-images.githubusercontent.com/113494159/196021525-b673e259-283a-407f-9cdf-ebf00c3796a3.png)


### 5.Creating a launch file

In order to create a launch file, we use the `rqt_graph` and `turtlesim` packages which we have already installed previously.

**5.1. Setup**

We need to create a new directory to store the launch files:

```
mkdir launch
```

**5.2. Writing the launch file**

In the newly created directory, we created a new file named `turtlesim_mimic_launch.py` and paste the following codes into the file:

```python
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='turtlesim',
            namespace='turtlesim1',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='turtlesim',
            namespace='turtlesim2',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='turtlesim',
            executable='mimic',
            name='mimic',
            remappings=[
                ('/input/pose', '/turtlesim1/turtle1/pose'),
                ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
            ]
        )
    ])
```

**5.3. ros2 launch**

In order to run the launch file created, we enter into the earlier created directory and run the following commands:

```
cd launch
ros2 launch turtlesim_mimic_launch.py
```

The output is shown in the image below:

![image](https://user-images.githubusercontent.com/113494159/196021738-0643f343-1071-4658-921c-95768bf41bd9.png)

Two turtlesim windows are opened with the above messages:

![image](https://user-images.githubusercontent.com/113494159/196021763-2c35af4d-817b-48fc-81fc-c39d2e618ec1.png)

_In order to see the sytem in action, we open a new terminal and run the `ros2 topic pub` command on `/turtlesim1/turtle1/cmd_vel` topic to get the first turtle moving._

![image](https://user-images.githubusercontent.com/113494159/196021849-9b6d5512-284c-4d28-a696-afa934e750f8.png)

**Both the turtle move in the same path.**


**5.4. Introspect the system with rqt_graph**

Open the new terminal without closing the system and we run `rqt_graph`.

```
rqt_graph
```

![image](https://user-images.githubusercontent.com/113494159/196022052-e8d67387-577a-41e9-916b-c4ac211548a6.png)


### 6.Integrating launch files into ROS2 packages

**6.1. Creating a package**

Firstly, we create a workspace for the package:

```
mkdir -p launch_ws/src
cd launch_ws/src
```

and create a python package:

```
ros2 pkg create py_launch_example --build-type ament_python
```


**6.2. Creating the structure to hold launch files **

After creating the packages, it should be looking as follows for python package:

![image](https://user-images.githubusercontent.com/113494159/196022501-78722f24-c268-4341-a589-706e7336f8eb.png)

And in order to colcon to launch files, we need to inform Python's setup tools of our launch files using the `data_files` parameter of `setup`.

Inside, `setup.py` file, we input the following codes:

```python
import os
from glob import glob
from setuptools import setup

package_name = 'py_launch_example'

setup(
    # Other parameters ...
    data_files=[
        # ... Other data files
        # Include all launch files.
        (os.path.join('share', package_name), glob('launch/*launch.[pxy][yma]*'))
    ]
)
```

**6.3. Writing the launch file**

Inside the `launch` directory, we create a new launch file named `my_script_launch.py`.
Here, the launch file should define the `generate_launch_description()` function which returns a `launch.LaunchDescription() to be used by the `ros2 launch` verb.

```python
import launch
import launch_ros.actions

def generate_launch_description():
    return launch.LaunchDescription([
        launch_ros.actions.Node(
            package='demo_nodes_cpp',
            executable='talker',
            name='talker'),
  ])
```

**6.4. Building and running the launch file**

We go to top-level of the workspace and build the file using:

```
colcon build
```

Once the build is successful, we should be able to run the launch file as follows:

```
ros2 launch py_launch_example my_script_launch.py
```

### 7.Using Substitutions

**7.1. Creating and Setting up the package**

We create a new package of build_type `ament_python` named `launch_tutorial` :

```
ros2 pkg create launch_tutorial --build-type ament_python
```

and inside of that package, we create a directory called `launch`.

```
mkdir launch_tutorial/launch
```

After that, we edit the `setup.py` file and add in changes so that launch file will be installed successfully. 

```python
import os
from glob import glob
from setuptools import setup

package_name = 'launch_tutorial'

setup(
    # Other parameters ...
    data_files=[
        # ... Other data files
        # Include all launch files.
        (os.path.join('share', package_name), glob('launch/*launch.[pxy][yma]*'))
    ]
)
```

**7.2. Parent Launch File**

After the above steps, we created a launch file named : `example_main.launch.py` in the launch folder of the `launch_tutorial` directory with the following codes in it:

```python
from launch_ros.substitutions import FindPackageShare

from launch import LaunchDescription
from launch.actions import IncludeLaunchDescription
from launch.launch_description_sources import PythonLaunchDescriptionSource
from launch.substitutions import PathJoinSubstitution, TextSubstitution


def generate_launch_description():
    colors = {
        'background_r': '200'
    }

    return LaunchDescription([
        IncludeLaunchDescription(
            PythonLaunchDescriptionSource([
                PathJoinSubstitution([
                    FindPackageShare('launch_tutorial'),
                    'example_substitutions.launch.py'
                ])
            ]),
            launch_arguments={
                'turtlesim_ns': 'turtlesim2',
                'use_provided_red': 'True',
                'new_background_r': TextSubstitution(text=str(colors['background_r']))
            }.items()
        )
    ])
```

**7.3. Substitutions example launch file**

A new file is created in the same folder: `example_substitutions.launch.py`

```python
from launch_ros.actions import Node

from launch import LaunchDescription
from launch.actions import DeclareLaunchArgument, ExecuteProcess, TimerAction
from launch.conditions import IfCondition
from launch.substitutions import LaunchConfiguration, PythonExpression


def generate_launch_description():
    turtlesim_ns = LaunchConfiguration('turtlesim_ns')
    use_provided_red = LaunchConfiguration('use_provided_red')
    new_background_r = LaunchConfiguration('new_background_r')

    turtlesim_ns_launch_arg = DeclareLaunchArgument(
        'turtlesim_ns',
        default_value='turtlesim1'
    )
    use_provided_red_launch_arg = DeclareLaunchArgument(
        'use_provided_red',
        default_value='False'
    )
    new_background_r_launch_arg = DeclareLaunchArgument(
        'new_background_r',
        default_value='200'
    )

    turtlesim_node = Node(
        package='turtlesim',
        namespace=turtlesim_ns,
        executable='turtlesim_node',
        name='sim'
    )
    spawn_turtle = ExecuteProcess(
        cmd=[[
            'ros2 service call ',
            turtlesim_ns,
            '/spawn ',
            'turtlesim/srv/Spawn ',
            '"{x: 2, y: 2, theta: 0.2}"'
        ]],
        shell=True
    )
    change_background_r = ExecuteProcess(
        cmd=[[
            'ros2 param set ',
            turtlesim_ns,
            '/sim background_r ',
            '120'
        ]],
        shell=True
    )
    change_background_r_conditioned = ExecuteProcess(
        condition=IfCondition(
            PythonExpression([
                new_background_r,
                ' == 200',
                ' and ',
                use_provided_red
            ])
        ),
        cmd=[[
            'ros2 param set ',
            turtlesim_ns,
            '/sim background_r ',
            new_background_r
        ]],
        shell=True
    )

    return LaunchDescription([
        turtlesim_ns_launch_arg,
        use_provided_red_launch_arg,
        new_background_r_launch_arg,
        turtlesim_node,
        spawn_turtle,
        change_background_r,
        TimerAction(
            period=2.0,
            actions=[change_background_r_conditioned],
        )
    ])
```

**7.4. Building the package**

We run the build command in the root of the workspace. 

```
colcon build
```

**7.5. Launching Example**

Now we are able to run the `example_main.launch.py` file using the `ros2 launch` command. 

```
ros2 launch launch_tutorial example_main.launch.py
```

![image](https://user-images.githubusercontent.com/113494159/196023691-55605922-f633-4f1a-b057-47543e52db44.png)

A turtlesim node is started with a blue background. After that second turtle is spawned and the background color is changed to purple and pink respectively.

### 8.Using Event Handlers

**8.1. Event handler example launch file**

We created a new file named: `example_event_handlers.launch.py` in the same directory.. i.e. inside `launch` folder of `launch_tutorial` package.

```python
from launch_ros.actions import Node

from launch import LaunchDescription
from launch.actions import (DeclareLaunchArgument, EmitEvent, ExecuteProcess,
                            LogInfo, RegisterEventHandler, TimerAction)
from launch.conditions import IfCondition
from launch.event_handlers import (OnExecutionComplete, OnProcessExit,
                                OnProcessIO, OnProcessStart, OnShutdown)
from launch.events import Shutdown
from launch.substitutions import (EnvironmentVariable, FindExecutable,
                                LaunchConfiguration, LocalSubstitution,
                                PythonExpression)


def generate_launch_description():
    turtlesim_ns = LaunchConfiguration('turtlesim_ns')
    use_provided_red = LaunchConfiguration('use_provided_red')
    new_background_r = LaunchConfiguration('new_background_r')

    turtlesim_ns_launch_arg = DeclareLaunchArgument(
        'turtlesim_ns',
        default_value='turtlesim1'
    )
    use_provided_red_launch_arg = DeclareLaunchArgument(
        'use_provided_red',
        default_value='False'
    )
    new_background_r_launch_arg = DeclareLaunchArgument(
        'new_background_r',
        default_value='200'
    )

    turtlesim_node = Node(
        package='turtlesim',
        namespace=turtlesim_ns,
        executable='turtlesim_node',
        name='sim'
    )
    spawn_turtle = ExecuteProcess(
        cmd=[[
            FindExecutable(name='ros2'),
            ' service call ',
            turtlesim_ns,
            '/spawn ',
            'turtlesim/srv/Spawn ',
            '"{x: 2, y: 2, theta: 0.2}"'
        ]],
        shell=True
    )
    change_background_r = ExecuteProcess(
        cmd=[[
            FindExecutable(name='ros2'),
            ' param set ',
            turtlesim_ns,
            '/sim background_r ',
            '120'
        ]],
        shell=True
    )
    change_background_r_conditioned = ExecuteProcess(
        condition=IfCondition(
            PythonExpression([
                new_background_r,
                ' == 200',
                ' and ',
                use_provided_red
            ])
        ),
        cmd=[[
            FindExecutable(name='ros2'),
            ' param set ',
            turtlesim_ns,
            '/sim background_r ',
            new_background_r
        ]],
        shell=True
    )

    return LaunchDescription([
        turtlesim_ns_launch_arg,
        use_provided_red_launch_arg,
        new_background_r_launch_arg,
        turtlesim_node,
        RegisterEventHandler(
            OnProcessStart(
                target_action=turtlesim_node,
                on_start=[
                    LogInfo(msg='Turtlesim started, spawning turtle'),
                    spawn_turtle
                ]
            )
        ),
        RegisterEventHandler(
            OnProcessIO(
                target_action=spawn_turtle,
                on_stdout=lambda event: LogInfo(
                    msg='Spawn request says "{}"'.format(
                        event.text.decode().strip())
                )
            )
        ),
        RegisterEventHandler(
            OnExecutionComplete(
                target_action=spawn_turtle,
                on_completion=[
                    LogInfo(msg='Spawn finished'),
                    change_background_r,
                    TimerAction(
                        period=2.0,
                        actions=[change_background_r_conditioned],
                    )
                ]
            )
        ),
        RegisterEventHandler(
            OnProcessExit(
                target_action=turtlesim_node,
                on_exit=[
                    LogInfo(msg=(EnvironmentVariable(name='USER'),
                            ' closed the turtlesim window')),
                    EmitEvent(event=Shutdown(
                        reason='Window closed'))
                ]
            )
        ),
        RegisterEventHandler(
            OnShutdown(
                on_shutdown=[LogInfo(
                    msg=['Launch was asked to shutdown: ',
                        LocalSubstitution('event.reason')]
                )]
            )
        ),
    ])
```

**8.2. Building and Running the Command**

After adding the file, we go back to the root of the workspace and run the build command there.
```
colcon build
```

After building, it is important to source the package and run the following codes for the output:

ros2 launch launch_tutorial example_event_handlers.launch.py turtlesim_ns:='turtlesim3' use_provided_red:='True' new_background_r:=200


![image](https://user-images.githubusercontent.com/113494159/196024114-0e8025ee-186e-4b6c-bc8a-5f518d23b78d.png)

It start a turtlesim node with a blue background and spawn the second turtle. After that, it change the background color to purple and then to pink.
If the turtlesim window is closed, it shutdown the launch file. 
