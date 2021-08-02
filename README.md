# imu2pose

## Introduction

This dataset aims to caculate relative pose changes of robot based on imu(Inertial Measurement Unit) data from sensor on board.

## Environment
The simulated environment shape in Gazebo is 20x20x10 meters (Length x Width x Height).
When you view the environment from above, the origin of the coordinate system is located in the bottom left of the environment. The unit of the coordinate system is 1 meter.

The ground robot moves in the middle 10x10 grids.

## Requirements
- Python3
- numpy

## Files
- Gazebo_data10_len120_conti_rndclr_Jun1th_train.npz
- Gazebo_data10_len120_conti_rndclr_Jun1th_test.npz
- Link to download files: https://drive.google.com/drive/folders/1fhf6fuxxHMewJtosEaryexNFbpogvr8q?usp=sharing

## Data
L is the number of waypoints of one trajectory<br />
B is batchsize

- image: LxBx3x64x64 rgb image
- depth: LxBx3x64x64 depth image
- delta: LxBx3 (x, y, yaw) pose in Gazebo(global) coordinate system
- imu:   LxBx20x3 (a_x, a_y, w_yaw) in egocentric system
  
## About imu
  The imu data is generated from the imu sensor boarding on the robot, which is egocentric. When robot moves betwwen two consecutive waypoints, the sensor record the linear accelaration(a_x and a_y) and angular velocity(w_yaw) 20 times, generating the imu data of size 20x3.
  
## Reading the data and an example of how to use data
```
file = np.load(data_path)
imu_data = file['imu'] # size: LxBx20x3
pose = file['delta']   # size: LxBx3

batch_index  = bi = 0
length_index = li = 0
input = imu_data[li+1,bi]           # imu data between two waypoints
label = pose[li+1,bi] - pose[li,bi] # pose changes of two waypoints
```

## Contact
Mingyang: mli170@syr.edu
