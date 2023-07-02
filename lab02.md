# Задание на работу №2
## Построение карт с использованием SLAM

### Задание

1. В среде Gazebo необходимо построить карту окружающего робота пространства с использованием любой библиотеки SLAM (например, gmapping, google catrtographer или др.).

2. Необходимо написать программу, которая позволит роботу перемещаться из одной точки в другую по заданным координатам (x, y). На пути следования робота должны встретиться препятствия. Робот должен объехать их и вернуться на траекторию  следования. В качестве возможного способа реализации поставленной задачи можно рассмотреть вариант просчета точек пути следования робота. Можно использоавать библиотеку AMCL.

# Выполнение
## Установка пакетов gazebo

```
sudo apt-get install ros-noetic-gazebo-pkgs
```

Если по какой-то причине у вас не установлено gazebo, то установить его можно комадной:

```
curl -sSL http://get.gazebosim.org | sh
```

## Решение часто возникаевых ошибок

### rosdep: command not found

Решение:

```
sudo apt-get install python-pip
sudo pip install -U rosdep
sudo rosdep init
rosdep update
```

### Failed to create the dwa_local_planner/DWAPlannerROS planner

Решение:

```
sudo apt-get install ros-melodic-dwa-local-planner
```

## Создание своего мира в gazebo

Запуск gazebo:

```
gazebo
```

После запуска у вас откроется пустой мир. Стены и прочие элементы можно создавать с помощью вкладки insert.

Если у вас не отображаются стандартные модели, то необходимо добавить путь до них "/home/ИМЯ/.gazebo/models". 

Далее необходимо просто выбирать объект из стандартных моделей и устанавливать его. В меню инструментов на верхней панели можно найти инструменты для перемещения, вращения и изменения размеров.

После создания мира его необходимо сохранить.

File -> Save World As.

## Установка turtlebot3

```
cd ~/catkin_ws/src/
git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b kinetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
cd ~/catkin_ws && catkin_make
```

## Построение карты

[Примеры launch файлов]: https://github.com/ulstu/robotics_cad/tree/master/practice/2020/samples/02navigation/launch

На этом этапе необходимо написать launch файл, который будет запускать ваш мир, робота нужной модели, ноду управления роботом с клавиш и slam алгоритм.

Далее необходимо с помощью клавиш пройти роботом всю карту. 

Карта сохраняется командой:

```
rosrun map_server map_saver -f ~/map
```

## Перемещение с помощью карты

[Примеры ко 2 лабораторной работе]: https://github.com/ulstu/robotics_cad/tree/master/practice/2020/samples/02navigation

В примерах находятся наброски скрипта, позволяющего роботу перемещаться к указанным координатам.

Его необходимо доработать.

Далее необоходимо написать launch файл, который запускает симуляцию мира и робота, ваш скрипт и навигацию робота.

Запуск launch-файла описан в методических указаниях к лабораторной работе №1/ 

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
