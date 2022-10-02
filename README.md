# Megoldás
🤖 Autonóm robot verseny megoldás template

# Telepítés

A minél szélesebb használhatóság érdeklében leírjuk a Windows alapú (WSL) és natív Ubuntu telepítés lépéseit is. A használt szoftververziók:
- Ubuntu 18.04
- ROS Melodic

## `1/A.` WSL alapú telepítés
Windows Subsystem for Linux

## `1/B.` Natív Ubuntu alapú telepítés
Ubuntu 18.04

## `2.` ROS telepítése

A teljes telepítési leírás megtalálható itt: http://wiki.ros.org/melodic/Installation/Ubuntu

## `3.` szimulátor és a példamegoldás telepítése

A szükésges csomagok így telepíthetőek:

```
sudo apt-get -y install ros-melodic-ros-control ros-melodic-gazebo-ros-control ros-melodic-ros-controllers ros-melodic-navigation qt4-default ros-melodic-ackermann-msgs ros-melodic-serial ros-melodic-teb-local-planner* ros-melodic-tf-conversions zip unzip python-catkin-tools
```

Készítsünk egy külön workspace-t ('sim_ws'), hogy később könnyen törölhessük, ha már nem kell.

```
cd ~
mkdir -p sim_ws/src
cd ~/sim_ws/src
git clone https://github.com/robotverseny/racecar_gazebo
git clone https://github.com/robotverseny/megoldas
catkin init
cd ~/sim_ws
catkin build
```

Hogy ne kelljen minden terminalban megadnunk a workspace-t, tegyük a bashrc-be. Ha ezt nem szerenénk, elég mindig kiadni a `source ~/sim_ws/devel/setup.bash` parancsot.

```
echo "source ~/sim_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
Később a `bashrc`-ből törölhető ez a sor, nyissuk meg vs code-ból: `code ~/.bashrc`.

### TODO

# Fejlesztés

Terminal1:
```
roscore
```
Terminal2:
```
roslaunch racecar_gazebo racecar.launch
```
Terminal3:
```
roslaunch megoldas megoldas1.launch
```

# Beküldés

```
cd sim_ws/src
zip -r megoldas.zip megoldas
```
### TODO