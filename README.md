![alt text](https://github.com/TRA370-Project-5/ROS-px4-master/blob/master/docs/architecture_xrce-dds_ros2.fed61809.svg)
![alt text](https://github.com/TRA370-Project-5/ROS-px4-master/blob/master/docs/px4_companion_computer_simple.f0c69339.svg)
![alt text](https://github.com/TRA370-Project-5/ROS-px4-master/blob/master/docs/eyJjb2RlIjoiZ3JhcGggVERcbiAgc3ViZ3JhcGggR3JvdW5kICBTdGF0aW9uXG4gIGduZFtST1MgRW5hYmxlZCBDb21wdXRlcl0gLS0tIHFnY1txR3JvdW5kQ29udHJvbF1cbiAgZW5kXG4gIGduZCAtLU1BVkxpbmsvVURQLS0-IHdbV2lGaV07XG4gIHFnYyAtLU1BVkxpbmstLT4gdztc.jpg?raw=true)

## Installation

Clone the repository

    git clone https://github.com/TRA370-Project-5/ROS-px4-master
    git submodule update --init --recursive --progress
    git submodule sync

Build the docker images

    docker compose build
    
or each seperately 

    docker compose build <name>

To launch a container use

    docker compose up <name>

The PX4 container launches the SITL px4 simulation and waits to connect to a simulator such as Gazebo. Edit the CMD command to change the simulator according to the documentation on PX4 website 
https://docs.px4.io/main/en/simulation/

The ROS container launches the ROS enviroment

The XRCE agent launches the XRCE agent node and tries to connect to any PX4 instance SITL or real hardware and broadcast ROS2 data to the DDS network.


#### Simulation

QGroundcontrol

UDP Server
For WSL:
Connect to WSL IP

#### Gazebo
TODO

#### AirSim/Unreal engine
Run latest 4.x version, dont run Unreal >=5.0

Open incoming/outgoing TCP port 4560 and incoming/outgoing UDP port 14540, 14580. I am not sure if 145480 is needed and if outgoing is needed. Probably not...

Airsim
In your settings.json which is generated in %USER%/Documents/Airsim/

change the file to:

```
{
  "SettingsVersion": 1.2,
  "SimMode": "Multirotor",
  "ClockType": "SteppableClock",
  "Vehicles": {
      "PX4": {
          "VehicleType": "PX4Multirotor",
          "UseSerial": false,
          "LockStep": true,
          "UseTcp": true,
          "TcpPort": 4560,
          "ControlIp": "remote",
          "ControlPortLocal": 14540,
          "ControlPortRemote": 14580,
          "LocalHostIp": "172.17.128.1",
          "Sensors":{
              "Barometer":{
                  "SensorType": 1,
                  "Enabled": true,
                  "PressureFactorSigma": 0.0001825
              }
          },
          "Parameters": {
              "NAV_RCL_ACT": 0,
              "NAV_DLL_ACT": 0,
              "COM_OBL_ACT": 1,
              "LPE_LAT": 47.641468,
              "LPE_LON": -122.140165
          }
      }
  }
}
```
