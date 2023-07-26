# Задание на работу №2
## Построение карт с использованием SLAM

### Задание

1. В среде Gazebo необходимо построить карту окружающего робота пространства с использованием любой библиотеки SLAM (например, gmapping, google catrtographer или др.).

2. Необходимо написать программу, которая позволит роботу перемещаться из одной точки в другую по заданным координатам (x, y). На пути следования робота должны встретиться препятствия. Робот должен объехать их и вернуться на траекторию  следования. В качестве возможного способа реализации поставленной задачи можно рассмотреть вариант просчета точек пути следования робота. Можно использоавать библиотеку AMCL.

# Выполнение
## Установка пакетов gazebo

```
sudo apt-get install ros-noetic-gazebo-ros-pkgs
```

Если по какой-то причине у вас не установлено gazebo, то установить его можно комадной:

```
curl -sSL http://get.gazebosim.org | sh
```

## Установка Gmapping

```
sudo apt install ros-noetic-slam-gmapping
```

## Установка DVA local planner

```
sudo apt-get install ros-noetic-dwa-local-planner
```

## Установка Map Saver

```
sudo apt-get install ros-noetic-map-server
```

## Установка turtlebot3
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src/
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ~/catkin_ws && catkin_make
```

## Построение карты

Как обычно, приложения можно запускать двумя способами: просто через консоль командой roscore и rosrun, либо с использованием roslaunch.

### С использованием roscore и rosrun

Все команды прописываются в <b>отдельных</b> терминалах, в каждом нужно <b>обязательно прописать</b> <code>source devel/setup.bash</code>

Сначала запустить ядро ros:
```
roscore
```

Затем указать модель робота и запустить симуляцию мира с роботом (в данном случае запустится дом из стандартного примера):
```
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_house.launch
```

Запустить SLAM-ноду:
```
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
<b>SLAM</b> - это одновременная локализация и построение карты.

Запустить ноду для телеуправления:
```
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

### С использованием launch файла

[Примеры launch файлов](https://github.com/Vladosok96/RAII_robotics/Samples/02navigation/launch)

Необходимо написать launch файл, который будет запускать ваш мир, робота нужной модели, ноду управления роботом с клавиш и slam алгоритм.

### Сохранение карты

Далее необходимо с помощью клавиш пройти роботом всю карту. 

Карта сохраняется командой:

```
rosrun map_server map_saver -f ~/map
```

## Планирование и следование маршрута

Если вы уже создали файл карты, то можете запустить стандартный пример с навигацией:
```
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```

## Полезные ссылки

Документация turtlebot3 -  http://emanual.robotis.com/docs/en/platform/turtlebot3/overview/

Документация gazebo - http://gazebosim.org/


### Библиографический список
1.	М.Шахинпур. Курс робототехники.
2.	Юревич Е.И. Основы робототехники.
3.	http://ros.org
4.	http://gazebosim.org/
5.	https://geektimes.ru/post/281760/ - описание установки ROS в среде Ubuntu на русском языке
6. Morgan Quigley, Brian Gerkey & William D. Smart. Programming robots with ROS. Автоматные модели: глава 13, State machines
7. Использование текстур в мире Gazebo: [1](http://answers.gazebosim.org/question/4761/how-to-build-a-world-with-real-image-as-ground-plane/) [2](http://answers.gazebosim.org/question/7922/ground-plane-texture-image/)
