
# Mebo v1.0 HTTP API

The mebo toy robot is controlled by a simple http API. 
Commands are sent to an HTTP server running on the robot.


# General Information
 - Default IP Address: 192.168.222.1 (when direct connected)
 - Port: 80
 - Video feed: rtsp://{ip address}/streamhd/
 - User-Agent: com.skyrocket.srtmebo


# Miscellaneous Commands

## Adding Timestamp

URLs can append "*&ts={1}*" where timestamp is in "HHmmss" format.


## Mebo Settings

**System Settings**
|Setting|URL|Parameter/Return|
|--|--|--|
|Get Wifi Board Version|?req=get_version|N/A|
|Get Motherboard Version|?req=get_soc_version|N/A|
|Get UUID|?req=get_udid|UUID|
|Set UTC|?req=set_date&value={0}|Current time as 'yyyyMMddHHmm.ss'|
|Restart System|?req=restart_system|N/A|
|Reboot|?req=reboot|N/A
|Set Eye LED|?req=set_eye_led_brightness&value={0}|LED Brightness as Int)
|Set Mouth LED|?req=set_mouth_led_brightness&value={0}|LED Brightness as Int)
|Set Reduced Video p1|?req=set_video_bitrate&value=150|Send all 3 commands|
|Set Reduced Video p2|?req=set_resolution&value=480p|Send all 3 commands|
|Set Reduced Video p3|?req=set_video_qp&value=48|Send all 3 commands|


**Wireless Settings**
|Setting|URL|Parameter/Return|
|--|--|--|
|Set Router SSID|?req=setup_wireless_save&auth={0}&ssid={1}&key={2}|{Unknown,Open,None,Wep,Wpa,Wpa2},SSID,Password)|
|Set WIFI PSK|?req=set_wifi_wpa_psk&value={0}|Escaped HTML password|
|Router Scan|?req=get_rt_list|XML Formatted list of Routers|
|Get Wifi Security|?req=get_wifi_cert|Wifi Security Type|
|Get list of SSIDs|?req=setup_wireless_read|List of 3 SSIDs|
|Clear Wireless Index|?req=setup_wireless_clear&index={0}|Clears SSID at idx|
|Set SSID Scan Timer|?req=set_scan_timer&value={0}|Time in Seconds|
|Set Timer State 0|?req=set_timer_state&value=0|N/A|



# Movement

## Enums
Various parameters are presented to the user as strings but sent to the API as integers, the below tables list those values.


**Wheel Directions**

|Direction|Int Value|
|--|--|
|forward|0|
|forward_right|1|
|right|2|
|backward_right|3|
|backward|4|
|backward_left|5|
|left|6|
|forward_left|7|

**Wheel Durations**
|Duration (ms)|Int Value |
|--|--|
|100|0|
|250|1|
|500|2|
|1000|3|
|2000|4|

**Arm/Claw Movement**
|Part|Direction|Int Value|
|--|--|--|
|Claw|open|0|
|Claw|close|1|
|Hand|up|0|
|Hand|down|1|
|Shoulder|open|0|
|Shoulder|close|1|
|Wrist|left|0|
|Wrist|right|1|

## Joint Boundaries

A list of joint boundaries can be requested with the URL "*?req=get_boundary_position*" the response string is made of of a list of boundaries:

**Response Boundaries**:
* c_open (claw)
* c_close (claw)
* s_up (shoulder)
* s_down (shoulder)
* h_up (hand)
* h_down (hand)
* w_left (wrist)
* w_right (wrist)


## Wheel Movement

|Command|URL|Parameter(s)|
|--|--|--|
|InchWheels|?req=inch_{0}|WheelDirection|
|MoveWheelsForDistance|?req=move_{0}&value={1}&distance={2}|WheelDirection,Speed,ClickCount|
|MoveWheels2ForDistance|?req=move_{0}&lms={1}&rms={2}&distance={3}|WheelDirection,LeftWheelSpeed,RightWheelSpeed,ClickCount|
|StopWheels|?req=fb_stop|N/A|


## Shoulder Movement
|Command|URL|Parameter(s)|
|--|--|--|
|MoveShoulder|?req=s_{0}&value={1}&dur={2}|ShoulderDirection,Speed,Duration|
|MoveShoulderToPosition|?req=s_{0}&value={1}&pos={2}|ShoulderDirection,Speed,Position|
|InchShoulder|?req=inch_s_{0}|ShoulderDirection|
|StopShoulder|?req=s_stop|N/A|

## Wrist Movement
|Command|URL|Parameter(s)|
|--|--|--|
|TurnWrist|?req=w_{0}&value={1}&dur={2}|WristDirection,Speed,Duration|
|TurnWristToPosition|?req=w_{0}&value={1}&pos={2}|WristDirection,Speed,Position|
|InchWrist|?req=inch_w_{0}|WristDirection|
|StopWrist|?req=w_stop|N/A|

## Hand Movement
|Command|URL|Parameter(s)|
|--|--|--|
|MoveHand|?req=h_{0}&value={1}&dur={2}|HandDirection,Speed,Duration|
|MoveHandToPosition|?req=h_{0}&value={1}&pos={2}|HandDirection,Speed,Position|
|InchHand|?req=inch_h_{0}|HandDirection|
|StopHand|?req=h_stop|N/A|

## Claw Movement
|Command|URL|Parameter(s)|
|--|--|--|
|MoveClaw|?req=c_{0}&value={1}&dur={2}|ClawDirection,Speed,Duration|
|MoveClawToPosition|?req=c_{0}&value={1}&pos={2}|ClawDirection,Speed,Position|
|StopClaw|?req=c_stop|N/A|


