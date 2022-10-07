# Megoldás
🤖 Autonóm robot verseny megoldás template

# Telepítés

A minél szélesebb használhatóság érdeklében leírjuk a Windows alapú (WSL) és natív Ubuntu telepítés lépéseit is. A használt szoftververziók:
- Ubuntu 18.04
- ROS Melodic

Az első lépés során tehát vagy az `1/A.` vagy az `1/B.` opciót javasoljuk 

## `1/A.` WSL alapú telepítés
Windows Subsystem for Linux
- VS code szerkesztő: https://code.visualstudio.com/download

## `1/B.` Natív Ubuntu alapú telepítés
Ubuntu 18.04
- VS code szerkesztő: https://code.visualstudio.com/download

## `2.` ROS telepítése

A teljes telepítési leírás megtalálható itt: http://wiki.ros.org/melodic/Installation/Ubuntu

## `3.` szimulátor és a példamegoldás telepítése

A szükésges csomagok így telepíthetőek:

```
sudo apt-get -y install ros-melodic-ros-control ros-melodic-gazebo-ros-control ros-melodic-ros-controllers ros-melodic-navigation qt4-default ros-melodic-ackermann-msgs ros-melodic-serial ros-melodic-teb-local-planner* ros-melodic-tf-conversions zip unzip ros-melodic-jsk-rviz-plugins python-catkin-tools
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

**Fontos**, hogy a középiskola neve és azonosítója ki legyen töltve, így a `/kozepiskola` topic-ban a tényleges középisola név és azonosító szerepeljen. Ezt a legkönnyebben a `pid_error.py` fájl elején lévő változók átírásával lehet elérni (ékezetek nélkül).

Tehát a következő állapot alaphelyzet, hibás beküldést jelent:

``` bash
$ rostopic echo -n1 /kozepiskola
data: "Ismeretlen kozepiskola(A00)"
```

Link: https://github.com/robotverseny/megoldas/blob/main/src/pid_error.py#L15-L16

Terminal1:
```
roscore
```
Terminal2:
```
roslaunch racecar_gazebo racecar.launch
```
*Tipp:* `rosservice call /gazebo/reset_simulation "{}"` paranccsal alaphelyzetbe állítható a szimulátor, de a `megoldas1.launch`-ban lévő:
``` xml
<node pkg="rosservice" type="rosservice" name="rosservice" args="call /gazebo/reset_simulation"/>
```
ugyanezt teszi.

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
