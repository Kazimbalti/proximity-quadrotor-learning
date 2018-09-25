# Vision-based Control of a Quadrotor in User Proximity: Mediated vs End-to-End Learning Approaches
*Dario Mantegazza, Jérôme Guzzi, Luca M. Gambardella and Alessandro Giusti*
## *Abstract*
We consider the task of controlling a quadrotor
to hover in front of a freely moving user, using input data
from an onboard camera. On this specific task we compare two
widespread learning paradigms: a mediated approach, which
learns an high-level state from the input and then uses it for de-
riving control signals; and an end-to-end approach, which skips
high-level state estimation altogether. We show that despite
their fundamental difference, both approaches yield equivalent
performance on this task. We finally qualitatively analyze the
behavior of a quadrotor implementing such approaches.

The paper can be seen [here](https://arxiv.org/abs/1809.08881)
## Dataset
The Dataset used is composed of 21 different [rosbag](http://wiki.ros.org/rosbag) files. 

Each rosbag correspond to a single recording session. For the recording sessions we used the [Drone Arena](https://github.com/jeguzzi/drone_arena) software. Each recording session as been manually analyzed to select the appropriate start and ending in order to avoid start-up or 'wind down' situations; this information is available in the `gloabl_parameters.py` script as `bag_start_cut` and `bag_end_cut` dictionaries with the bag name as key.


In each file we recorded multiple [topics](http://wiki.ros.org/Topics); for this paper we use the following topics:

| Topic | data contained |
| - | - |
| `/bebop/image_raw/compressed` | Drone's front facing camera feed |
| `/optitrack/head` | Motion Capture information about the 6DOF user's head's [pose](http://docs.ros.org/lunar/api/geometry_msgs/html/msg/Pose.html). In sync with OptiTrack system timestamp |
| `/optitrack/bebop` | Motion Capture information about the 6DOF drone's [pose](http://docs.ros.org/lunar/api/geometry_msgs/html/msg/Pose.html). In sync with OptiTrack system timestamp |
| `/bebop/mocap_odom` | Motion Capture information about the 6DOF drone's [pose](http://docs.ros.org/lunar/api/geometry_msgs/html/msg/Pose.html) + [twist](http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html). In sync with Drone Arena timestamp |
| `/bebop/odom` | Drone's Optical Flow odometry |

In our test we randomly divided the whole dataset in train and test set as follows

| Train set bagfiles | Test set bagfiles |
| - | - |
| 1, 2, 5, 7, 8, 9, 10, 11, 12, 13, 14, 16, 17, 18, 19, 20, 21 | 3, 4, 6, 15 |

The whole dataset can be downloaded (6.6 GB) [here](https://drive.switch.ch/index.php/s/1Q0zN0XDzyRxug4).

A Jupyter notebook on how we extract the data can be found [here](https://github.com/idsia-robotics/proximity-quadrotor-learning/tree/master/dataset).

## Code
The code present in this repository is thought to be used in a directory structured like the one that follows.

    .
    ├── script                  # Script directory
    ├── bagfiles                # Bagfiles main directory
    │   ├── train               # Directory for the bagfiles selected for the train set
    │   └── test                # Directory for the bagfiles selected for the test set
    └── dataset
        ├── version1            # Model 1 dataset .pickle files
        ├── version2            # Model 2 dataset .pickle files
        └── version3            # Model 3 dataset .pickle files

The script that are executable are two:
* `dataset_generator.py`
* `keras_train.py`
### `dataset_generator.py`
It is used to create the dataset files used by the models. After launchin the script you will be prompted with a menu in order to select the type of dataset to create.
Each model has it's own dataset.

### `keras_train.py`
Allows you to run each model by it self or all three with the same data.

All scripts are available [here](https://github.com/idsia-robotics/proximity-quadrotor-learning/tree/master/script)

## Video
Some videos related to our work can be found [here](https://github.com/idsia-robotics/proximity-quadrotor-learning/tree/master/video)

## Errata
In the linked paper each image in Fig.2 have the left and bottom plot with inverted direction. Also in the same figures the smaller plot is rotated by 90° to the right
