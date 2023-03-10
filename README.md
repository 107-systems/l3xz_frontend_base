<a href="https://107-systems.org/"><img align="right" src="https://raw.githubusercontent.com/107-systems/.github/main/logo/107-systems.png" width="15%"></a>
:floppy_disk: `l3xz_frontend_base`
=============================
[![Spell Check status](https://github.com/107-systems/l3xz_frontend_base/actions/workflows/spell-check.yml/badge.svg)](https://github.com/107-systems/l3xz_frontend_base/actions/workflows/spell-check.yml)


<p align="center">
  <a href="https://github.com/107-systems/l3xz"><img src="https://raw.githubusercontent.com/107-systems/.github/main/logo/l3xz-logo-memento-mori-github.png" width="40%"></a>
</p>

Fundamental functionalities for frontends using roslibjs.

# Implementation overview

~~~bash
── base_js                      Javascript root
   ├── 3rdparty                    Third party libraries
   ├── frontend                    Callbacks for frontend elements
   ├── rosinterface                Rosbridge socket interaction 
   ├── setup                       Setup routines for pages
   ├── util                        Helpers like geocalculation or logging
   └── visualizer                  Topic visualization
       ├── base                    Rendering cores that can be attached via DOM
       └── renderers               Rendering functions sorted by ROS topics
           ├── diagnostic-msgs
           ├── geometry-msgs
           ├── nav-msgs
           ├── sensor-msgs
           └── std-msgs
~~~

## Adding visualization for a topic

A rendering function for a new topic should be created in a new file according to the hierarchy in ```javascript/visualizer/renderers```. It is important to extend the entries in the ```map.js``` files to make the new function available for the visualizer base. Then, if a topic of the right type is found, the rendering function will be called automatically. A rendering function must have the following signature:

~~~js
/**
 * @param name          Name of the topic
 * @param type          Type of the topic
 * @param message       Current message payload
 * @param visualizer    Visualizer object
 *
 * @return suitable     True, if the topic can be rendered with this function
 **/
function render_message_packet_topic(name, type, message, visualizer)
~~~

The visualizer base is attached to a canvas, which and also it's context are parameters of the ```visualizer``` object.
The function ```visualizer.defaultDownload(name)``` takes a named screenshot of the current rendering. Note, that also the download content can be overwritten by changing the self-explaining parameters ```visualizer.downloadName```, ```visualizer.downloadMIME```, ```visualizer.downloadData```.

## Third-party 

* [download](https://github.com/rndme/download)
* [eventemitter](https://github.com/Olical/EventEmitter)
* [joystick (patched)](https://github.com/bobboteck/JoyStick)
* [jquery](https://github.com/jquery/jquery)
* [plotly](https://github.com/plotly/plotly.js)
* [roslib](https://github.com/RobotWebTools/roslibjs)
