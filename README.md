# telegram_ros

Bridges between a [Telegram](https://telegram.org/) conversation and [ROS](http://ros.org).

Only a single Telegram user can send and receive text, images and locations to/from the ROS bridge.
A user must send the `/start` command to start a conversation. A new user can then `/start` as well and take over. 

Currently, there is *no* authentication (Issue #6)

## Travis CI Build Status

[![Build Status](https://travis-ci.org/tue-robotics/telegram_ros.svg)](https://travis-ci.org/tue-robotics/telegram_ros)

## Installation (from source)

Go to the `src` directory of your catkin workspace and clone the package from github:

    git clone https://github.com/tue-robotics/telegram_ros.git
    
Install the required dependencies:

    rosdep install --from-path -y -i telegram_ros
    
Compile your workspace

    catkin build # or catkin_make (make sure to refresh your workspace env afterwards)

## Create a bot

If you don't have a bot yet, chat to [BotFather](https://core.telegram.org/bots#6-botfather) in Telegram to create one. You can provide a name for your bot and you will receive the API token. 

## Run

    rosrun telegram_ros telegram_ros_bridge _token:=[YOUR_BOT_API_TOKEN]

## ROS API

### Topics

#### Output

- `message_to_ros` ([std_msgs/String](http://docs.ros.org/api/std_msgs/html/msg/String.html))
- `image_to_ros` ([sensor_msgs/Image](http://docs.ros.org/api/sensor_msgs/html/msg/Image.html))

#### Input

- `message_from_ros` ([std_msgs/String](http://docs.ros.org/api/std_msgs/html/msg/String.html))
- `image_from_ros` ([sensor_msgs/Image](http://docs.ros.org/api/sensor_msgs/html/msg/Image.html))

### Parameters

- `~token` (string): Telegram BOT API token
- `~caption_as_frame_id` (bool): Whether to put the caption of the image in the frame_id (default=`False`)
- `~whitelist/required` (bool): True when only whitelisted users can chat with the bot or False when everyone can use the bot (default=`False`)
- `~whitelist/users` (dict {string:int}): Mapping of username to Telegram user ID. Only these users are allowed to chat with the bot. 
    Users can be added with the `add_user_to_whitelist` service.
