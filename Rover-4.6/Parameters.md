
This is a complete list of the parameters which can be set via the MAVLink protocol in the EEPROM of your autopilot to control vehicle behaviour. This list is automatically generated from the latest ardupilot source code, and so may contain parameters which are not yet in the stable released versions of the code. Some parameters may only be available for developers, and are enabled at compile-time.

# Rover Parameters

## FORMAT_VERSION: Eeprom format version number

*Note: This parameter is for advanced users*

This value is incremented when changes are made to the eeprom format

## LOG_BITMASK: Log bitmask

*Note: This parameter is for advanced users*

Bitmap of what log types to enable in on-board logger. This value is made up of the sum of each of the log types you want to be saved. On boards supporting microSD cards or other large block-storage devices it is usually best just to enable all basic log types by setting this to 65535.

- Bitmask: 0:Fast Attitude,1:Medium Attitude,2:GPS,3:System Performance,4:Throttle,5:Navigation Tuning,7:IMU,8:Mission Commands,9:Battery Monitor,10:Rangefinder,11:Compass,12:Camera,13:Steering,14:RC Input-Output,19:Raw IMU,20:Video Stabilization,21:Optical Flow

## RST_SWITCH_CH: Reset Switch Channel

*Note: This parameter is for advanced users*

RC channel to use to reset to last flight mode after geofence takeover.

## INITIAL_MODE: Initial driving mode

*Note: This parameter is for advanced users*

This selects the mode to start in on boot. This is useful for when you want to start in AUTO mode on boot without a receiver. Usually used in combination with when AUTO_TRIGGER_PIN or AUTO_KICKSTART.

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## SYSID_THISMAV: MAVLink system ID of this vehicle

*Note: This parameter is for advanced users*

Allows setting an individual MAVLink system id for this vehicle to distinguish it from others on the same network

- Range: 1 255

## SYSID_MYGCS: MAVLink ground station ID

*Note: This parameter is for advanced users*

The identifier of the ground station in the MAVLink protocol. Don't change this unless you also modify the ground station to match.

- Range: 1 255

- Increment: 1

## TELEM_DELAY: Telemetry startup delay

The amount of time (in seconds) to delay radio telemetry to prevent an Xbee bricking on power up

- Units: s

- Range: 0 30

- Increment: 1

## GCS_PID_MASK: GCS PID tuning mask

*Note: This parameter is for advanced users*

bitmask of PIDs to send MAVLink PID_TUNING messages for

- Bitmask: 0:Steering,1:Throttle,2:Pitch,3:Left Wheel,4:Right Wheel,5:Sailboat Heel,6:Velocity North,7:Velocity East

## AUTO_TRIGGER_PIN: Auto mode trigger pin

pin number to use to enable the throttle in auto mode. If set to -1 then don't use a trigger, otherwise this is a pin number which if held low in auto mode will enable the motor to run. If the switch is released while in AUTO then the motor will stop again. This can be used in combination with INITIAL_MODE to give a 'press button to start' rover with no receiver.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|APM TriggerPin0|
|1|APM TriggerPin1|
|2|APM TriggerPin2|
|3|APM TriggerPin3|
|4|APM TriggerPin4|
|5|APM TriggerPin5|
|6|APM TriggerPin6|
|7|APM TriggerPin7|
|8|APM TriggerPin8|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## AUTO_KICKSTART: Auto mode trigger kickstart acceleration

X acceleration in meters/second/second to use to trigger the motor start in auto mode. If set to zero then auto throttle starts immediately when the mode switch happens, otherwise the rover waits for the X acceleration to go above this value before it will start the motor

- Units: m/s/s

- Range: 0 20

- Increment: 0.1

## CRUISE_SPEED: Target cruise speed in auto modes

The target speed in auto missions.

- Units: m/s

- Range: 0 100

- Increment: 0.1

## CRUISE_THROTTLE: Base throttle percentage in auto

The base throttle percentage to use in auto mode. The CRUISE_SPEED parameter controls the target speed, but the rover starts with the CRUISE_THROTTLE setting as the initial estimate for how much throttle is needed to achieve that speed. It then adjusts the throttle based on how fast the rover is actually going.

- Units: %

- Range: 0 100

- Increment: 1

## PILOT_STEER_TYPE: Pilot input steering type

Pilot RC input interpretation

|Value|Meaning|
|:---:|:---:|
|0|Default|
|1|Two Paddles Input|
|2|Direction reversed when backing up|
|3|Direction unchanged when backing up|

## FS_ACTION: Failsafe Action

What to do on a failsafe event

|Value|Meaning|
|:---:|:---:|
|0|Nothing|
|1|RTL|
|2|Hold|
|3|SmartRTL or RTL|
|4|SmartRTL or Hold|
|5|Terminate|

## FS_TIMEOUT: Failsafe timeout

The time in seconds that a failsafe condition must persist before the failsafe action is triggered

- Units: s

- Range: 1 100

- Increment: 0.5

## FS_THR_ENABLE: Throttle Failsafe Enable

The throttle failsafe allows you to configure a software failsafe activated by a setting on the throttle input channel to a low value. This can be used to detect the RC transmitter going out of range. Failsafe will be triggered when the throttle channel goes below the FS_THR_VALUE for FS_TIMEOUT seconds.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Enabled Continue with Mission in Auto|

## FS_THR_VALUE: Throttle Failsafe Value

The PWM level on the throttle channel below which throttle failsafe triggers.

- Range: 910 1100

- Increment: 1

## FS_GCS_ENABLE: GCS failsafe enable

Enable ground control station telemetry failsafe. When enabled the Rover will execute the FS_ACTION when it fails to receive MAVLink heartbeat packets for FS_TIMEOUT seconds.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Enabled Continue with Mission in Auto|

## FS_CRASH_CHECK: Crash check action

What to do on a crash event. When enabled the rover will go to hold if a crash is detected.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Hold|
|2|HoldAndDisarm|

## FS_EKF_ACTION: EKF Failsafe Action

*Note: This parameter is for advanced users*

Controls the action that will be taken when an EKF failsafe is invoked

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Hold|
|2|ReportOnly|

## FS_EKF_THRESH: EKF failsafe variance threshold

*Note: This parameter is for advanced users*

Allows setting the maximum acceptable compass and velocity variance

|Value|Meaning|
|:---:|:---:|
|0.6|Strict|
|0.8|Default|
|1.0|Relaxed|

## MODE_CH: Mode channel

*Note: This parameter is for advanced users*

RC Channel to use for driving mode control

## MODE1: Mode1

Driving mode for switch position 1 (910 to 1230 and above 2049)

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## MODE2: Mode2

Driving mode for switch position 2 (1231 to 1360)

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## MODE3: Mode3

Driving mode for switch position 3 (1361 to 1490)

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## MODE4: Mode4

Driving mode for switch position 4 (1491 to 1620)

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## MODE5: Mode5

Driving mode for switch position 5 (1621 to 1749)

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## MODE6: Mode6

Driving mode for switch position 6 (1750 to 2049)

|Value|Meaning|
|:---:|:---:|
|0|Manual|
|1|Acro|
|3|Steering|
|4|Hold|
|5|Loiter|
|6|Follow|
|7|Simple|
|8|Dock|
|9|Circle|
|10|Auto|
|11|RTL|
|12|SmartRTL|
|15|Guided|

## SYSID_ENFORCE: GCS sysid enforcement

*Note: This parameter is for advanced users*

This controls whether packets from other than the expected GCS system ID will be accepted

|Value|Meaning|
|:---:|:---:|
|0|NotEnforced|
|1|Enforced|

## TURN_RADIUS: Turn radius of vehicle

Turn radius of vehicle in meters while at low speeds.  Lower values produce tighter turns in steering mode

- Units: m

- Range: 0 10

- Increment: 0.1

## ACRO_TURN_RATE: Acro mode turn rate maximum

Acro mode turn rate maximum

- Units: deg/s

- Range: 0 360

- Increment: 1

## RTL_SPEED: Return-to-Launch speed default

Return-to-Launch speed default.  If zero use WP_SPEED or CRUISE_SPEED.

- Units: m/s

- Range: 0 100

- Increment: 0.1

## FRAME_CLASS: Frame Class

Frame Class

|Value|Meaning|
|:---:|:---:|
|0|Undefined|
|1|Rover|
|2|Boat|
|3|BalanceBot|

## BAL_PITCH_MAX: BalanceBot Maximum Pitch

Pitch angle in degrees at 100% throttle

- Units: deg

- Range: 0 15

- Increment: 0.1

## CRASH_ANGLE: Crash Angle

Pitch/Roll angle limit in degrees for crash check. Zero disables check

- Units: deg

- Range: 0 60

- Increment: 1

## FRAME_TYPE: Frame Type

Frame Type

|Value|Meaning|
|:---:|:---:|
|0|Undefined|
|1|Omni3|
|2|OmniX|
|3|OmniPlus|
|4|Omni3Mecanum|

- RebootRequired: True

## LOIT_TYPE: Loiter type

Loiter behaviour when moving to the target point

|Value|Meaning|
|:---:|:---:|
|0|Forward or reverse to target point|
|1|Always face bow towards target point|
|2|Always face stern towards target point|

## SIMPLE_TYPE: Simple_Type

Simple mode types

|Value|Meaning|
|:---:|:---:|
|0|InitialHeading|
|1|CardinalDirections|

- RebootRequired: True

## LOIT_RADIUS: Loiter radius

Vehicle will drift when within this distance of the target position

- Units: m

- Range: 0 20

- Increment: 1

## MIS_DONE_BEHAVE: Mission done behave

Behaviour after mission completes

|Value|Meaning|
|:---:|:---:|
|0|Hold in Auto Mode|
|1|Loiter in Auto Mode|
|2|Acro Mode|
|3|Manual Mode|

## BAL_PITCH_TRIM: Balance Bot pitch trim angle

Balance Bot pitch trim for balancing. This offsets the tilt of the center of mass.

- Units: deg

- Range: -2 2

- Increment: 0.1

## STICK_MIXING: Stick Mixing

*Note: This parameter is for advanced users*

When enabled, this adds steering user stick input in auto modes, allowing the user to have some degree of control without changing modes.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SPEED_MAX: Speed maximum

*Note: This parameter is for advanced users*

Maximum speed vehicle can obtain at full throttle. If 0, it will be estimated based on CRUISE_SPEED and CRUISE_THROTTLE.

- Units: m/s

- Range: 0 30

- Increment: 0.1

## LOIT_SPEED_GAIN: Loiter speed gain

*Note: This parameter is for advanced users*

Determines how agressively LOITER tries to correct for drift from loiter point. Higher is faster but default should be acceptable.

- Range: 0 5

- Increment: 0.01

## FS_OPTIONS: Failsafe Options

*Note: This parameter is for advanced users*

Bitmask to enable failsafe options

- Bitmask: 0:Failsafe enabled in Hold mode

## GUID_OPTIONS: Guided mode options

*Note: This parameter is for advanced users*

Options that can be applied to change guided mode behaviour

- Bitmask: 6:SCurves used for navigation

## MANUAL_OPTIONS: Manual mode options

*Note: This parameter is for advanced users*

Manual mode specific options

- Bitmask: 0:Enable steering speed scaling

## MANUAL_STR_EXPO: Manual Steering Expo

*Note: This parameter is for advanced users*

Manual steering expo to allow faster steering when stick at edges

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|0.1|Very Low|
|0.2|Low|
|0.3|Medium|
|0.4|High|
|0.5|Very High|

- Range: -0.5 0.95

## FS_GCS_TIMEOUT: GCS failsafe timeout

Timeout before triggering the GCS failsafe

- Units: s

- Range: 2 120

- Increment: 1

## CH7_OPTION: Channel 7 option

What to do use channel 7 for

|Value|Meaning|
|:---:|:---:|
|0|Nothing|
|1|SaveWaypoint|
|2|LearnCruiseSpeed|
|3|ArmDisarm|
|4|Manual|
|5|Acro|
|6|Steering|
|7|Hold|
|8|Auto|
|9|RTL|
|10|SmartRTL|
|11|Guided|
|12|Loiter|

## AUX_CH: Auxiliary switch channel

*Note: This parameter is for advanced users*

RC Channel to use for auxiliary functions including saving waypoints

## PIVOT_TURN_ANGLE: Pivot turn angle

Navigation angle threshold in degrees to switch to pivot steering. This allows you to setup a skid steering rover to turn on the spot in auto mode when the angle it needs to turn it greater than this angle. An angle of zero means to disable pivot turning. Note that you will probably also want to set a low value for WP_RADIUS to get neat turns.

- Units: deg

- Range: 0 360

- Increment: 1

## PIVOT_TURN_RATE: Pivot turn rate

Desired pivot turn rate in deg/s.

- Units: deg/s

- Range: 0 360

- Increment: 1

# VEHICLE Parameters

## FLTMODE_GCSBLOCK: Flight mode block from GCS

Bitmask of flight modes to disable for GCS selection. Mode can still be accessed via RC or failsafe.

- Bitmask: 0:Manual,1:Acro,2:Steering,3:Loiter,4:Follow,5:Simple,6:Circle,7:Auto,8:RTL,9:SmartRTL,10:Guided,11:Dock

# Lua Script Parameters

## CAM1_THERM_PAL: Camera1 Thermal Palette

thermal image colour palette

|Value|Meaning|
|:---:|:---:|
|-1|Leave Unchanged|
|0|WhiteHot|
|2|Sepia|
|3|IronBow|
|4|Rainbow|
|5|Night|
|6|Aurora|
|7|RedHot|
|8|Jungle|
|9|Medical|
|10|BlackHot|
|11|GloryHot|

## CAM1_THERM_GAIN: Camera1 Thermal Gain

thermal image temperature range

|Value|Meaning|
|:---:|:---:|
|-1|Leave Unchanged|
|0|LowGain (50C to 550C)|
|1|HighGain (-20C to 150C)|

## CAM1_THERM_RAW: Camera1 Thermal Raw Data

save images with raw temperatures

|Value|Meaning|
|:---:|:---:|
|-1|Leave Unchanged|
|0|Disabled (30fps)|
|1|Enabled (25 fps)|

- Units: m

## BATT_SOC_COUNT: Count of SOC estimators

Number of battery SOC estimators

- Range: 0 4

## BATT_SOC1_IDX: Battery estimator index

Battery estimator index

- Range: 0 4

## BATT_SOC1_NCELL: Battery estimator cell count

Battery estimator cell count

- Range: 0 48

## BATT_SOC1_C1: Battery estimator coefficient1

Battery estimator coefficient1

- Range: 100 200

## BATT_SOC1_C2: Battery estimator coefficient2

Battery estimator coefficient2

- Range: 2 5

## BATT_SOC1_C3: Battery estimator coefficient3

Battery estimator coefficient3

- Range: 0.01 0.5

## BATT_SOC2_IDX: Battery estimator index

Battery estimator index

- Range: 0 4

## BATT_SOC2_NCELL: Battery estimator cell count

Battery estimator cell count

- Range: 0 48

## BATT_SOC2_C1: Battery estimator coefficient1

Battery estimator coefficient1

- Range: 100 200

## BATT_SOC2_C2: Battery estimator coefficient2

Battery estimator coefficient2

- Range: 2 5

## BATT_SOC2_C3: Battery estimator coefficient3

Battery estimator coefficient3

- Range: 0.01 0.5

## BATT_SOC3_IDX: Battery estimator index

Battery estimator index

- Range: 0 4

## BATT_SOC3_NCELL: Battery estimator cell count

Battery estimator cell count

- Range: 0 48

## BATT_SOC3_C1: Battery estimator coefficient1

Battery estimator coefficient1

- Range: 100 200

## BATT_SOC3_C2: Battery estimator coefficient2

Battery estimator coefficient2

- Range: 2 5

## BATT_SOC3_C3: Battery estimator coefficient3

Battery estimator coefficient3

- Range: 0.01 0.5

## BATT_SOC4_IDX: Battery estimator index

Battery estimator index

- Range: 0 4

## BATT_SOC4_NCELL: Battery estimator cell count

Battery estimator cell count

- Range: 0 48

## BATT_SOC4_C1: Battery estimator coefficient1

Battery estimator coefficient1

- Range: 100 200

## BATT_SOC4_C2: Battery estimator coefficient2

Battery estimator coefficient2

- Range: 2 5

## BATT_SOC4_C3: Battery estimator coefficient3

Battery estimator coefficient3

- Range: 0.01 0.5

## ESRC_EXTN_THRESH: EKF Source ExternalNav Innovation Threshold

ExternalNav may be used if innovations are below this threshold

- Range: 0 1

## ESRC_EXTN_QUAL: EKF Source ExternalNav Quality Threshold

ExternalNav may be used if quality is above this threshold

- Range: 0 100

- Units: %

## ESRC_FLOW_THRESH: EKF Source OpticalFlow Innovation Threshold

OpticalFlow may be used if innovations are below this threshold

- Range: 0 1

## ESRC_FLOW_QUAL: EKF Source OpticalFlow Quality Threshold

OpticalFlow may be used if quality is above this threshold

- Range: 0 100

- Units: %

## ESRC_RNGFND_MAX: EKF Source Rangefinder Max

OpticalFlow may be used if rangefinder distance is below this threshold

- Range: 0 50

- Units: m

## WEB_ENABLE: enable web server

enable web server

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## WEB_BIND_PORT: web server TCP port

web server TCP port

- Range: 1 65535

## WEB_DEBUG: web server debugging

*Note: This parameter is for advanced users*

web server debugging

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## WEB_BLOCK_SIZE: web server block size

*Note: This parameter is for advanced users*

web server block size for download

- Range: 1 65535

## WEB_TIMEOUT: web server timeout

*Note: This parameter is for advanced users*

timeout for inactive connections

- Units: s

- Range: 0.1 60

## WEB_SENDFILE_MIN: web server minimum file size for sendfile

*Note: This parameter is for advanced users*

sendfile is an offloading mechanism for faster file download. If this is non-zero and the file is larger than this size then sendfile will be used for file download

- Range: 0 10000000

## DR_ENABLE: Deadreckoning Enable

Deadreckoning Enable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## DR_ENABLE_DIST: Deadreckoning Enable Distance

Distance from home (in meters) beyond which the dead reckoning will be enabled

- Units: m

## DR_GPS_SACC_MAX: Deadreckoning GPS speed accuracy maximum threshold

GPS speed accuracy maximum, above which deadreckoning home will begin (default is 0.8).  Lower values trigger with good GPS quality, higher values will allow poorer GPS before triggering. Set to 0 to disable use of GPS speed accuracy

- Range: 0 10

## DR_GPS_SAT_MIN: Deadreckoning GPS satellite count min threshold

GPS satellite count threshold below which deadreckoning home will begin (default is 6).  Higher values trigger with good GPS quality, Lower values trigger with worse GPS quality. Set to 0 to disable use of GPS satellite count

- Range: 0 30

## DR_GPS_TRIGG_SEC: Deadreckoning GPS check trigger seconds

GPS checks must fail for this many seconds before dead reckoning will be triggered

- Units: s

## DR_FLY_ANGLE: Deadreckoning Lean Angle

lean angle (in degrees) during deadreckoning

- Units: deg

- Range: 0 45

## DR_FLY_ALT_MIN: Deadreckoning Altitude Min

Copter will fly at at least this altitude (in meters) above home during deadreckoning

- Units: m

- Range: 0 1000

## DR_FLY_TIMEOUT: Deadreckoning flight timeout

Copter will attempt to switch to NEXT_MODE after this many seconds of deadreckoning.  If it cannot switch modes it will continue in Guided_NoGPS.  Set to 0 to disable timeout

- Units: s

## DR_NEXT_MODE: Deadreckoning Next Mode

Copter switch to this mode after GPS recovers or DR_FLY_TIMEOUT has elapsed.  Default is 6/RTL.  Set to -1 to return to mode used before deadreckoning was triggered

|Value|Meaning|
|:---:|:---:|
|2|AltHold|
|3|Auto|
|4|Guided|
|5|Loiter|
|6|RTL|
|7|Circle|
|9|Land|
|16|PosHold|
|17|Brake|
|20|Guided_NoGPS|
|21|Smart_RTL|
|27|Auto RTL|

## VID1_CAMMODEL: Camera1 Video Stream Camera Model

Video stream camera model

|Value|Meaning|
|:---:|:---:|
|0|Unknown|
|1|Siyi A8|
|2|Siyi ZR10|
|3|Siyi ZR30|
|4|Siyi ZT30 Zoom|
|5|Siyi ZT30 Wide|
|6|Siyi ZT30 IR|
|7|Siyi ZT6 RGB|
|8|Siyi ZT6 IR|
|9|Herelink WifiAP|
|10|Herelink USB-tethering|
|11|Topotek 1080p|
|12|Topotek 480p|
|13|Viewpro|

## VID1_ID: Camera1 Video Stream Id

Video stream id

- Range: 0 50

## VID1_TYPE: Camera1 Video Stream Type

Video stream type

|Value|Meaning|
|:---:|:---:|
|0|RTSP|
|1|RTPUDP|
|2|TCP_MPEG|
|3|MPEG_TS|

## VID1_FLAG: Camera1 Video Stream Flags

Video stream flags

- Bitmask: 0:Running,1:Thermal,2:Thermal Range Enabled

## VID1_FRAME_RATE: Camera1 Video Stream Frame Rate

Video stream frame rate

- Range: 0 50

## VID1_HRES: Camera1 Video Stream Horizontal Resolution

Video stream horizontal resolution

- Range: 0 4096

## VID1_VRES: Camera1 Video Stream Vertical Resolution

Video stream vertical resolution

- Range: 0 4096

## VID1_BITRATE: Camera1 Video Stream Bitrate

Video stream bitrate

- Range: 0 10000

## VID1_HFOV: Camera1 Video Stream Horizontal FOV

Video stream horizontal FOV

- Range: 0 360

## VID1_ENCODING: Camera1 Video Stream Encoding

Video stream encoding

|Value|Meaning|
|:---:|:---:|
|0|Unknown|
|1|H264|
|2|H265|

## VID1_IPADDR0: Camera1 Video Stream IP Address 0

Video stream IP Address first octet

- Range: 0 255

## VID1_IPADDR1: Camera1 Video Stream IP Address 1

Video stream IP Address second octet

- Range: 0 255

## VID1_IPADDR2: Camera1 Video Stream IP Address 2

Video stream IP Address third octet

- Range: 0 255

## VID1_IPADDR3: Camera1 Video Stream IP Address 3

Video stream IP Address fourth octet

- Range: 0 255

## VID1_IPPORT: Camera1 Video Stream IP Address Port

Video stream IP Address Port

- Range: 0 65535

## RTUN_ENABLE: Rover Quicktune enable

Enable quicktune system

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## RTUN_AXES: Rover Quicktune axes

axes to tune

- Bitmask: 0:Steering,1:Speed

## RTUN_STR_FFRATIO: Rover Quicktune Steering Rate FeedForward ratio

Ratio between measured response and FF gain. Raise this to get a higher FF gain

- Range: 0 1.0

## RTUN_STR_P_RATIO: Rover Quicktune Steering FF to P ratio

Ratio between steering FF and P gains. Raise this to get a higher P gain, 0 to leave P unchanged

- Range: 0 2.0

## RTUN_STR_I_RATIO: Rover Quicktune Steering FF to I ratio

Ratio between steering FF and I gains. Raise this to get a higher I gain, 0 to leave I unchanged

- Range: 0 2.0

## RTUN_SPD_FFRATIO: Rover Quicktune Speed FeedForward (equivalent) ratio

Ratio between measured response and CRUISE_THROTTLE value. Raise this to get a higher CRUISE_THROTTLE value

- Range: 0 1.0

## RTUN_SPD_P_RATIO: Rover Quicktune Speed FF to P ratio

Ratio between speed FF and P gain. Raise this to get a higher P gain, 0 to leave P unchanged

- Range: 0 2.0

## RTUN_SPD_I_RATIO: Rover Quicktune Speed FF to I ratio

Ratio between speed FF and I gain. Raise this to get a higher I gain, 0 to leave I unchanged

- Range: 0 2.0

## RTUN_AUTO_FILTER: Rover Quicktune auto filter enable

When enabled the PID filter settings are automatically set based on INS_GYRO_FILTER

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## RTUN_AUTO_SAVE: Rover Quicktune auto save

Number of seconds after completion of tune to auto-save. This is useful when using a 2 position switch for quicktune

- Units: s

## RTUN_RC_FUNC: Rover Quicktune RC function

RCn_OPTION number to use to control tuning stop/start/save

|Value|Meaning|
|:---:|:---:|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

## RTUN_SPEED_MIN: Rover Quicktune minimum speed for tuning

The mimimum speed in m/s required for tuning to start

- Units: m/s

- Range: 0.1 0.5

## PREV_ENABLE: parameter reversion enable

Enable parameter reversion system

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## PREV_RC_FUNC: param reversion RC function

RCn_OPTION number to used to trigger parameter reversion

## TERR_BRK_ENABLE: terrain brake enable

terrain brake enable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## TERR_BRK_ALT: terrain brake altitude

terrain brake altitude. The altitude above the ground below which BRAKE mode will be engaged if in LOITER mode.

- Range: 1 100

- Units: m

## TERR_BRK_HDIST: terrain brake home distance

terrain brake home distance. The distance from home where the auto BRAKE will be enabled. When within this distance of home the script will not activate

- Range: 0 1000

- Units: m

## TERR_BRK_SPD: terrain brake speed threshold

terrain brake speed threshold. Don't trigger BRAKE if both horizontal speed and descent rate are below this threshold. By setting this to a small value this can be used to allow the user to climb up to a safe altitude in LOITER mode. A value of 0.5 is recommended if you want to use LOITER to recover from an emergency terrain BRAKE mode change.

- Range: 0 5

- Units: m/s

## WINCH_RATE_UP: WinchControl Rate Up

Maximum rate when retracting line

- Range: 0.1 5.0

## WINCH_RATE_DN: WinchControl Rate Down

Maximum rate when releasing line

- Range: 0.1 5.0

## WINCH_RC_FUNC: Winch Rate Control RC function

RCn_OPTION number to use to control winch rate

|Value|Meaning|
|:---:|:---:|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

## POI_DIST_MAX: Mount POI distance max

POI's max distance (in meters) from the vehicle

- Range: 0 10000

## SHIP_ENABLE: Ship landing enable

Enable ship landing system

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SHIP_LAND_ANGLE: Ship landing angle

Angle from the stern of the ship for landing approach. Use this to ensure that on a go-around that ship superstructure and cables are avoided. A value of zero means to approach from the rear of the ship. A value of 90 means the landing will approach from the port (left) side of the ship. A value of -90 will mean approaching from the starboard (right) side of the ship. A value of 180 will approach from the bow of the ship. This parameter is combined with the sign of the RTL_RADIUS parameter to determine the holdoff pattern. If RTL_RADIUS is positive then a clockwise loiter is performed, if RTL_RADIUS is negative then a counter-clockwise loiter is used.

- Range: -180 180

- Units: deg

## SHIP_AUTO_OFS: Ship automatic offset trigger

Settings this parameter to one triggers an automatic follow offset calculation based on current position of the vehicle and the landing target. NOTE: This parameter will auto-reset to zero once the offset has been calculated.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Trigger|

## QUIK_ENABLE: Quicktune enable

Enable quicktune system

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## QUIK_AXES: Quicktune axes

axes to tune

- Bitmask: 0:Roll,1:Pitch,2:Yaw

## QUIK_DOUBLE_TIME: Quicktune doubling time

Time to double a tuning parameter. Raise this for a slower tune.

- Range: 5 20

- Units: s

## QUIK_GAIN_MARGIN: Quicktune gain margin

Reduction in gain after oscillation detected. Raise this number to get a more conservative tune

- Range: 20 80

- Units: %

## QUIK_OSC_SMAX: Quicktune oscillation rate threshold

Threshold for oscillation detection. A lower value will lead to a more conservative tune.

- Range: 1 10

## QUIK_YAW_P_MAX: Quicktune Yaw P max

Maximum value for yaw P gain

- Range: 0.1 3

## QUIK_YAW_D_MAX: Quicktune Yaw D max

Maximum value for yaw D gain

- Range: 0.001 1

## QUIK_RP_PI_RATIO: Quicktune roll/pitch PI ratio

Ratio between P and I gains for roll and pitch. Raise this to get a lower I gain

- Range: 0.5 1.0

## QUIK_Y_PI_RATIO: Quicktune Yaw PI ratio

Ratio between P and I gains for yaw. Raise this to get a lower I gain

- Range: 0.5 20

## QUIK_AUTO_FILTER: Quicktune auto filter enable

When enabled the PID filter settings are automatically set based on INS_GYRO_FILTER

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## QUIK_AUTO_SAVE: Quicktune auto save

Number of seconds after completion of tune to auto-save. This is useful when using a 2 position switch for quicktune

- Units: s

## QUIK_RC_FUNC: Quicktune RC function

RCn_OPTION number to use to control tuning stop/start/save

## QUIK_MAX_REDUCE: Quicktune maximum gain reduction

This controls how much quicktune is allowed to lower gains from the original gains. If the vehicle already has a reasonable tune and is not oscillating then you can set this to zero to prevent gain reductions. The default of 20% is reasonable for most vehicles. Using a maximum gain reduction lowers the chance of an angle P oscillation happening if quicktune gets a false positive oscillation at a low gain, which can result in very low rate gains and a dangerous angle P oscillation.

- Units: %

- Range: 0 100

## QUIK_OPTIONS: Quicktune options

Additional options. When the Two Position Switch option is enabled then a high switch position will start the tune, low will disable the tune. you should also set a QUIK_AUTO_SAVE time so that you will be able to save the tune.

- Bitmask: 0:UseTwoPositionSwitch

## QUIK_ANGLE_MAX: maximum angle error for tune abort

If while tuning the angle error goes over this limit then the tune will aborts to prevent a bad oscillation in the case of the tuning algorithm failing. If you get an error "Tuning: attitude error ABORTING" and you think it is a false positive then you can either raise this parameter or you can try increasing the QUIK_DOUBLE_TIME to do the tune more slowly. A value of zero disables this check.

- Units: deg

## PLND_ALT_CUTOFF: Precland altitude cutoff

The altitude (rangefinder distance) below which we stop using the precision landing sensor and continue landing

- Range: 0 20

- Units: m

## DIST_CUTOFF: Precland distance cutoff

The distance from target beyond which the target is ignored

- Range: 0 100

- Units: m

## RCK_FORCEHL: Force enable High Latency mode

Automatically enables High Latency mode if not already enabled

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## RCK_PERIOD: Update rate

When in High Latency mode, send Rockblock updates every N seconds

- Range: 0 600

- Units: s

## RCK_DEBUG: Display Rockblock debugging text

Sends Rockblock debug text to GCS via statustexts

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## RCK_ENABLE: Enable Message transmission

Enables the Rockblock sending and recieving

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## CGA_RATIO: CoG adjustment ratio

*Note: This parameter is for advanced users*

The ratio between the front and back motor outputs during steady-state hover. Positive when the CoG is in front of the motors midpoint (front motors work harder).

- Range: 0.5 2

## SLUP_ENABLE: Slung Payload enable

Slung Payload enable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SLUP_VEL_P: Slung Payload Velocity P gain

Slung Payload Velocity P gain, higher values will result in faster movements in sync with payload

- Range: 0 0.8

## SLUP_DIST_MAX: Slung Payload horizontal distance max

Oscillation is suppressed when vehicle and payload are no more than this distance horizontally.  Set to 0 to always suppress

- Range: 0 30

## SLUP_SYSID: Slung Payload mavlink system id

Slung Payload mavlink system id.  0 to use any/all system ids

- Range: 0 255

## SLUP_WP_POS_P: Slung Payload return to WP position P gain

WP position P gain. higher values will result in vehicle moving more quickly back to the original waypoint

- Range: 0 1

## SLUP_RESTOFS_TC: Slung Payload resting offset estimate filter time constant

payload's position estimator's time constant used to compensate for GPS errors and wind.  Higher values result in smoother estimate but slower response

- Range: 1 20

## SLUP_DEBUG: Slung Payload debug output

Slung payload debug output, set to 1 to enable debug

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## AEROM_ANG_ACCEL: Angular acceleration limit

Maximum angular acceleration in maneuvers

- Units: deg/s/s

## AEROM_ANG_TC: Roll control filtertime constant

This is the time over which we filter the desired roll to smooth it

- Units: s

## AEROM_THR_PIT_FF: Throttle feed forward from pitch

This controls how much extra throttle to add based on pitch ange. The value is for 90 degrees and is applied in proportion to pitch

- Units: %

## AEROM_SPD_P: P gain for speed controller

This controls how rapidly the throttle is raised to compensate for a speed error

- Units: %

## AEROM_SPD_I: I gain for speed controller

This controls how rapidly the throttle is raised to compensate for a speed error

- Units: %

## AEROM_ROL_COR_TC: Roll control time constant

This is the time constant for correcting roll errors. A smaller value leads to faster roll corrections

- Units: s

## AEROM_TIME_COR_P: Time constant for correction of our distance along the path

This is the time constant for correcting path position errors

- Units: s

## AEROM_ERR_COR_P: P gain for path error corrections

This controls how rapidly we correct back onto the desired path

## AEROM_ERR_COR_D: D gain for path error corrections

This controls how rapidly we correct back onto the desired path

## AEROM_ENTRY_RATE: The roll rate to use when entering a roll maneuver

This controls how rapidly we roll into a new orientation

- Units: deg/s

## AEROM_THR_LKAHD: The lookahead for throttle control

This controls how far ahead we look in time along the path for the target throttle

- Units: s

## AEROM_DEBUG: Debug control

This controls the printing of extra debug information on paths

## AEROM_THR_MIN: Minimum Throttle

Lowest throttle used during maneuvers

- Units: %

## AEROM_THR_BOOST: Throttle boost

This is the extra throttle added in schedule elements marked as needing a throttle boost

- Units: %

## AEROM_YAW_ACCEL: Yaw acceleration

This is maximum yaw acceleration to use

- Units: deg/s/s

## AEROM_LKAHD: Lookahead

This is how much time to look ahead in the path for calculating path rates

- Units: s

## AEROM_PATH_SCALE: Path Scale

Scale factor for Path/Box size. 0.5 would half the distances in maneuvers. Radii are unaffected.

- Range: 0.1 100

## AEROM_BOX_WIDTH: Box Width

Length of aerobatic "box" 

- Units: m

## AEROM_STALL_THR: Stall turn throttle

Amount of throttle to reduce to for a stall turn

- Units: %

## AEROM_STALL_PIT: Stall turn pitch threshold

Pitch threashold for moving to final stage of stall turn

- Units: deg

## AEROM_KE_RUDD: KnifeEdge Rudder

Percent of rudder normally uses to sustain knife-edge at trick speed

- Units: %

## AEROM_KE_RUDD_LK: KnifeEdge Rudder lookahead

Time to look ahead in the path to calculate rudder correction for bank angle

- Units: s

## AEROM_ALT_ABORT: Altitude Abort

Maximum allowable loss in altitude during a trick or sequence from its starting altitude.

- Units: m

## AEROM_TS_P: Timesync P gain

This controls how rapidly two aircraft are brought back into time sync

## AEROM_TS_I: Timesync I gain

This controls how rapidly two aircraft are brought back into time sync

## AEROM_TS_SPDMAX: Timesync speed max

This sets the maximum speed adjustment for time sync between aircraft

- Units: m/s

## AEROM_TS_RATE: Timesync rate of send of NAMED_VALUE_FLOAT data

This sets the rate we send data for time sync between aircraft

- Units: Hz

## AEROM_MIS_ANGLE: Mission angle

When set to a non-zero value, this is the assumed direction of the mission. Otherwise the waypoint angle is used

- Units: deg

## AEROM_OPTIONS: Aerobatic options

Options to control aerobatic behavior

- Bitmask: 0:UseRTLOnAbort, 1:AddAtToMessages, 2:DualAircraftSynchronised

- Units: deg

## TRIK_ENABLE: Tricks on Switch Enable

Enables Tricks on Switch. TRIK params hidden until enabled

## TRIK_SEL_FN: Trik Selection Scripting Function

Setting an RC channel's _OPTION to this value will use it for trick selection

- Range: 301 307

## TRIK_ACT_FN: Trik Action Scripting Function

Setting an RC channel's _OPTION to this value will use it for trick action (abort,announce,execute)

- Range: 301 307

## TRIK_COUNT: Trik Count

Number of tricks which can be selected over the range of the trik selection RC channel

- Range: 1 11

## EFI_INF_ENABLE: EFI INF-Inject enable

Enable EFI INF-Inject driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_INF_OPTIONS: EFI INF-Inject options

EFI INF driver options

- Bitmask: 0:EnableLogging

## EFI_INF_THR_HZ: EFI INF-Inject throttle rate

EFI INF throttle output rate

- Range: 0 50

- Units: Hz

## EFI_INF_IGN_AUX: EFI INF-Inject ignition aux function

EFI INF throttle ignition aux function

## DJIR_DEBUG: DJIRS2 debug

*Note: This parameter is for advanced users*

Enable DJIRS2 debug

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Enabled with attitude reporting|

## DJIR_UPSIDEDOWN: DJIRS2 upside down

DJIRS2 upside down

|Value|Meaning|
|:---:|:---:|
|0|Right side up|
|1|Upside down|

## EFI_SVF_ENABLE: Generator SVFFI enable

Enable SVFFI generator support

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_SVF_ARMCHECK: Generator SVFFI arming check

Check for Generator ARM state before arming

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BATT_ANX_ENABLE: Enable ANX battery support

Enable ANX battery support

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BATT_ANX_CANDRV: Set ANX CAN driver

Set ANX CAN driver

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|1stCANDriver|
|2|2ndCanDriver|

## BATT_ANX_INDEX: ANX CAN battery index

ANX CAN battery index

- Range: 1 10

## BATT_ANX_OPTIONS: ANX CAN battery options

*Note: This parameter is for advanced users*

ANX CAN battery options

- Bitmask: 0:LogAllFrames

## EFI_DLA_ENABLE: EFI DLA enable

Enable EFI DLA driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_DLA_LPS: EFI DLA fuel scale

EFI DLA litres of fuel per second of injection time

- Range: 0.00001 1

- Units: litres

## EFI_SP_ENABLE: Enable SkyPower EFI support

Enable SkyPower EFI support

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_SP_CANDRV: Set SkyPower EFI CAN driver

Set SkyPower EFI CAN driver

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|1stCANDriver|
|2|2ndCanDriver|

## EFI_SP_UPDATE_HZ: SkyPower EFI update rate

*Note: This parameter is for advanced users*

SkyPower EFI update rate

- Range: 10 200

- Units: Hz

## EFI_SP_THR_FN: SkyPower EFI throttle function

SkyPower EFI throttle function. This sets which SERVOn_FUNCTION to use for the target throttle. This should be 70 for fixed wing aircraft and 31 for helicopter rotor speed control

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|70|FixedWing|
|31|HeliRSC|

## EFI_SP_THR_RATE: SkyPower EFI throttle rate

*Note: This parameter is for advanced users*

SkyPower EFI throttle rate. This sets rate at which throttle updates are sent to the engine

- Range: 10 100

- Units: Hz

## EFI_SP_START_FN: SkyPower EFI start function

SkyPower EFI start function. This is the RCn_OPTION value to use to find the R/C channel used for controlling engine start

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|300|300|
|301|301|
|302|302|
|303|303|
|304|304|
|305|305|
|306|306|
|307|307|

## EFI_SP_GEN_FN: SkyPower EFI generator control function

SkyPower EFI generator control function. This is the RCn_OPTION value to use to find the R/C channel used for controlling generator start/stop

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|300|300|
|301|301|
|302|302|
|303|303|
|304|304|
|305|305|
|306|306|
|307|307|

## EFI_SP_MIN_RPM: SkyPower EFI minimum RPM

*Note: This parameter is for advanced users*

SkyPower EFI minimum RPM. This is the RPM below which the engine is considered to be stopped

- Range: 1 1000

## EFI_SP_TLM_RT: SkyPower EFI telemetry rate

*Note: This parameter is for advanced users*

SkyPower EFI telemetry rate. This is the rate at which extra telemetry values are sent to the GCS

- Range: 1 10

- Units: Hz

## EFI_SP_LOG_RT: SkyPower EFI log rate

*Note: This parameter is for advanced users*

SkyPower EFI log rate. This is the rate at which extra logging of the SkyPower EFI is performed

- Range: 1 50

- Units: Hz

## EFI_SP_ST_DISARM: SkyPower EFI allow start disarmed

SkyPower EFI allow start disarmed. This controls if starting the engine while disarmed is allowed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_SP_MODEL: SkyPower EFI ECU model

SkyPower EFI ECU model

|Value|Meaning|
|:---:|:---:|
|0|SRE_180|
|1|SP_275|

## EFI_SP_GEN_CTRL: SkyPower EFI enable generator control

SkyPower EFI enable generator control

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_SP_RST_TIME: SkyPower EFI restart time

SkyPower EFI restart time. If engine should be running and it has stopped for this amount of time then auto-restart. To disable this feature set this value to zero.

- Range: 0 10

- Units: s

## EFI_H6K_ENABLE: Enable Halo6000 EFI driver

Enable Halo6000 EFI driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_H6K_CANDRV: Halo6000 CAN driver

Halo6000 CAN driver. Use 1 for first CAN scripting driver, 2 for 2nd driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|FirstCAN|
|2|SecondCAN|

## EFI_H6K_START_FN: Halo6000 start auxilliary function

The RC auxilliary function number for start/stop of the generator. Zero to disable start function

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|300|300|
|301|301|
|302|302|
|303|303|
|304|304|
|305|305|
|306|306|
|307|307|

## EFI_H6K_TELEM_RT: Halo6000 telemetry rate

The rate that additional generator telemetry is sent

- Units: Hz

## EFI_H6K_FUELTOT: Halo6000 total fuel capacity

The capacity of the tank in litres

- Units: litres

## EFI_H6K_OPTIONS: Halo6000 options

Halo6000 options

- Bitmask: 0:LogAllCanPackets

## EFI_2K_ENABLE: Enable NMEA 2000 EFI driver

Enable NMEA 2000 EFI driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_2K_CANDRV: NMEA 2000 CAN driver

NMEA 2000 CAN driver. Use 1 for first CAN scripting driver, 2 for 2nd driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|FirstCAN|
|2|SecondCAN|

## EFI_2K_OPTIONS: NMEA 2000 options

NMEA 2000 driver options

- Bitmask: 0:EnableLogging

## ESC_HW_ENABLE: Hobbywing ESC Enable

Enable Hobbywing ESC telemetry

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## ESC_HW_POLES: Hobbywing ESC motor poles

Number of motor poles for eRPM scaling

- Range: 1 50

## ESC_HW_OFS: Hobbywing ESC motor offset

Motor number offset of first ESC

- Range: 0 31

## VIEP_DEBUG: ViewPro debug

*Note: This parameter is for advanced users*

ViewPro debug

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Enabled including attitude reporting|

## VIEP_CAM_SWLOW: ViewPro Camera For Switch Low

Camera selection when switch is in low position

|Value|Meaning|
|:---:|:---:|
|0|No change in camera selection|
|1|EO1|
|2|IR thermal|
|3|EO1 + IR Picture-in-picture|
|4|IR + EO1 Picture-in-picture|
|5|Fusion|
|6|IR1 13mm|
|7|IR2 52mm|

## VIEP_CAM_SWMID: ViewPro Camera For Switch Mid

Camera selection when switch is in middle position

|Value|Meaning|
|:---:|:---:|
|0|No change in camera selection|
|1|EO1|
|2|IR thermal|
|3|EO1 + IR Picture-in-picture|
|4|IR + EO1 Picture-in-picture|
|5|Fusion|
|6|IR1 13mm|
|7|IR2 52mm|

## VIEP_CAM_SWHIGH: ViewPro Camera For Switch High

Camera selection when switch is in high position

|Value|Meaning|
|:---:|:---:|
|0|No change in camera selection|
|1|EO1|
|2|IR thermal|
|3|EO1 + IR Picture-in-picture|
|4|IR + EO1 Picture-in-picture|
|5|Fusion|
|6|IR1 13mm|
|7|IR2 52mm|

## VIEP_ZOOM_SPEED: ViewPro Zoom Speed

ViewPro Zoom Speed.  Higher numbers result in faster zooming

- Range: 0 7

## VIEP_ZOOM_MAX: ViewPro Zoom Times Max

ViewPro Zoom Times Max

- Range: 0 30

## UM_SERVO_MASK: Mask of UltraMotion servos

Mask of UltraMotion servos

- Bitmask: 0:SERVO1,1:SERVO2,2:SERVO3,3:SERVO4,4:SERVO5,5:SERVO6,6:SERVO7,7:SERVO8,8:SERVO9,9:SERVO10,10:SERVO11,11:SERVO12

## UM_CANDRV: Set CAN driver

Set CAN driver

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|1stCANDriver|
|2|2ndCanDriver|

## UM_RATE_HZ: Update rate for UltraMotion servos

Update rate for UltraMotion servos

- Units: Hz

- Range: 1 400

## UM_OPTIONS: Optional settings

Optional settings

- Bitmask: 0:LogAllFrames,1:ParseTelemetry,2:SendPosAsNamedValueFloat

## TOFSENSE_PRX: TOFSENSE-M to be used as Proximity sensor

Set 0 if sensor is to be used as a 1-D rangefinder (minimum of all distances will be sent, typically used for height detection). Set 1 if it should be used as a 3-D proximity device (Eg. Obstacle Avoidance)

|Value|Meaning|
|:---:|:---:|
|0|Set as Rangefinder|
|1|Set as Proximity sensor|

## TOFSENSE_NO: TOFSENSE-M Connected

Number of TOFSENSE-M CAN sensors connected

- Range: 1 3

## TOFSENSE_MODE: TOFSENSE-M mode to be used

TOFSENSE-M mode to be used. 0 for 8x8 mode. 1 for 4x4 mode

|Value|Meaning|
|:---:|:---:|
|0|8x8 mode|
|1|4x4 mode|

## TOFSENSE_INST1: TOFSENSE-M First Instance

First TOFSENSE-M sensors backend Instance. Setting this to 1 will pick the first backend from PRX_ or RNG_ Parameters (Depending on TOFSENSE_PRX)

- Range: 1 3

## TOFSENSE_ID1: TOFSENSE-M First ID

First TOFSENSE-M sensor ID. Leave this at 0 to accept all IDs and if only one sensor is present. You can change ID of sensor from NAssistant Software

- Range: 1 255

## TOFSENSE_INST2: TOFSENSE-M Second Instance

Second TOFSENSE-M sensors backend Instance. Setting this to 2 will pick the second backend from PRX_ or RNG_ Parameters (Depending on TOFSENSE_PRX)

- Range: 1 3

## TOFSENSE_ID2: TOFSENSE-M Second ID

Second TOFSENSE-M sensor ID. This cannot be 0. You can change ID of sensor from NAssistant Software

- Range: 1 255

## TOFSENSE_INST3: TOFSENSE-M Third Instance

Third TOFSENSE-M sensors backend Instance. Setting this to 3 will pick the second backend from PRX_ or RNG_ Parameters (Depending on TOFSENSE_PRX)

- Range: 1 3

## TOFSENSE_ID3: TOFSENSE-M Thir ID

Third TOFSENSE-M sensor ID. This cannot be 0. You can change ID of sensor from NAssistant Software

- Range: 1 255

## TOFSENSE_S1_PRX: TOFSENSE-M to be used as Proximity sensor

Set 0 if sensor is to be used as a 1-D rangefinder (minimum of all distances will be sent, typically used for height detection). Set 1 if it should be used as a 3-D proximity device (Eg. Obstacle Avoidance)

|Value|Meaning|
|:---:|:---:|
|0|Set as Rangefinder|
|1|Set as Proximity sensor|

## TOFSENSE_S1_SP: TOFSENSE-M serial port config

UART instance sensor is connected to. Set 1 if sensor is connected to the port with fist SERIALx_PROTOCOL = 28. 

- Range: 1 4

## TOFSENSE_S1_BR: TOFSENSE-M serial port baudrate

Serial Port baud rate. Sensor baud rate can be changed from Nassistant software

# AFS Parameters

## AFS_ENABLE: Enable Advanced Failsafe

*Note: This parameter is for advanced users*

This enables the advanced failsafe system. If this is set to zero (disable) then all the other AFS options have no effect

## AFS_MAN_PIN: Manual Pin

*Note: This parameter is for advanced users*

This sets a digital output pin to set high when in manual mode.  See the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

## AFS_HB_PIN: Heartbeat Pin

*Note: This parameter is for advanced users*

This sets a digital output pin which is cycled at 10Hz when termination is not activated. Note that if a FS_TERM_PIN is set then the heartbeat pin will continue to cycle at 10Hz when termination is activated, to allow the termination board to distinguish between autopilot crash and termination. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|

## AFS_WP_COMMS: Comms Waypoint

*Note: This parameter is for advanced users*

Waypoint number to navigate to on comms loss

## AFS_WP_GPS_LOSS: GPS Loss Waypoint

*Note: This parameter is for advanced users*

Waypoint number to navigate to on GPS lock loss

## AFS_TERMINATE: Force Terminate

*Note: This parameter is for advanced users*

Can be set in flight to force termination of the heartbeat signal

## AFS_TERM_ACTION: Terminate action

*Note: This parameter is for advanced users*

This can be used to force an action on flight termination. Normally this is handled by an external failsafe board, but you can setup ArduPilot to handle it here. Please consult the wiki for more information on the possible values of the parameter

## AFS_TERM_PIN: Terminate Pin

*Note: This parameter is for advanced users*

This sets a digital output pin to set high on flight termination. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|

## AFS_AMSL_LIMIT: AMSL limit

*Note: This parameter is for advanced users*

This sets the AMSL (above mean sea level) altitude limit. If the pressure altitude determined by QNH exceeds this limit then flight termination will be forced. Note that this limit is in meters, whereas pressure altitude limits are often quoted in feet. A value of zero disables the pressure altitude limit.

- Units: m

## AFS_AMSL_ERR_GPS: Error margin for GPS based AMSL limit

*Note: This parameter is for advanced users*

This sets margin for error in GPS derived altitude limit. This error margin is only used if the barometer has failed. If the barometer fails then the GPS will be used to enforce the AMSL_LIMIT, but this margin will be subtracted from the AMSL_LIMIT first, to ensure that even with the given amount of GPS altitude error the pressure altitude is not breached. OBC users should set this to comply with their D2 safety case. A value of -1 will mean that barometer failure will lead to immediate termination.

- Units: m

## AFS_QNH_PRESSURE: QNH pressure

*Note: This parameter is for advanced users*

This sets the QNH pressure in millibars to be used for pressure altitude in the altitude limit. A value of zero disables the altitude limit.

- Units: hPa

## AFS_MAX_GPS_LOSS: Maximum number of GPS loss events

*Note: This parameter is for advanced users*

Maximum number of GPS loss events before the aircraft stops returning to mission on GPS recovery. Use zero to allow for any number of GPS loss events.

## AFS_MAX_COM_LOSS: Maximum number of comms loss events

*Note: This parameter is for advanced users*

Maximum number of comms loss events before the aircraft stops returning to mission on comms recovery. Use zero to allow for any number of comms loss events.

## AFS_GEOFENCE: Enable geofence Advanced Failsafe

*Note: This parameter is for advanced users*

This enables the geofence part of the AFS. Will only be in effect if AFS_ENABLE is also 1

## AFS_RC: Enable RC Advanced Failsafe

*Note: This parameter is for advanced users*

This enables the RC part of the AFS. Will only be in effect if AFS_ENABLE is also 1

## AFS_RC_MAN_ONLY: Enable RC Termination only in manual control modes

*Note: This parameter is for advanced users*

If this parameter is set to 1, then an RC loss will only cause the plane to terminate in manual control modes. If it is 0, then the plane will terminate in any flight mode.

## AFS_DUAL_LOSS: Enable dual loss terminate due to failure of both GCS and GPS simultaneously

*Note: This parameter is for advanced users*

This enables the dual loss termination part of the AFS system. If this parameter is 1 and both GPS and the ground control station fail simultaneously, this will be considered a "dual loss" and cause termination.

## AFS_RC_FAIL_TIME: RC failure time

*Note: This parameter is for advanced users*

This is the time in seconds in manual mode that failsafe termination will activate if RC input is lost. For the OBC rules this should be (1.5). Use 0 to disable.

- Units: s

## AFS_MAX_RANGE: Max allowed range

*Note: This parameter is for advanced users*

This is the maximum range of the vehicle in kilometers from first arming. If the vehicle goes beyond this range then the TERM_ACTION is performed. A value of zero disables this feature.

- Units: km

## AFS_OPTIONS: AFS options

See description for each bitmask bit description

- Bitmask: 0: Continue the mission even after comms are recovered (does not go to the mission item at the time comms were lost), 1: Enable AFS for all autonomous modes (not just AUTO) 

## AFS_GCS_TIMEOUT: GCS timeout

*Note: This parameter is for advanced users*

The time (in seconds) of persistent data link loss before GCS failsafe occurs. 

- Units: s

# AHRS Parameters

## AHRS_GPS_GAIN: AHRS GPS gain

*Note: This parameter is for advanced users*

This controls how much to use the GPS to correct the attitude. This should never be set to zero for a plane as it would result in the plane losing control in turns. For a plane please use the default value of 1.0.

- Range: 0.0 1.0

- Increment: .01

## AHRS_GPS_USE: AHRS use GPS for DCM navigation and position-down

*Note: This parameter is for advanced users*

This controls whether to use dead-reckoning or GPS based navigation. If set to 0 then the GPS won't be used for navigation, and only dead reckoning will be used. A value of zero should never be used for normal flight. Currently this affects only the DCM-based AHRS: the EKF uses GPS according to its own parameters. A value of 2 means to use GPS for height as well as position - both in DCM estimation and when determining altitude-above-home.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Use GPS for DCM position|
|2|Use GPS for DCM position and height|

## AHRS_YAW_P: Yaw P

*Note: This parameter is for advanced users*

This controls the weight the compass or GPS has on the heading. A higher value means the heading will track the yaw source (GPS or compass) more rapidly.

- Range: 0.1 0.4

- Increment: .01

## AHRS_RP_P: AHRS RP_P

*Note: This parameter is for advanced users*

This controls how fast the accelerometers correct the attitude

- Range: 0.1 0.4

- Increment: .01

## AHRS_WIND_MAX: Maximum wind

*Note: This parameter is for advanced users*

This sets the maximum allowable difference between ground speed and airspeed. A value of zero means to use the airspeed as is. This allows the plane to cope with a failing airspeed sensor by clipping it to groundspeed plus/minus this limit. See ARSPD_OPTIONS and ARSPD_WIND_MAX to disable airspeed sensors.

- Range: 0 127

- Units: m/s

- Increment: 1

## AHRS_TRIM_X: AHRS Trim Roll

Compensates for the roll angle difference between the control board and the frame. Positive values make the vehicle roll right.

- Units: rad

- Range: -0.1745 +0.1745

- Increment: 0.01

## AHRS_TRIM_Y: AHRS Trim Pitch

Compensates for the pitch angle difference between the control board and the frame. Positive values make the vehicle pitch up/back.

- Units: rad

- Range: -0.1745 +0.1745

- Increment: 0.01

## AHRS_TRIM_Z: AHRS Trim Yaw

*Note: This parameter is for advanced users*

Not Used

- Units: rad

- Range: -0.1745 +0.1745

- Increment: 0.01

## AHRS_ORIENTATION: Board Orientation

*Note: This parameter is for advanced users*

Overall board orientation relative to the standard orientation for the board type. This rotates the IMU and compass readings to allow the board to be oriented in your vehicle at any 90 or 45 degree angle. The label for each option is specified in the order of rotations for that orientation. This option takes affect on next boot. After changing you will need to re-level your vehicle. Firmware versions 4.2 and prior can use a CUSTOM (100) rotation to set the AHRS_CUSTOM_ROLL/PIT/YAW angles for AHRS orientation. Later versions provide two general custom rotations which can be used, Custom 1 and Custom 2, with CUST_ROT1_ROLL/PIT/YAW or CUST_ROT2_ROLL/PIT/YAW angles.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Yaw45|
|2|Yaw90|
|3|Yaw135|
|4|Yaw180|
|5|Yaw225|
|6|Yaw270|
|7|Yaw315|
|8|Roll180|
|9|Yaw45Roll180|
|10|Yaw90Roll180|
|11|Yaw135Roll180|
|12|Pitch180|
|13|Yaw225Roll180|
|14|Yaw270Roll180|
|15|Yaw315Roll180|
|16|Roll90|
|17|Yaw45Roll90|
|18|Yaw90Roll90|
|19|Yaw135Roll90|
|20|Roll270|
|21|Yaw45Roll270|
|22|Yaw90Roll270|
|23|Yaw135Roll270|
|24|Pitch90|
|25|Pitch270|
|26|Yaw90Pitch180|
|27|Yaw270Pitch180|
|28|Pitch90Roll90|
|29|Pitch90Roll180|
|30|Pitch90Roll270|
|31|Pitch180Roll90|
|32|Pitch180Roll270|
|33|Pitch270Roll90|
|34|Pitch270Roll180|
|35|Pitch270Roll270|
|36|Yaw90Pitch180Roll90|
|37|Yaw270Roll90|
|38|Yaw293Pitch68Roll180|
|39|Pitch315|
|40|Pitch315Roll90|
|42|Roll45|
|43|Roll315|
|100|Custom 4.1 and older|
|101|Custom 1|
|102|Custom 2|

## AHRS_COMP_BETA: AHRS Velocity Complementary Filter Beta Coefficient

*Note: This parameter is for advanced users*

This controls the time constant for the cross-over frequency used to fuse AHRS (airspeed and heading) and GPS data to estimate ground velocity. Time constant is 0.1/beta. A larger time constant will use GPS data less and a small time constant will use air data less.

- Range: 0.001 0.5

- Increment: .01

## AHRS_GPS_MINSATS: AHRS GPS Minimum satellites

*Note: This parameter is for advanced users*

Minimum number of satellites visible to use GPS for velocity based corrections attitude correction. This defaults to 6, which is about the point at which the velocity numbers from a GPS become too unreliable for accurate correction of the accelerometers.

- Range: 0 10

- Increment: 1

## AHRS_EKF_TYPE: Use NavEKF Kalman filter for attitude and position estimation

*Note: This parameter is for advanced users*

This controls which NavEKF Kalman filter version is used for attitude and position estimation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|2|Enable EKF2|
|3|Enable EKF3|
|11|ExternalAHRS|

## AHRS_CUSTOM_ROLL: Board orientation roll offset

*Note: This parameter is for advanced users*

Autopilot mounting position roll offset. Positive values = roll right, negative values = roll left. This parameter is only used when AHRS_ORIENTATION is set to CUSTOM.

- Range: -180 180

- Units: deg

- Increment: 1

## AHRS_CUSTOM_PIT: Board orientation pitch offset

*Note: This parameter is for advanced users*

Autopilot mounting position pitch offset. Positive values = pitch up, negative values = pitch down. This parameter is only used when AHRS_ORIENTATION is set to CUSTOM.

- Range: -180 180

- Units: deg

- Increment: 1

## AHRS_CUSTOM_YAW: Board orientation yaw offset

*Note: This parameter is for advanced users*

Autopilot mounting position yaw offset. Positive values = yaw right, negative values = yaw left. This parameter is only used when AHRS_ORIENTATION is set to CUSTOM.

- Range: -180 180

- Units: deg

- Increment: 1

## AHRS_OPTIONS: Optional AHRS behaviour

*Note: This parameter is for advanced users*

This controls optional AHRS behaviour. Setting DisableDCMFallbackFW will change the AHRS behaviour for fixed wing aircraft in fly-forward flight to not fall back to DCM when the EKF stops navigating. Setting DisableDCMFallbackVTOL will change the AHRS behaviour for fixed wing aircraft in non fly-forward (VTOL) flight to not fall back to DCM when the EKF stops navigating. Setting DontDisableAirspeedUsingEKF disables the EKF based innovation check for airspeed consistency

- Bitmask: 0:DisableDCMFallbackFW, 1:DisableDCMFallbackVTOL, 2:DontDisableAirspeedUsingEKF

# AIS Parameters

## AIS_TYPE: AIS receiver type

AIS receiver type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|NMEA AIVDM message|

- RebootRequired: True

## AIS_LIST_MAX: AIS vessel list size

*Note: This parameter is for advanced users*

AIS list size of nearest vessels. Longer lists take longer to refresh with lower SRx_ADSB values.

- Range: 1 100

## AIS_TIME_OUT: AIS vessel time out

*Note: This parameter is for advanced users*

if no updates are received in this time a vessel will be removed from the list

- Units: s

- Range: 1 2000

## AIS_LOGGING: AIS logging options

*Note: This parameter is for advanced users*

Bitmask of AIS logging options

- Bitmask: 0:Log all AIVDM messages,1:Log only unsupported AIVDM messages,2:Log decoded messages

# ARMING Parameters

## ARMING_REQUIRE: Require Arming Motors 

*Note: This parameter is for advanced users*

Arming disabled until some requirements are met. If 0, there are no requirements (arm immediately).  If 1, sends the minimum throttle PWM value to the throttle channel when disarmed. If 2, send 0 PWM (no signal) to throttle channel when disarmed. On planes with ICE enabled and the throttle while disarmed option set in ICE_OPTIONS, the motor will always get THR_MIN when disarmed. Arming will occur using either rudder stick arming (if enabled) or GCS command when all mandatory and ARMING_CHECK items are satisfied. Note, when setting this parameter to 0, a reboot is required to immediately arm the plane.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|minimum PWM when disarmed|
|2|0 PWM when disarmed|

## ARMING_ACCTHRESH: Accelerometer error threshold

*Note: This parameter is for advanced users*

Accelerometer error threshold used to determine inconsistent accelerometers. Compares this error range to other accelerometers to detect a hardware or calibration error. Lower value means tighter check and harder to pass arming check. Not all accelerometers are created equal.

- Units: m/s/s

- Range: 0.25 3.0

## ARMING_RUDDER: Arming with Rudder enable/disable

*Note: This parameter is for advanced users*

Allow arm/disarm by rudder input. When enabled arming can be done with right rudder, disarming with left rudder. Rudder arming only works with throttle at zero +- deadzone (RCx_DZ). Depending on vehicle type, arming in certain modes is prevented. See the wiki for each vehicle. Caution is recommended when arming if it is allowed in an auto-throttle mode!

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|ArmingOnly|
|2|ArmOrDisarm|

## ARMING_MIS_ITEMS: Required mission items

*Note: This parameter is for advanced users*

Bitmask of mission items that are required to be planned in order to arm the aircraft

- Bitmask: 0:Land,1:VTOL Land,2:DO_LAND_START,3:Takeoff,4:VTOL Takeoff,5:Rallypoint,6:RTL

## ARMING_CHECK: Arm Checks to Perform (bitmask)

Checks prior to arming motor. This is a bitmask of checks that will be performed before allowing arming. For most users it is recommended to leave this at the default of 1 (all checks enabled). You can select whatever checks you prefer by adding together the values of each check type to set this parameter. For example, to only allow arming when you have GPS lock and no RC failsafe you would set ARMING_CHECK to 72.

- Bitmask: 0:All,1:Barometer,2:Compass,3:GPS lock,4:INS,5:Parameters,6:RC Channels,7:Board voltage,8:Battery Level,10:Logging Available,11:Hardware safety switch,12:GPS Configuration,13:System,14:Mission,15:Rangefinder,16:Camera,17:AuxAuth,18:VisualOdometry,19:FFT

## ARMING_OPTIONS: Arming options

*Note: This parameter is for advanced users*

Options that can be applied to change arming behaviour

- Bitmask: 0:Disable prearm display,1:Do not send status text on state change

## ARMING_MAGTHRESH: Compass magnetic field strength error threshold vs earth magnetic model

*Note: This parameter is for advanced users*

Compass magnetic field strength error threshold vs earth magnetic model.  X and y axis are compared using this threhold, Z axis uses 2x this threshold.  0 to disable check

- Units: mGauss

- Range: 0 500

## ARMING_CRSDP_IGN: Disable CrashDump Arming check

*Note: This parameter is for advanced users*

Must have value "1" if crashdump data is present on the system, or a prearm failure will be raised.  Do not set this parameter unless the risks of doing so are fully understood.  The presence of a crash dump means that the firmware currently installed has suffered a critical software failure which resulted in the autopilot immediately rebooting.  The crashdump file gives diagnostic information which can help in finding the issue, please contact the ArduPIlot support team.  If this crashdump data is present, the vehicle is likely unsafe to fly.  Check the ArduPilot documentation for more details.

|Value|Meaning|
|:---:|:---:|
|0|Crash Dump arming check active|
|1|Crash Dump arming check deactivated|

# ARSPD Parameters

## ARSPD_ENABLE: Airspeed Enable

Enable airspeed sensor support

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## ARSPD_TUBE_ORDER: Control pitot tube order

*Note: This parameter is for advanced users*

This parameter allows you to control whether the order in which the tubes are attached to your pitot tube matters. If you set this to 0 then the first (often the top) connector on the sensor needs to be the stagnation pressure (the pressure at the tip of the pitot tube). If set to 1 then the second (often the bottom) connector needs to be the stagnation pressure. If set to 2 (the default) then the airspeed driver will accept either order. The reason you may wish to specify the order is it will allow your airspeed sensor to detect if the aircraft is receiving excessive pressure on the static port compared to the stagnation port such as during a stall, which would otherwise be seen as a positive airspeed.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Swapped|
|2|Auto Detect|

## ARSPD_PRIMARY: Primary airspeed sensor

*Note: This parameter is for advanced users*

This selects which airspeed sensor will be the primary if multiple sensors are found

|Value|Meaning|
|:---:|:---:|
|0|FirstSensor|
|1|2ndSensor|

## ARSPD_OPTIONS: Airspeed options bitmask

*Note: This parameter is for advanced users*

This parameter and function is not used by this vehicle. Always set to 0.

- Bitmask: 0:SpeedMismatchDisable, 1:AllowSpeedMismatchRecovery, 2:DisableVoltageCorrection, 3:UseEkf3Consistency, 4:ReportOffset

## ARSPD_WIND_MAX: Maximum airspeed and ground speed difference

*Note: This parameter is for advanced users*

This parameter and function is not used by this vehicle. Always set to 0.

- Units: m/s

## ARSPD_WIND_WARN: Airspeed and GPS speed difference that gives a warning

*Note: This parameter is for advanced users*

This parameter and function is not used by this vehicle. Always set to 0.

- Units: m/s

## ARSPD_WIND_GATE: Re-enable Consistency Check Gate Size

*Note: This parameter is for advanced users*

This parameter and function is not used by this vehicle.

- Range: 0.0 10.0

## ARSPD_OFF_PCNT: Maximum offset cal speed error 

*Note: This parameter is for advanced users*

The maximum percentage speed change in airspeed reports that is allowed due to offset changes between calibrations before a warning is issued. This potential speed error is in percent of ASPD_FBW_MIN. 0 disables. Helps warn of calibrations without pitot being covered.

- Range: 0.0 10.0

- Units: %

# ARSPD2 Parameters

## ARSPD2_TYPE: Airspeed type

Type of airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|I2C-MS4525D0|
|2|Analog|
|3|I2C-MS5525|
|4|I2C-MS5525 (0x76)|
|5|I2C-MS5525 (0x77)|
|6|I2C-SDP3X|
|7|I2C-DLVR-5in|
|8|DroneCAN|
|9|I2C-DLVR-10in|
|10|I2C-DLVR-20in|
|11|I2C-DLVR-30in|
|12|I2C-DLVR-60in|
|13|NMEA water speed|
|14|MSP|
|15|ASP5033|
|16|ExternalAHRS|
|100|SITL|

## ARSPD2_USE: Airspeed use

This parameter is not used by this vehicle. Always set to 0.

|Value|Meaning|
|:---:|:---:|
|0|DoNotUse|
|1|Use|
|2|UseWhenZeroThrottle|

## ARSPD2_OFFSET: Airspeed offset

*Note: This parameter is for advanced users*

Airspeed calibration offset

- Increment: 0.1

## ARSPD2_RATIO: Airspeed ratio

*Note: This parameter is for advanced users*

Calibrates pitot tube pressure to velocity. Increasing this value will indicate a higher airspeed at any given dynamic pressure.

- Increment: 0.1

## ARSPD2_PIN: Airspeed pin

*Note: This parameter is for advanced users*

The pin number that the airspeed sensor is connected to for analog sensors. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## ARSPD2_AUTOCAL: This parameter and function is not used by this vehicle. Always set to 0.

*Note: This parameter is for advanced users*

Enables automatic adjustment of airspeed ratio during a calibration flight based on estimation of ground speed and true airspeed. New ratio saved every 2 minutes if change is > 5%. Should not be left enabled.

## ARSPD2_TUBE_ORDR: Control pitot tube order

*Note: This parameter is for advanced users*

This parameter allows you to control whether the order in which the tubes are attached to your pitot tube matters. If you set this to 0 then the first (often the top) connector on the sensor needs to be the stagnation pressure (the pressure at the tip of the pitot tube). If set to 1 then the second (often the bottom) connector needs to be the stagnation pressure. If set to 2 (the default) then the airspeed driver will accept either order. The reason you may wish to specify the order is it will allow your airspeed sensor to detect if the aircraft is receiving excessive pressure on the static port compared to the stagnation port such as during a stall, which would otherwise be seen as a positive airspeed.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Swapped|
|2|Auto Detect|

## ARSPD2_SKIP_CAL: Skip airspeed offset calibration on startup

*Note: This parameter is for advanced users*

This parameter allows you to skip airspeed offset calibration on startup, instead using the offset from the last calibration. This may be desirable if the offset variance between flights for your sensor is low and you want to avoid having to cover the pitot tube on each boot.

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## ARSPD2_PSI_RANGE: The PSI range of the device

*Note: This parameter is for advanced users*

This parameter allows you to set the PSI (pounds per square inch) range for your sensor. You should not change this unless you examine the datasheet for your device

## ARSPD2_BUS: Airspeed I2C bus

*Note: This parameter is for advanced users*

Bus number of the I2C bus where the airspeed sensor is connected. May not correspond to board's I2C bus number labels. Retry another bus and reboot if airspeed sensor fails to initialize.

|Value|Meaning|
|:---:|:---:|
|0|Bus0|
|1|Bus1|
|2|Bus2|

- RebootRequired: True

## ARSPD2_DEVID: Airspeed ID

*Note: This parameter is for advanced users*

Airspeed sensor ID, taking into account its type, bus and instance

- ReadOnly: True

# ARSPD Parameters

## ARSPD_TYPE: Airspeed type

Type of airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|I2C-MS4525D0|
|2|Analog|
|3|I2C-MS5525|
|4|I2C-MS5525 (0x76)|
|5|I2C-MS5525 (0x77)|
|6|I2C-SDP3X|
|7|I2C-DLVR-5in|
|8|DroneCAN|
|9|I2C-DLVR-10in|
|10|I2C-DLVR-20in|
|11|I2C-DLVR-30in|
|12|I2C-DLVR-60in|
|13|NMEA water speed|
|14|MSP|
|15|ASP5033|
|16|ExternalAHRS|
|100|SITL|

## ARSPD_USE: Airspeed use

This parameter is not used by this vehicle. Always set to 0.

|Value|Meaning|
|:---:|:---:|
|0|DoNotUse|
|1|Use|
|2|UseWhenZeroThrottle|

## ARSPD_OFFSET: Airspeed offset

*Note: This parameter is for advanced users*

Airspeed calibration offset

- Increment: 0.1

## ARSPD_RATIO: Airspeed ratio

*Note: This parameter is for advanced users*

Calibrates pitot tube pressure to velocity. Increasing this value will indicate a higher airspeed at any given dynamic pressure.

- Increment: 0.1

## ARSPD_PIN: Airspeed pin

*Note: This parameter is for advanced users*

The pin number that the airspeed sensor is connected to for analog sensors. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## ARSPD_AUTOCAL: This parameter and function is not used by this vehicle. Always set to 0.

*Note: This parameter is for advanced users*

Enables automatic adjustment of airspeed ratio during a calibration flight based on estimation of ground speed and true airspeed. New ratio saved every 2 minutes if change is > 5%. Should not be left enabled.

## ARSPD_TUBE_ORDR: Control pitot tube order

*Note: This parameter is for advanced users*

This parameter allows you to control whether the order in which the tubes are attached to your pitot tube matters. If you set this to 0 then the first (often the top) connector on the sensor needs to be the stagnation pressure (the pressure at the tip of the pitot tube). If set to 1 then the second (often the bottom) connector needs to be the stagnation pressure. If set to 2 (the default) then the airspeed driver will accept either order. The reason you may wish to specify the order is it will allow your airspeed sensor to detect if the aircraft is receiving excessive pressure on the static port compared to the stagnation port such as during a stall, which would otherwise be seen as a positive airspeed.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Swapped|
|2|Auto Detect|

## ARSPD_SKIP_CAL: Skip airspeed offset calibration on startup

*Note: This parameter is for advanced users*

This parameter allows you to skip airspeed offset calibration on startup, instead using the offset from the last calibration. This may be desirable if the offset variance between flights for your sensor is low and you want to avoid having to cover the pitot tube on each boot.

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## ARSPD_PSI_RANGE: The PSI range of the device

*Note: This parameter is for advanced users*

This parameter allows you to set the PSI (pounds per square inch) range for your sensor. You should not change this unless you examine the datasheet for your device

## ARSPD_BUS: Airspeed I2C bus

*Note: This parameter is for advanced users*

Bus number of the I2C bus where the airspeed sensor is connected. May not correspond to board's I2C bus number labels. Retry another bus and reboot if airspeed sensor fails to initialize.

|Value|Meaning|
|:---:|:---:|
|0|Bus0|
|1|Bus1|
|2|Bus2|

- RebootRequired: True

## ARSPD_DEVID: Airspeed ID

*Note: This parameter is for advanced users*

Airspeed sensor ID, taking into account its type, bus and instance

- ReadOnly: True

# ATC Parameters

## ATC_STR_RAT_P: Steering control rate P gain

Steering control rate P gain.  Converts the turn rate error (in radians/sec) to a steering control output (in the range -1 to +1)

- Range: 0.000 2.000

- Increment: 0.001

## ATC_STR_RAT_I: Steering control I gain

Steering control I gain.  Corrects long term error between the desired turn rate (in rad/s) and actual

- Range: 0.000 2.000

- Increment: 0.001

## ATC_STR_RAT_IMAX: Steering control I gain maximum

Steering control I gain maximum.  Constrains the steering output (range -1 to +1) that the I term will generate

- Range: 0.000 1.000

- Increment: 0.01

## ATC_STR_RAT_D: Steering control D gain

Steering control D gain.  Compensates for short-term change in desired turn rate vs actual

- Range: 0.000 0.400

- Increment: 0.001

## ATC_STR_RAT_FF: Steering control feed forward

Steering control feed forward

- Range: 0.000 3.000

- Increment: 0.001

## ATC_STR_RAT_FILT: Steering control filter frequency

Steering control input filter.  Lower values reduce noise but add delay.

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_STR_RAT_FLTT: Steering control Target filter frequency in Hz

Target filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_STR_RAT_FLTE: Steering control Error filter frequency in Hz

Error filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_STR_RAT_FLTD: Steering control Derivative term filter frequency in Hz

Derivative filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_STR_RAT_SMAX: Steering slew rate limit

*Note: This parameter is for advanced users*

Sets an upper limit on the slew rate produced by the combined P and D gains. If the amplitude of the control action produced by the rate feedback exceeds this value, then the D+P gain is reduced to respect the limit. This limits the amplitude of high frequency oscillations caused by an excessive gain. The limit should be set to no more than 25% of the actuators maximum slew rate to allow for load effects. Note: The gain will not be reduced to less than 10% of the nominal value. A value of zero will disable this feature.

- Range: 0 200

- Increment: 0.5

## ATC_STR_RAT_PDMX: Steering control PD sum maximum

Steering control PD sum maximum.  The maximum/minimum value that the sum of the P and D term can output

- Range: 0.000 1.000

- Increment: 0.01

## ATC_STR_RAT_D_FF: Steering control Derivative FeedForward Gain

*Note: This parameter is for advanced users*

FF D Gain which produces an output that is proportional to the rate of change of the target

- Range: 0 0.03

- Increment: 0.001

## ATC_STR_RAT_NTF: Steering control Target notch filter index

*Note: This parameter is for advanced users*

Steering control Target notch filter index

- Range: 1 8

## ATC_STR_RAT_NEF: Steering control Error notch filter index

*Note: This parameter is for advanced users*

Steering control Error notch filter index

- Range: 1 8

## ATC_SPEED_P: Speed control P gain

Speed control P gain.  Converts the error between the desired speed (in m/s) and actual speed to a motor output (in the range -1 to +1)

- Range: 0.010 2.000

- Increment: 0.01

## ATC_SPEED_I: Speed control I gain

Speed control I gain.  Corrects long term error between the desired speed (in m/s) and actual speed

- Range: 0.000 2.000

- Increment: 0.01

## ATC_SPEED_IMAX: Speed control I gain maximum

Speed control I gain maximum.  Constrains the maximum motor output (range -1 to +1) that the I term will generate

- Range: 0.000 1.000

- Increment: 0.01

## ATC_SPEED_D: Speed control D gain

Speed control D gain.  Compensates for short-term change in desired speed vs actual

- Range: 0.000 0.400

- Increment: 0.001

## ATC_SPEED_FF: Speed control feed forward

Speed control feed forward

- Range: 0.000 0.500

- Increment: 0.001

## ATC_SPEED_FILT: Speed control filter frequency

Speed control input filter.  Lower values reduce noise but add delay.

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SPEED_FLTT: Speed control Target filter frequency in Hz

Target filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SPEED_FLTE: Speed control Error filter frequency in Hz

Error filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SPEED_FLTD: Speed control Derivative term filter frequency in Hz

Derivative filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SPEED_SMAX: Speed control slew rate limit

*Note: This parameter is for advanced users*

Sets an upper limit on the slew rate produced by the combined P and D gains. If the amplitude of the control action produced by the rate feedback exceeds this value, then the D+P gain is reduced to respect the limit. This limits the amplitude of high frequency oscillations caused by an excessive gain. The limit should be set to no more than 25% of the actuators maximum slew rate to allow for load effects. Note: The gain will not be reduced to less than 10% of the nominal value. A value of zero will disable this feature.

- Range: 0 200

- Increment: 0.5

## ATC_SPEED_PDMX: Speed control PD sum maximum

Speed control PD sum maximum.  The maximum/minimum value that the sum of the P and D term can output

- Range: 0.000 1.000

- Increment: 0.01

## ATC_SPEED_D_FF: Speed control Derivative FeedForward Gain

*Note: This parameter is for advanced users*

FF D Gain which produces an output that is proportional to the rate of change of the target

- Range: 0 0.03

- Increment: 0.001

## ATC_SPEED_NTF: Speed control Target notch filter index

*Note: This parameter is for advanced users*

Speed control Target notch filter index

- Range: 1 8

## ATC_SPEED_NEF: Speed control Error notch filter index

*Note: This parameter is for advanced users*

Speed control Error notch filter index

- Range: 1 8

## ATC_ACCEL_MAX: Speed control acceleration (and deceleration) maximum in m/s/s

Speed control acceleration (and deceleration) maximum in m/s/s.  0 to disable acceleration limiting

- Range: 0.0 10.0

- Increment: 0.1

- Units: m/s/s

## ATC_BRAKE: Speed control brake enable/disable

Speed control brake enable/disable. Allows sending a reversed output to the motors to slow the vehicle.

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## ATC_STOP_SPEED: Speed control stop speed

Speed control stop speed.  Motor outputs to zero once vehicle speed falls below this value

- Range: 0.00 0.50

- Increment: 0.01

- Units: m/s

## ATC_STR_ANG_P: Steering control angle P gain

Steering control angle P gain.  Converts the error between the desired heading/yaw (in radians) and actual heading/yaw to a desired turn rate (in rad/sec)

- Range: 1.000 10.000

- Increment: 0.1

## ATC_STR_ACC_MAX: Steering control angular acceleration maximum

Steering control angular acceleration maximum (in deg/s/s).  0 to disable acceleration limiting

- Range: 0 1000

- Increment: 0.1

- Units: deg/s/s

## ATC_STR_RAT_MAX: Steering control rotation rate maximum

Steering control rotation rate maximum in deg/s.  0 to remove rate limiting

- Range: 0 1000

- Increment: 0.1

- Units: deg/s

## ATC_DECEL_MAX: Speed control deceleration maximum in m/s/s

Speed control and deceleration maximum in m/s/s.  0 to use ATC_ACCEL_MAX for deceleration

- Range: 0.0 10.0

- Increment: 0.1

- Units: m/s/s

## ATC_BAL_P: Pitch control P gain

Pitch control P gain for BalanceBots.  Converts the error between the desired pitch (in radians) and actual pitch to a motor output (in the range -1 to +1)

- Range: 0.000 2.000

- Increment: 0.01

## ATC_BAL_I: Pitch control I gain

Pitch control I gain for BalanceBots.  Corrects long term error between the desired pitch (in radians) and actual pitch

- Range: 0.000 2.000

- Increment: 0.01

## ATC_BAL_IMAX: Pitch control I gain maximum

Pitch control I gain maximum.  Constrains the maximum motor output (range -1 to +1) that the I term will generate

- Range: 0.000 1.000

- Increment: 0.01

## ATC_BAL_D: Pitch control D gain

Pitch control D gain.  Compensates for short-term change in desired pitch vs actual

- Range: 0.000 0.100

- Increment: 0.001

## ATC_BAL_FF: Pitch control feed forward

Pitch control feed forward

- Range: 0.000 0.500

- Increment: 0.001

## ATC_BAL_FILT: Pitch control filter frequency

Pitch control input filter.  Lower values reduce noise but add delay.

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_BAL_FLTT: Pitch control Target filter frequency in Hz

Pitch control Target filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_BAL_FLTE: Pitch control Error filter frequency in Hz

Pitch control Error filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_BAL_FLTD: Pitch control Derivative term filter frequency in Hz

Pitch control Derivative filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_BAL_SMAX: Pitch control slew rate limit

*Note: This parameter is for advanced users*

Pitch control upper limit on the slew rate produced by the combined P and D gains. If the amplitude of the control action produced by the rate feedback exceeds this value, then the D+P gain is reduced to respect the limit. This limits the amplitude of high frequency oscillations caused by an excessive gain. The limit should be set to no more than 25% of the actuators maximum slew rate to allow for load effects. Note: The gain will not be reduced to less than 10% of the nominal value. A value of zero will disable this feature.

- Range: 0 200

- Increment: 0.5

## ATC_BAL_PDMX: Pitch control PD sum maximum

Pitch control PD sum maximum.  The maximum/minimum value that the sum of the P and D term can output

- Range: 0.000 1.000

- Increment: 0.01

## ATC_BAL_D_FF: Pitch control Derivative FeedForward Gain

*Note: This parameter is for advanced users*

FF D Gain which produces an output that is proportional to the rate of change of the target

- Range: 0 0.03

- Increment: 0.001

## ATC_BAL_NTF: Pitch control Target notch filter index

*Note: This parameter is for advanced users*

Pitch control Target notch filter index

- Range: 1 8

## ATC_BAL_NEF: Pitch control Error notch filter index

*Note: This parameter is for advanced users*

Pitch control Error notch filter index

- Range: 1 8

## ATC_BAL_PIT_FF: Pitch control feed forward from current pitch angle

Pitch control feed forward from current pitch angle

- Range: 0.0 1.0

- Increment: 0.01

## ATC_SAIL_P: Sail Heel control P gain

Sail Heel control P gain for sailboats.  Converts the error between the desired heel angle (in radians) and actual heel to a main sail output (in the range -1 to +1)

- Range: 0.000 2.000

- Increment: 0.01

## ATC_SAIL_I: Sail Heel control I gain

Sail Heel control I gain for sailboats.  Corrects long term error between the desired heel angle (in radians) and actual

- Range: 0.000 2.000

- Increment: 0.01

## ATC_SAIL_IMAX: Sail Heel control I gain maximum

Sail Heel control I gain maximum.  Constrains the maximum I term contribution to the main sail output (range -1 to +1)

- Range: 0.000 1.000

- Increment: 0.01

## ATC_SAIL_D: Sail Heel control D gain

Sail Heel control D gain.  Compensates for short-term change in desired heel angle vs actual

- Range: 0.000 0.100

- Increment: 0.001

## ATC_SAIL_FF: Sail Heel control feed forward

Sail Heel control feed forward

- Range: 0.000 0.500

- Increment: 0.001

## ATC_SAIL_FILT: Sail Heel control filter frequency

Sail Heel control input filter.  Lower values reduce noise but add delay.

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SAIL_FLTT: Sail Heel Target filter frequency in Hz

Target filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SAIL_FLTE: Sail Heel Error filter frequency in Hz

Error filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SAIL_FLTD: Sail Heel Derivative term filter frequency in Hz

Derivative filter frequency in Hz

- Range: 0.000 100.000

- Increment: 0.1

- Units: Hz

## ATC_SAIL_SMAX: Sail heel slew rate limit

*Note: This parameter is for advanced users*

Sets an upper limit on the slew rate produced by the combined P and D gains. If the amplitude of the control action produced by the rate feedback exceeds this value, then the D+P gain is reduced to respect the limit. This limits the amplitude of high frequency oscillations caused by an excessive gain. The limit should be set to no more than 25% of the actuators maximum slew rate to allow for load effects. Note: The gain will not be reduced to less than 10% of the nominal value. A value of zero will disable this feature.

- Range: 0 200

- Increment: 0.5

## ATC_SAIL_PDMX: Sail Heel control PD sum maximum

Sail Heel control PD sum maximum.  The maximum/minimum value that the sum of the P and D term can output

- Range: 0.000 1.000

- Increment: 0.01

## ATC_SAIL_D_FF: Sail Heel Derivative FeedForward Gain

*Note: This parameter is for advanced users*

FF D Gain which produces an output that is proportional to the rate of change of the target

- Range: 0 0.03

- Increment: 0.001

## ATC_SAIL_NTF: Sail Heel Target notch filter index

*Note: This parameter is for advanced users*

Sail Heel Target notch filter index

- Range: 1 8

## ATC_SAIL_NEF: Sail Heel Error notch filter index

*Note: This parameter is for advanced users*

Sail Heel Error notch filter index

- Range: 1 8

## ATC_TURN_MAX_G: Turning maximum G force

The maximum turning acceleration (in units of gravities) that the rover can handle while remaining stable. The navigation code will keep the lateral acceleration below this level to avoid rolling over or slipping the wheels in turns

- Units: gravities

- Range: 0.1 10

- Increment: 0.01

## ATC_BAL_LIM_TC: Pitch control limit time constant

Pitch control limit time constant to protect against falling.  Lower values limit pitch more quickly, higher values limit more slowly.  Set to 0 to disable

- Range: 0.0 5.0

- Increment: 0.01

## ATC_BAL_LIM_THR: Pitch control limit throttle threshold

Pitch control limit throttle threshold.  Pitch angle will be limited if throttle crosses this threshold (from 0 to 1)

- Range: 0.0 1.0

- Increment: 0.01

# AVOID Parameters

## AVOID_ENABLE: Avoidance control enable/disable

Enabled/disable avoidance input sources

- Bitmask: 0:UseFence,1:UseProximitySensor,2:UseBeaconFence

## AVOID_MARGIN: Avoidance distance margin in GPS modes

Vehicle will attempt to stay at least this distance (in meters) from objects while in GPS modes

- Units: m

- Range: 1 10

## AVOID_BEHAVE: Avoidance behaviour

Avoidance behaviour (slide or stop)

|Value|Meaning|
|:---:|:---:|
|0|Slide|
|1|Stop|

## AVOID_BACKUP_SPD: Avoidance maximum horizontal backup speed

Maximum speed that will be used to back away from obstacles horizontally in position control modes (m/s). Set zero to disable horizontal backup.

- Units: m/s

- Range: 0 2

## AVOID_ACCEL_MAX: Avoidance maximum acceleration

Maximum acceleration with which obstacles will be avoided with. Set zero to disable acceleration limits

- Units: m/s/s

- Range: 0 9

## AVOID_BACKUP_DZ: Avoidance deadzone between stopping and backing away from obstacle

Distance beyond AVOID_MARGIN parameter, after which vehicle will backaway from obstacles. Increase this parameter if you see vehicle going back and forth in front of obstacle.

- Units: m

- Range: 0 2

## AVOID_BACKZ_SPD: Avoidance maximum vertical backup speed

Maximum speed that will be used to back away from obstacles vertically in height control modes (m/s). Set zero to disable vertical backup.

- Units: m/s

- Range: 0 2

# BARO Parameters

## BARO1_GND_PRESS: Ground Pressure

*Note: This parameter is for advanced users*

calibrated ground pressure in Pascals

- Units: Pa

- Increment: 1

- ReadOnly: True

- Volatile: True

## BARO_GND_TEMP: ground temperature

*Note: This parameter is for advanced users*

User provided ambient ground temperature in degrees Celsius. This is used to improve the calculation of the altitude the vehicle is at. This parameter is not persistent and will be reset to 0 every time the vehicle is rebooted. A value of 0 means use the internal measurement ambient temperature.

- Units: degC

- Increment: 1

- Volatile: True

## BARO_ALT_OFFSET: altitude offset

*Note: This parameter is for advanced users*

altitude offset in meters added to barometric altitude. This is used to allow for automatic adjustment of the base barometric altitude by a ground station equipped with a barometer. The value is added to the barometric altitude read by the aircraft. It is automatically reset to 0 when the barometer is calibrated on each reboot or when a preflight calibration is performed.

- Units: m

- Increment: 0.1

## BARO_PRIMARY: Primary barometer

*Note: This parameter is for advanced users*

This selects which barometer will be the primary if multiple barometers are found

|Value|Meaning|
|:---:|:---:|
|0|FirstBaro|
|1|2ndBaro|
|2|3rdBaro|

## BARO_EXT_BUS: External baro bus

*Note: This parameter is for advanced users*

This selects the bus number for looking for an I2C barometer. When set to -1 it will probe all external i2c buses based on the BARO_PROBE_EXT parameter.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Bus0|
|1|Bus1|
|6|Bus6|

## BARO2_GND_PRESS: Ground Pressure

*Note: This parameter is for advanced users*

calibrated ground pressure in Pascals

- Units: Pa

- Increment: 1

- ReadOnly: True

- Volatile: True

## BARO3_GND_PRESS: Absolute Pressure

*Note: This parameter is for advanced users*

calibrated ground pressure in Pascals

- Units: Pa

- Increment: 1

- ReadOnly: True

- Volatile: True

## BARO_FLTR_RNG: Range in which sample is accepted

This sets the range around the average value that new samples must be within to be accepted. This can help reduce the impact of noise on sensors that are on long I2C cables. The value is a percentage from the average value. A value of zero disables this filter.

- Units: %

- Range: 0 100

- Increment: 1

## BARO_PROBE_EXT: External barometers to probe

*Note: This parameter is for advanced users*

This sets which types of external i2c barometer to look for. It is a bitmask of barometer types. The I2C buses to probe is based on BARO_EXT_BUS. If BARO_EXT_BUS is -1 then it will probe all external buses, otherwise it will probe just the bus number given in BARO_EXT_BUS.

- Bitmask: 0:BMP085,1:BMP280,2:MS5611,3:MS5607,4:MS5637,5:FBM320,6:DPS280,7:LPS25H,8:Keller,9:MS5837,10:BMP388,11:SPL06,12:MSP,13:BMP581

## BARO1_DEVID: Baro ID

*Note: This parameter is for advanced users*

Barometer sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## BARO2_DEVID: Baro ID2

*Note: This parameter is for advanced users*

Barometer2 sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## BARO3_DEVID: Baro ID3

*Note: This parameter is for advanced users*

Barometer3 sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## BARO_FIELD_ELV: field elevation

*Note: This parameter is for advanced users*

User provided field elevation in meters. This is used to improve the calculation of the altitude the vehicle is at. This parameter is not persistent and will be reset to 0 every time the vehicle is rebooted. Changes to this parameter will only be used when disarmed. A value of 0 means the EKF origin height is used for takeoff height above sea level.

- Units: m

- Increment: 0.1

- Volatile: True

## BARO_ALTERR_MAX: Altitude error maximum

*Note: This parameter is for advanced users*

This is the maximum acceptable altitude discrepancy between GPS altitude and barometric presssure altitude calculated against a standard atmosphere for arming checks to pass. If you are getting an arming error due to this parameter then you may have a faulty or substituted barometer. A common issue is vendors replacing a MS5611 in a "Pixhawk" with a MS5607. If you have that issue then please see BARO_OPTIONS parameter to force the MS5611 to be treated as a MS5607. This check is disabled if the value is zero.

- Units: m

- Increment: 1

- Range: 0 5000

## BARO_OPTIONS: Barometer options

*Note: This parameter is for advanced users*

Barometer options

- Bitmask: 0:Treat MS5611 as MS5607

# BARO1WCF Parameters

## BARO1_WCF_ENABLE: Wind coefficient enable

*Note: This parameter is for advanced users*

This enables the use of wind coefficients for barometer compensation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BARO1_WCF_FWD: Pressure error coefficient in positive X direction (forward)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the X body axis. If the baro height estimate rises during forwards flight, then this will be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO1_WCF_BCK: Pressure error coefficient in negative X direction (backwards)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the X body axis. If the baro height estimate rises during backwards flight, then this will be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO1_WCF_RGT: Pressure error coefficient in positive Y direction (right)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the Y body axis. If the baro height estimate rises during sideways flight to the right, then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO1_WCF_LFT: Pressure error coefficient in negative Y direction (left)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the Y body axis. If the baro height estimate rises during sideways flight to the left, then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO1_WCF_UP: Pressure error coefficient in positive Z direction (up)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the Z body axis. If the baro height estimate rises above truth height during climbing flight (or forward flight with a high forwards lean angle), then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO1_WCF_DN: Pressure error coefficient in negative Z direction (down)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the Z body axis. If the baro height estimate rises above truth height during descending flight (or forward flight with a high backwards lean angle, eg braking manoeuvre), then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

# BARO2WCF Parameters

## BARO2_WCF_ENABLE: Wind coefficient enable

*Note: This parameter is for advanced users*

This enables the use of wind coefficients for barometer compensation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BARO2_WCF_FWD: Pressure error coefficient in positive X direction (forward)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the X body axis. If the baro height estimate rises during forwards flight, then this will be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO2_WCF_BCK: Pressure error coefficient in negative X direction (backwards)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the X body axis. If the baro height estimate rises during backwards flight, then this will be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO2_WCF_RGT: Pressure error coefficient in positive Y direction (right)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the Y body axis. If the baro height estimate rises during sideways flight to the right, then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO2_WCF_LFT: Pressure error coefficient in negative Y direction (left)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the Y body axis. If the baro height estimate rises during sideways flight to the left, then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO2_WCF_UP: Pressure error coefficient in positive Z direction (up)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the Z body axis. If the baro height estimate rises above truth height during climbing flight (or forward flight with a high forwards lean angle), then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO2_WCF_DN: Pressure error coefficient in negative Z direction (down)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the Z body axis. If the baro height estimate rises above truth height during descending flight (or forward flight with a high backwards lean angle, eg braking manoeuvre), then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

# BARO3WCF Parameters

## BARO3_WCF_ENABLE: Wind coefficient enable

*Note: This parameter is for advanced users*

This enables the use of wind coefficients for barometer compensation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BARO3_WCF_FWD: Pressure error coefficient in positive X direction (forward)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the X body axis. If the baro height estimate rises during forwards flight, then this will be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO3_WCF_BCK: Pressure error coefficient in negative X direction (backwards)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the X body axis. If the baro height estimate rises during backwards flight, then this will be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO3_WCF_RGT: Pressure error coefficient in positive Y direction (right)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the Y body axis. If the baro height estimate rises during sideways flight to the right, then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO3_WCF_LFT: Pressure error coefficient in negative Y direction (left)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the Y body axis. If the baro height estimate rises during sideways flight to the left, then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO3_WCF_UP: Pressure error coefficient in positive Z direction (up)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a positive wind relative velocity along the Z body axis. If the baro height estimate rises above truth height during climbing flight (or forward flight with a high forwards lean angle), then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

## BARO3_WCF_DN: Pressure error coefficient in negative Z direction (down)

*Note: This parameter is for advanced users*

This is the ratio of static pressure error to dynamic pressure generated by a negative wind relative velocity along the Z body axis. If the baro height estimate rises above truth height during descending flight (or forward flight with a high backwards lean angle, eg braking manoeuvre), then this should be a negative number. Multirotors can use this feature only if using EKF3 and if the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters have been tuned.

- Range: -1.0 1.0

- Increment: 0.05

# BATT2 Parameters

## BATT2_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT2_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT2_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT2_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT2_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT2_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT2_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT2_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT2_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT2_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT2_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT2_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT2_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT2_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT2_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT2_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT2_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT2_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT2_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT2_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT2_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT2_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT2_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT2_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT2_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT2_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT2_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT2_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT2_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT2_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT2_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT2_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT2_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT2_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT2_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT2_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT2_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT2_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT2_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT2_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT2_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT2_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT2_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT2_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT2_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT2_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT2_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT3 Parameters

## BATT3_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT3_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT3_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT3_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT3_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT3_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT3_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT3_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT3_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT3_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT3_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT3_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT3_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT3_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT3_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT3_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT3_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT3_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT3_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT3_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT3_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT3_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT3_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT3_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT3_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT3_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT3_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT3_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT3_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT3_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT3_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT3_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT3_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT3_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT3_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT3_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT3_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT3_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT3_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT3_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT3_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT3_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT3_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT3_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT3_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT3_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT3_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT4 Parameters

## BATT4_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT4_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT4_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT4_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT4_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT4_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT4_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT4_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT4_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT4_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT4_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT4_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT4_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT4_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT4_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT4_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT4_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT4_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT4_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT4_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT4_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT4_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT4_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT4_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT4_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT4_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT4_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT4_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT4_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT4_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT4_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT4_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT4_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT4_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT4_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT4_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT4_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT4_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT4_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT4_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT4_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT4_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT4_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT4_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT4_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT4_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT4_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT5 Parameters

## BATT5_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT5_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT5_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT5_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT5_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT5_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT5_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT5_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT5_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT5_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT5_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT5_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT5_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT5_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT5_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT5_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT5_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT5_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT5_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT5_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT5_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT5_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT5_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT5_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT5_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT5_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT5_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT5_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT5_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT5_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT5_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT5_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT5_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT5_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT5_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT5_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT5_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT5_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT5_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT5_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT5_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT5_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT5_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT5_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT5_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT5_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT5_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT6 Parameters

## BATT6_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT6_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT6_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT6_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT6_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT6_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT6_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT6_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT6_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT6_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT6_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT6_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT6_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT6_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT6_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT6_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT6_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT6_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT6_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT6_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT6_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT6_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT6_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT6_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT6_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT6_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT6_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT6_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT6_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT6_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT6_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT6_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT6_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT6_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT6_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT6_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT6_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT6_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT6_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT6_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT6_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT6_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT6_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT6_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT6_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT6_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT6_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT7 Parameters

## BATT7_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT7_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT7_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT7_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT7_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT7_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT7_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT7_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT7_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT7_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT7_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT7_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT7_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT7_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT7_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT7_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT7_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT7_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT7_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT7_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT7_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT7_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT7_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT7_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT7_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT7_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT7_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT7_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT7_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT7_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT7_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT7_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT7_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT7_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT7_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT7_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT7_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT7_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT7_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT7_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT7_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT7_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT7_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT7_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT7_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT7_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT7_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT8 Parameters

## BATT8_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT8_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT8_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT8_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT8_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT8_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT8_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT8_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT8_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT8_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT8_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT8_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT8_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT8_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT8_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT8_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT8_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT8_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT8_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT8_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT8_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT8_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT8_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT8_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT8_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT8_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT8_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT8_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT8_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT8_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT8_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT8_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT8_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT8_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT8_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT8_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT8_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT8_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT8_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT8_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT8_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT8_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT8_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT8_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT8_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT8_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT8_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT9 Parameters

## BATT9_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT9_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT9_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT9_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT9_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT9_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT9_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT9_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT9_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT9_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT9_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT9_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT9_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT9_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT9_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT9_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT9_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT9_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT9_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT9_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT9_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT9_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT9_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT9_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT9_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT9_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT9_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT9_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT9_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT9_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT9_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT9_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT9_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT9_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT9_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT9_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT9_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT9_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT9_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT9_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT9_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT9_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT9_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT9_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT9_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT9_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT9_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTA Parameters

## BATTA_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTA_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTA_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTA_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTA_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTA_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTA_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTA_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTA_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTA_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTA_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTA_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTA_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTA_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTA_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTA_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTA_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTA_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTA_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTA_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTA_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTA_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTA_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTA_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTA_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTA_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTA_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTA_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTA_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTA_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTA_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTA_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTA_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTA_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTA_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTA_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTA_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTA_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTA_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTA_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTA_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTA_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTA_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTA_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTA_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTA_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTA_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTB Parameters

## BATTB_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTB_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTB_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTB_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTB_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTB_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTB_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTB_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTB_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTB_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTB_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTB_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTB_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTB_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTB_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTB_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTB_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTB_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTB_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTB_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTB_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTB_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTB_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTB_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTB_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTB_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTB_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTB_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTB_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTB_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTB_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTB_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTB_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTB_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTB_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTB_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTB_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTB_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTB_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTB_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTB_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTB_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTB_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTB_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTB_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTB_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTB_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTC Parameters

## BATTC_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTC_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTC_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTC_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTC_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTC_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTC_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTC_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTC_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTC_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTC_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTC_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTC_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTC_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTC_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTC_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTC_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTC_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTC_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTC_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTC_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTC_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTC_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTC_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTC_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTC_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTC_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTC_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTC_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTC_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTC_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTC_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTC_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTC_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTC_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTC_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTC_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTC_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTC_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTC_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTC_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTC_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTC_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTC_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTC_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTC_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTC_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTD Parameters

## BATTD_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTD_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTD_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTD_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTD_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTD_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTD_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTD_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTD_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTD_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTD_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTD_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTD_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTD_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTD_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTD_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTD_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTD_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTD_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTD_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTD_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTD_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTD_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTD_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTD_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTD_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTD_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTD_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTD_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTD_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTD_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTD_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTD_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTD_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTD_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTD_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTD_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTD_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTD_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTD_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTD_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTD_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTD_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTD_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTD_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTD_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTD_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTE Parameters

## BATTE_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTE_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTE_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTE_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTE_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTE_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTE_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTE_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTE_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTE_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTE_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTE_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTE_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTE_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTE_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTE_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTE_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTE_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTE_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTE_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTE_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTE_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTE_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTE_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTE_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTE_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTE_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTE_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTE_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTE_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTE_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTE_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTE_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTE_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTE_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTE_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTE_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTE_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTE_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTE_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTE_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTE_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTE_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTE_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTE_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTE_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTE_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTF Parameters

## BATTF_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTF_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTF_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTF_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTF_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTF_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTF_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTF_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTF_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTF_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTF_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTF_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTF_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTF_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTF_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTF_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTF_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTF_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTF_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTF_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTF_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTF_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTF_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTF_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTF_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTF_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTF_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTF_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTF_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTF_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTF_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTF_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTF_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTF_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTF_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTF_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTF_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTF_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTF_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTF_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTF_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTF_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTF_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTF_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTF_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTF_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTF_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATTG Parameters

## BATTG_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATTG_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATTG_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATTG_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATTG_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATTG_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTG_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTG_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATTG_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTG_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATTG_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATTG_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATTG_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATTG_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATTG_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATTG_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTG_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATTG_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATTG_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATTG_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATTG_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATTG_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATTG_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATTG_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATTG_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATTG_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATTG_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATTG_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATTG_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATTG_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTG_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATTG_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATTG_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATTG_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATTG_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATTG_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATTG_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATTG_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATTG_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATTG_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATTG_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATTG_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATTG_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATTG_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATTG_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATTG_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATTG_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BATT Parameters

## BATT_MONITOR: Battery monitoring

Controls enabling monitoring of the battery's voltage and current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|3|Analog Voltage Only|
|4|Analog Voltage and Current|
|5|Solo|
|6|Bebop|
|7|SMBus-Generic|
|8|DroneCAN-BatteryInfo|
|9|ESC|
|10|Sum Of Selected Monitors|
|11|FuelFlow|
|12|FuelLevelPWM|
|13|SMBUS-SUI3|
|14|SMBUS-SUI6|
|15|NeoDesign|
|16|SMBus-Maxell|
|17|Generator-Elec|
|18|Generator-Fuel|
|19|Rotoye|
|20|MPPT|
|21|INA2XX|
|22|LTC2946|
|23|Torqeedo|
|24|FuelLevelAnalog|
|25|Synthetic Current and Analog Voltage|
|26|INA239_SPI|
|27|EFI|
|28|AD7091R5|
|29|Scripting|

- RebootRequired: True

## BATT_CAPACITY: Battery capacity

Capacity of the battery in mAh when full

- Units: mAh

- Increment: 50

## BATT_SERIAL_NUM: Battery serial number

*Note: This parameter is for advanced users*

Battery serial number, automatically filled in for SMBus batteries, otherwise will be -1. With DroneCan it is the battery_id.

## BATT_LOW_TIMER: Low voltage timeout

*Note: This parameter is for advanced users*

This is the timeout in seconds before a low voltage event will be triggered. For aircraft with low C batteries it may be necessary to raise this in order to cope with low voltage on long takeoffs. A value of zero disables low voltage errors.

- Units: s

- Increment: 1

- Range: 0 120

## BATT_FS_VOLTSRC: Failsafe voltage source

*Note: This parameter is for advanced users*

Voltage type used for detection of low voltage event

|Value|Meaning|
|:---:|:---:|
|0|Raw Voltage|
|1|Sag Compensated Voltage|

## BATT_LOW_VOLT: Low battery voltage

Battery voltage that triggers a low battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT_FS_LOW_ACT parameter.

- Units: V

- Increment: 0.1

## BATT_LOW_MAH: Low battery capacity

Battery capacity at which the low battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT_FS_LOW_ACT parameter.

- Units: mAh

- Increment: 50

## BATT_CRT_VOLT: Critical battery voltage

Battery voltage that triggers a critical battery failsafe. Set to 0 to disable. If the battery voltage drops below this voltage continuously for more then the period specified by the BATT_LOW_TIMER parameter then the vehicle will perform the failsafe specified by the BATT_FS_CRT_ACT parameter.

- Units: V

- Increment: 0.1

## BATT_CRT_MAH: Battery critical capacity

Battery capacity at which the critical battery failsafe is triggered. Set to 0 to disable battery remaining failsafe. If the battery capacity drops below this level the vehicle will perform the failsafe specified by the BATT_FS_CRT_ACT parameter.

- Units: mAh

- Increment: 50

## BATT_FS_LOW_ACT: Low battery failsafe action

What action the vehicle should perform if it hits a low battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT_FS_CRT_ACT: Critical battery failsafe action

What action the vehicle should perform if it hits a critical battery failsafe

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|RTL|
|2|Hold|
|3|SmartRTL|
|4|SmartRTL or Hold|
|5|Terminate|

## BATT_ARM_VOLT: Required arming voltage

*Note: This parameter is for advanced users*

Battery voltage level which is required to arm the aircraft. Set to 0 to allow arming at any voltage.

- Units: V

- Increment: 0.1

## BATT_ARM_MAH: Required arming remaining capacity

*Note: This parameter is for advanced users*

Battery capacity remaining which is required to arm the aircraft. Set to 0 to allow arming at any capacity. Note that execept for smart batteries rebooting the vehicle will always reset the remaining capacity estimate, which can lead to this check not providing sufficent protection, it is recommended to always use this in conjunction with the BATT_ARM_VOLT parameter.

- Units: mAh

- Increment: 50

## BATT_OPTIONS: Battery monitor options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the battery monitor

- Bitmask: 0:Ignore DroneCAN SoC, 1:MPPT reports input voltage and current, 2:MPPT Powered off when disarmed, 3:MPPT Powered on when armed, 4:MPPT Powered off at boot, 5:MPPT Powered on at boot, 6:Send resistance compensated voltage to GCS, 7:Allow DroneCAN InfoAux to be from a different CAN node, 8:Battery is for internal autopilot use only, 9:Sum monitor measures minimum voltage instead of average

## BATT_ESC_INDEX: ESC Telemetry Index to write to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write voltage, current, consumption and temperature data to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## BATT_VOLT_PIN: Battery Voltage sensing pin

Sets the analog input pin that should be used for voltage monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

- RebootRequired: True

## BATT_CURR_PIN: Battery Current sensing pin

Sets the analog input pin that should be used for current monitoring.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|3|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|4|CubeOrange_PM2/Navigator|
|14|Pixhawk2_PM2|
|15|CubeOrange|
|17|Durandal|
|101|PX4-v1|

- RebootRequired: True

## BATT_VOLT_MULT: Voltage Multiplier

*Note: This parameter is for advanced users*

Used to convert the voltage of the voltage sensing pin (BATT_VOLT_PIN) to the actual battery's voltage (pin_voltage * VOLT_MULT). For the 3DR Power brick with a Pixhawk, this should be set to 10.1. For the Pixhawk with the 3DR 4in1 ESC this should be 12.02. For the PX using the PX4IO power supply this should be set to 1.

## BATT_AMP_PERVLT: Amps per volt

Number of amps that a 1V reading on the current sensor corresponds to. With a Pixhawk using the 3DR Power brick this should be set to 17. For the Pixhawk with the 3DR 4in1 ESC this should be 17. For Synthetic Current sensor monitors, this is the maximum, full throttle current draw.

- Units: A/V

## BATT_AMP_OFFSET: AMP offset

Voltage offset at zero current on current sensor for Analog Sensors. For Synthetic Current sensor, this offset is the zero throttle system current and is added to the calculated throttle base current.

- Units: V

## BATT_VLT_OFFSET: Voltage offset

*Note: This parameter is for advanced users*

Voltage offset on voltage pin. This allows for an offset due to a diode. This voltage is subtracted before the scaling is applied.

- Units: V

## BATT_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address

- Range: 0 127

- RebootRequired: True

## BATT_SUM_MASK: Battery Sum mask

0: sum of remaining battery monitors, If none 0 sum of specified monitors. Current will be summed and voltages averaged.

- Bitmask: 0:monitor 1, 1:monitor 2, 2:monitor 3, 3:monitor 4, 4:monitor 5, 5:monitor 6, 6:monitor 7, 7:monitor 8, 8:monitor 9

## BATT_CURR_MULT: Scales reported power monitor current

*Note: This parameter is for advanced users*

Multiplier applied to all current related reports to allow for adjustment if no UAVCAN param access or current splitting applications

- Range: .1 10

## BATT_FL_VLT_MIN: Empty fuel level voltage

*Note: This parameter is for advanced users*

The voltage seen on the analog pin when the fuel tank is empty. Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

- Units: V

## BATT_FL_V_MULT: Fuel level voltage multiplier

*Note: This parameter is for advanced users*

Voltage multiplier to determine what the full tank voltage reading is. This is calculated as 1 / (Voltage_Full - Voltage_Empty) Note: For this type of battery monitor, the voltage seen by the analog pin is displayed as battery voltage on a GCS.

- Range: 0.01 10

## BATT_FL_FLTR: Fuel level filter frequency

*Note: This parameter is for advanced users*

Filter frequency in Hertz where a low pass filter is used. This is used to filter out tank slosh from the fuel level reading. A value of -1 disables the filter and unfiltered voltage is used to determine the fuel level. The suggested values at in the range of 0.2 Hz to 0.5 Hz.

- Range: -1 1

- Units: Hz

- RebootRequired: True

## BATT_FL_PIN: Fuel level analog pin number

Analog input pin that fuel level sensor is connected to.Analog Airspeed or RSSI ports can be used for Analog input( some autopilots provide others also). Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## BATT_FL_FF: First order term

*Note: This parameter is for advanced users*

First order polynomial fit term

- Range: 0 10

## BATT_FL_FS: Second order term

*Note: This parameter is for advanced users*

Second order polynomial fit term

- Range: 0 10

## BATT_FL_FT: Third order term

*Note: This parameter is for advanced users*

Third order polynomial fit term

- Range: 0 10

## BATT_FL_OFF: Offset term

*Note: This parameter is for advanced users*

Offset polynomial fit term

- Range: 0 10

## BATT_MAX_VOLT: Maximum Battery Voltage

*Note: This parameter is for advanced users*

Maximum voltage of battery. Provides scaling of current versus voltage

- Range: 7 100

## BATT_I2C_BUS: Battery monitor I2C bus number

*Note: This parameter is for advanced users*

Battery monitor I2C bus number

- Range: 0 3

- RebootRequired: True

## BATT_I2C_ADDR: Battery monitor I2C address

*Note: This parameter is for advanced users*

Battery monitor I2C address. If this is zero then probe list of supported addresses

- Range: 0 127

- RebootRequired: True

## BATT_MAX_AMPS: Battery monitor max current

*Note: This parameter is for advanced users*

This controls the maximum current the INS2XX sensor will work with.

- Range: 1 400

- Units: A

## BATT_SHUNT: Battery monitor shunt resistor

*Note: This parameter is for advanced users*

This sets the shunt resistor used in the device

- Range: 0.0001 0.01

- Units: Ohm

## BATT_ESC_MASK: ESC mask

If 0 all connected ESCs will be used. If non-zero, only those selected in will be used.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

# BCN Parameters

## BCN_TYPE: Beacon based position estimation device type

*Note: This parameter is for advanced users*

What type of beacon based position estimation device is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Pozyx|
|2|Marvelmind|
|3|Nooploop|
|10|SITL|

## BCN_LATITUDE: Beacon origin's latitude

*Note: This parameter is for advanced users*

Beacon origin's latitude

- Units: deg

- Increment: 0.000001

- Range: -90 90

## BCN_LONGITUDE: Beacon origin's longitude

*Note: This parameter is for advanced users*

Beacon origin's longitude

- Units: deg

- Increment: 0.000001

- Range: -180 180

## BCN_ALT: Beacon origin's altitude above sealevel in meters

*Note: This parameter is for advanced users*

Beacon origin's altitude above sealevel in meters

- Units: m

- Increment: 1

- Range: 0 10000

## BCN_ORIENT_YAW: Beacon systems rotation from north in degrees

*Note: This parameter is for advanced users*

Beacon systems rotation from north in degrees

- Units: deg

- Increment: 1

- Range: -180 +180

# BRD Parameters

## BRD_SER1_RTSCTS: Serial 1 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 1 (telemetry 1). You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup. Note that the PX4v1 does not have hardware flow control pins on this port, so you should leave this disabled.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

- RebootRequired: True

## BRD_SER2_RTSCTS: Serial 2 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 2 (telemetry 2). You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

## BRD_SER3_RTSCTS: Serial 3 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 3. You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

## BRD_SER4_RTSCTS: Serial 4 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 4. You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

## BRD_SER5_RTSCTS: Serial 5 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 5. You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

## BRD_SER6_RTSCTS: Serial 6 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 6. You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

## BRD_SER7_RTSCTS: Serial 7 flow control

*Note: This parameter is for advanced users*

Enable flow control on serial 7. You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Auto|
|3|RS-485 Driver enable RTS pin|

## BRD_SER8_RTSCTS: Serial 8 flow control

Enable flow control on serial 8. You must have the RTS and CTS pins connected to your radio. The standard DF13 6 pin connector for a 3DR radio does have those pins connected. If this is set to 2 then flow control will be auto-detected by checking for the output buffer filling on startup.

## BRD_SAFETY_DEFLT: Sets default state of the safety switch

This controls the default state of the safety switch at startup. When set to 1 the safety switch will start in the safe state (flashing) at boot. When set to zero the safety switch will start in the unsafe state (solid) at startup. Note that if a safety switch is fitted the user can still control the safety state after startup using the switch. The safety state can also be controlled in software using a MAVLink message.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## BRD_SBUS_OUT:  SBUS output rate

*Note: This parameter is for advanced users*

This sets the SBUS output frame rate in Hz

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|50Hz|
|2|75Hz|
|3|100Hz|
|4|150Hz|
|5|200Hz|
|6|250Hz|
|7|300Hz|

- RebootRequired: True

## BRD_SERIAL_NUM: User-defined serial number

User-defined serial number of this vehicle, it can be any arbitrary number you want and has no effect on the autopilot

- Range: -8388608 8388607

## BRD_SAFETY_MASK: Outputs which ignore the safety switch state

*Note: This parameter is for advanced users*

A bitmask which controls what outputs can move while the safety switch has not been pressed

- Bitmask: 0:Output1,1:Output2,2:Output3,3:Output4,4:Output5,5:Output6,6:Output7,7:Output8,8:Output9,9:Output10,10:Output11,11:Output12,12:Output13,13:Output14

- RebootRequired: True

## BRD_HEAT_TARG: Board heater temperature target

*Note: This parameter is for advanced users*

Board heater target temperature for boards with controllable heating units. Set to -1 to disable the heater, please reboot after setting to -1.

- Range: -1 80

- Units: degC

## BRD_TYPE: Board type

*Note: This parameter is for advanced users*

This allows selection of a PX4 or VRBRAIN board type. If set to zero then the board type is auto-detected (PX4)

|Value|Meaning|
|:---:|:---:|
|0|AUTO|
|1|PX4V1|
|2|Pixhawk|
|3|Cube/Pixhawk2|
|4|Pixracer|
|5|PixhawkMini|
|6|Pixhawk2Slim|
|13|Intel Aero FC|
|14|Pixhawk Pro|
|20|AUAV2.1|
|21|PCNC1|
|22|MINDPXV2|
|23|SP01|
|24|CUAVv5/FMUV5|
|30|VRX BRAIN51|
|32|VRX BRAIN52|
|33|VRX BRAIN52E|
|34|VRX UBRAIN51|
|35|VRX UBRAIN52|
|36|VRX CORE10|
|38|VRX BRAIN54|
|39|PX4 FMUV6|
|100|PX4 OLDDRIVERS|

- RebootRequired: True

## BRD_IO_ENABLE: Enable IO co-processor

*Note: This parameter is for advanced users*

This allows for the IO co-processor on boards with an IOMCU to be disabled. Setting to 2 will enable the IOMCU but not attempt to update firmware on startup

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|EnableNoFWUpdate|

- RebootRequired: True

## BRD_SAFETYOPTION: Options for safety button behavior

This controls the activation of the safety button. It allows you to control if the safety button can be used for safety enable and/or disable, and whether the button is only active when disarmed

- Bitmask: 0:ActiveForSafetyDisable,1:ActiveForSafetyEnable,2:ActiveWhenArmed,3:Force safety on when the aircraft disarms

## BRD_VBUS_MIN: Autopilot board voltage requirement

*Note: This parameter is for advanced users*

Minimum voltage on the autopilot power rail to allow the aircraft to arm. 0 to disable the check.

- Units: V

- Range: 4.0 5.5

- Increment: 0.1

## BRD_VSERVO_MIN: Servo voltage requirement

*Note: This parameter is for advanced users*

Minimum voltage on the servo rail to allow the aircraft to arm. 0 to disable the check.

- Units: V

- Range: 3.3 12.0

- Increment: 0.1

## BRD_SD_SLOWDOWN: microSD slowdown

*Note: This parameter is for advanced users*

This is a scaling factor to slow down microSD operation. It can be used on flight board and microSD card combinations where full speed is not reliable. For normal full speed operation a value of 0 should be used.

- Range: 0 32

- Increment: 1

## BRD_PWM_VOLT_SEL: Set PWM Out Voltage

*Note: This parameter is for advanced users*

This sets the voltage max for PWM output pulses. 0 for 3.3V and 1 for 5V output. On boards with an IOMCU that support this parameter this option only affects the 8 main outputs, not the 6 auxiliary outputs. Using 5V output can help to reduce the impact of ESC noise interference corrupting signals to the ESCs.

|Value|Meaning|
|:---:|:---:|
|0|3.3V|
|1|5V|

## BRD_OPTIONS: Board options

*Note: This parameter is for advanced users*

Board specific option flags

- Bitmask: 0:Enable hardware watchdog, 1:Disable MAVftp, 2:Enable set of internal parameters, 3:Enable Debug Pins, 4:Unlock flash on reboot, 5:Write protect firmware flash on reboot, 6:Write protect bootloader flash on reboot, 7:Skip board validation, 8:Disable board arming gpio output change on arm/disarm

## BRD_BOOT_DELAY: Boot delay

*Note: This parameter is for advanced users*

This adds a delay in milliseconds to boot to ensure peripherals initialise fully

- Range: 0 10000

- Units: ms

## BRD_HEAT_P: Board Heater P gain

*Note: This parameter is for advanced users*

Board Heater P gain

- Range: 1 500

- Increment: 1

## BRD_HEAT_I: Board Heater I gain

*Note: This parameter is for advanced users*

Board Heater integrator gain

- Range: 0 1

- Increment: 0.1

## BRD_HEAT_IMAX: Board Heater IMAX

*Note: This parameter is for advanced users*

Board Heater integrator maximum

- Range: 0 100

- Increment: 1

## BRD_ALT_CONFIG: Alternative HW config

*Note: This parameter is for advanced users*

Select an alternative hardware configuration. A value of zero selects the default configuration for this board. Other values are board specific. Please see the documentation for your board for details on any alternative configuration values that may be available.

- Range: 0 10

- Increment: 1

- RebootRequired: True

## BRD_HEAT_LOWMGN: Board heater temp lower margin

*Note: This parameter is for advanced users*

Arming check will fail if temp is lower than this margin below BRD_HEAT_TARG. 0 disables the low temperature check

- Range: 0 20

- Units: degC

## BRD_SD_MISSION:  SDCard Mission size

*Note: This parameter is for advanced users*

This sets the amount of storage in kilobytes reserved on the microsd card in mission.stg for waypoint storage. Each waypoint uses 15 bytes.

- Range: 0 64

- RebootRequired: True

## BRD_SD_FENCE:  SDCard Fence size

*Note: This parameter is for advanced users*

This sets the amount of storage in kilobytes reserved on the microsd card in fence.stg for fence storage.

- Range: 0 64

- RebootRequired: True

## BRD_IO_DSHOT: Load DShot FW on IO

*Note: This parameter is for advanced users*

This loads the DShot firmware on the IO co-processor

|Value|Meaning|
|:---:|:---:|
|0|StandardFW|
|1|DshotFW|

- RebootRequired: True

# BRDRADIO Parameters

## BRD_RADIO_TYPE: Set type of direct attached radio

This enables support for direct attached radio receivers

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|CYRF6936|
|2|CC2500|
|3|BK2425|

## BRD_RADIO_PROT: protocol

*Note: This parameter is for advanced users*

Select air protocol

|Value|Meaning|
|:---:|:---:|
|0|Auto|
|1|DSM2|
|2|DSMX|

## BRD_RADIO_DEBUG: debug level

*Note: This parameter is for advanced users*

radio debug level

- Range: 0 4

## BRD_RADIO_DISCRC: disable receive CRC

*Note: This parameter is for advanced users*

disable receive CRC (for debug)

|Value|Meaning|
|:---:|:---:|
|0|NotDisabled|
|1|Disabled|

## BRD_RADIO_SIGCH: RSSI signal strength

*Note: This parameter is for advanced users*

Channel to show receive RSSI signal strength, or zero for disabled

- Range: 0 16

## BRD_RADIO_PPSCH: Packet rate channel

*Note: This parameter is for advanced users*

Channel to show received packet-per-second rate, or zero for disabled

- Range: 0 16

## BRD_RADIO_TELEM: Enable telemetry

*Note: This parameter is for advanced users*

If this is non-zero then telemetry packets will be sent over DSM

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BRD_RADIO_TXPOW: Telemetry Transmit power

*Note: This parameter is for advanced users*

Set telemetry transmit power. This is the power level (from 1 to 8) for telemetry packets sent from the RX to the TX

- Range: 1 8

## BRD_RADIO_FCCTST: Put radio into FCC test mode

*Note: This parameter is for advanced users*

If this is enabled then the radio will continuously transmit as required for FCC testing. The transmit channel is set by the value of the parameter. The radio will not work for RC input while this is enabled

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|MinChannel|
|2|MidChannel|
|3|MaxChannel|
|4|MinChannelCW|
|5|MidChannelCW|
|6|MaxChannelCW|

## BRD_RADIO_STKMD: Stick input mode

*Note: This parameter is for advanced users*

This selects between different stick input modes. The default is mode2, which has throttle on the left stick and pitch on the right stick. You can instead set mode1, which has throttle on the right stick and pitch on the left stick.

|Value|Meaning|
|:---:|:---:|
|1|Mode1|
|2|Mode2|

## BRD_RADIO_TESTCH: Set radio to factory test channel

*Note: This parameter is for advanced users*

This sets the radio to a fixed test channel for factory testing. Using a fixed channel avoids the need for binding in factory testing.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TestChan1|
|2|TestChan2|
|3|TestChan3|
|4|TestChan4|
|5|TestChan5|
|6|TestChan6|
|7|TestChan7|
|8|TestChan8|

## BRD_RADIO_TSIGCH: RSSI value channel for telemetry data on transmitter

*Note: This parameter is for advanced users*

Channel to show telemetry RSSI value as received by TX

- Range: 0 16

## BRD_RADIO_TPPSCH: Telemetry PPS channel

*Note: This parameter is for advanced users*

Channel to show telemetry packets-per-second value, as received at TX

- Range: 0 16

## BRD_RADIO_TXMAX: Transmitter transmit power

*Note: This parameter is for advanced users*

Set transmitter maximum transmit power (from 1 to 8)

- Range: 1 8

## BRD_RADIO_BZOFS: Transmitter buzzer adjustment

*Note: This parameter is for advanced users*

Set transmitter buzzer note adjustment (adjust frequency up)

- Range: 0 40

## BRD_RADIO_ABTIME: Auto-bind time

*Note: This parameter is for advanced users*

When non-zero this sets the time with no transmitter packets before we start looking for auto-bind packets.

- Range: 0 120

## BRD_RADIO_ABLVL: Auto-bind level

*Note: This parameter is for advanced users*

This sets the minimum RSSI of an auto-bind packet for it to be accepted. This should be set so that auto-bind will only happen at short range to minimise the change of an auto-bind happening accidentially

- Range: 0 31

# BRDRTC Parameters

## BRD_RTC_TYPES: Allowed sources of RTC time

*Note: This parameter is for advanced users*

Specifies which sources of UTC time will be accepted

- Bitmask: 0:GPS,1:MAVLINK_SYSTEM_TIME,2:HW

## BRD_RTC_TZ_MIN: Timezone offset from UTC

*Note: This parameter is for advanced users*

Adds offset in +- minutes from UTC to calculate local time

- Range: -720 +840

# BTN Parameters

## BTN_ENABLE: Enable button reporting

*Note: This parameter is for advanced users*

This enables the button checking module. When this is disabled the parameters for setting button inputs are not visible

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## BTN_PIN1: First button Pin

Digital pin number for first button input.  Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|

## BTN_PIN2: Second button Pin

Digital pin number for second button input.  Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|

## BTN_PIN3: Third button Pin

Digital pin number for third button input.  Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|

## BTN_PIN4: Fourth button Pin

Digital pin number for fourth button input. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|

## BTN_REPORT_SEND: Report send time

The duration in seconds that a BUTTON_CHANGE report is repeatedly sent to the GCS regarding a button changing state. Note that the BUTTON_CHANGE message is MAVLink2 only.

- Range: 0 3600

## BTN_OPTIONS1: Button Pin 1 Options

Options for Pin 1. PWM input detects PWM above or below 1800/1200us instead of logic level. If PWM is not detected or is less than 800us or above 2200us the button will interpreted as low. Invert changes HIGH state to be logic low voltage on pin, or below 1200us, if PWM input.

- Bitmask: 0:PWM Input,1:InvertInput

## BTN_OPTIONS2: Button Pin 2 Options

Options for Pin 2. PWM input detects PWM above or below 1800/1200us instead of logic level. If PWM is not detected or is less than 800us or above 2200us the button will interpreted as low. Invert changes HIGH state to be logic low voltage on pin, or below 1200us, if PWM input.

- Bitmask: 0:PWM Input,1:InvertInput

## BTN_OPTIONS3: Button Pin 3 Options

Options for Pin 3. PWM input detects PWM above or below 1800/1200us instead of logic level. If PWM is not detected or is less than 800us or above 2200us the button will interpreted as low. Invert changes HIGH state to be logic low voltage on pin, or below 1200us, if PWM input.

- Bitmask: 0:PWM Input,1:InvertInput

## BTN_OPTIONS4: Button Pin 4 Options

Options for Pin 4. PWM input detects PWM above or below 1800/1200us instead of logic level. If PWM is not detected or is less than 800us or above 2200us the button will interpreted as low. Invert changes HIGH state to be logic low voltage on pin, or below 1200us, if PWM input.

- Bitmask: 0:PWM Input,1:InvertInput

## BTN_FUNC1: Button Pin 1 RC Channel function

Auxiliary RC Options function executed on pin change

|Value|Meaning|
|:---:|:---:|
|0|Do Nothing|
|4|RTL|
|5|Save Trim (4.1 and lower)|
|7|Save WP|
|9|Camera Trigger|
|11|Fence Enable|
|16|AUTO Mode|
|19|Gripper Release|
|24|Auto Mission Reset|
|27|Retract Mount1|
|28|Relay1 On/Off|
|30|Lost Rover Sound|
|31|Motor Emergency Stop|
|34|Relay2 On/Off|
|35|Relay3 On/Off|
|36|Relay4 On/Off|
|40|Proximity Avoidance Enable|
|41|ArmDisarm (4.1 and lower)|
|42|SMARTRTL Mode|
|46|RC Override Enable|
|50|LearnCruise Speed|
|51|MANUAL Mode|
|52|ACRO Mode|
|53|STEERING Mode|
|54|HOLD Mode|
|55|GUIDED Mode|
|56|LOITER Mode|
|57|FOLLOW Mode|
|58|Clear Waypoints|
|59|Simple Mode|
|62|Compass Learn|
|63|Sailboat Tack|
|65|GPS Disable|
|66|Relay5 On/Off|
|67|Relay6 On/Off|
|72|CIRCLE Mode|
|74|Sailboat motoring 3pos|
|78|RunCam Control|
|79|RunCam OSD Control|
|80|VisoOdom Align|
|81|Disarm|
|90|EKF Source Set|
|94|VTX Power|
|97|Windvane home heading direction offset|
|100|KillIMU1|
|101|KillIMU2|
|102|Camera Mode Toggle|
|105|GPS Disable Yaw|
|106|Disable Airspeed Use|
|110|KillIMU3|
|112|SwitchExternalAHRS|
|113|Retract Mount2|
|153|ArmDisarm (4.2 and higher)|
|155|Set steering trim to current servo and RC|
|156|Torqeedo Clear Err|
|162|FFT Tune|
|163|Mount Lock|
|164|Pause Stream Logging|
|165|Arm/Emergency Motor Stop|
|166|Camera Record Video|
|167|Camera Zoom|
|168|Camera Manual Focus|
|169|Camera Auto Focus|
|171|Calibrate Compasses|
|172|Battery MPPT Enable|
|174|Camera Image Tracking|
|175|Camera Lens|
|177|Mount LRF enable|
|201|Roll|
|202|Pitch|
|207|MainSail|
|208|Flap|
|211|Walking Height|
|212|Mount1 Roll|
|213|Mount1 Pitch|
|214|Mount1 Yaw|
|215|Mount2 Roll|
|216|Mount2 Pitch|
|217|Mount2 Yaw|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

## BTN_FUNC2: Button Pin 2 RC Channel function

Auxiliary RC Options function executed on pin change

|Value|Meaning|
|:---:|:---:|
|0|Do Nothing|
|4|RTL|
|5|Save Trim (4.1 and lower)|
|7|Save WP|
|9|Camera Trigger|
|11|Fence Enable|
|16|AUTO Mode|
|19|Gripper Release|
|24|Auto Mission Reset|
|27|Retract Mount1|
|28|Relay1 On/Off|
|30|Lost Rover Sound|
|31|Motor Emergency Stop|
|34|Relay2 On/Off|
|35|Relay3 On/Off|
|36|Relay4 On/Off|
|40|Proximity Avoidance Enable|
|41|ArmDisarm (4.1 and lower)|
|42|SMARTRTL Mode|
|46|RC Override Enable|
|50|LearnCruise Speed|
|51|MANUAL Mode|
|52|ACRO Mode|
|53|STEERING Mode|
|54|HOLD Mode|
|55|GUIDED Mode|
|56|LOITER Mode|
|57|FOLLOW Mode|
|58|Clear Waypoints|
|59|Simple Mode|
|62|Compass Learn|
|63|Sailboat Tack|
|65|GPS Disable|
|66|Relay5 On/Off|
|67|Relay6 On/Off|
|72|CIRCLE Mode|
|74|Sailboat motoring 3pos|
|78|RunCam Control|
|79|RunCam OSD Control|
|80|VisoOdom Align|
|81|Disarm|
|90|EKF Source Set|
|94|VTX Power|
|97|Windvane home heading direction offset|
|100|KillIMU1|
|101|KillIMU2|
|102|Camera Mode Toggle|
|105|GPS Disable Yaw|
|106|Disable Airspeed Use|
|110|KillIMU3|
|112|SwitchExternalAHRS|
|113|Retract Mount2|
|153|ArmDisarm (4.2 and higher)|
|155|Set steering trim to current servo and RC|
|156|Torqeedo Clear Err|
|162|FFT Tune|
|163|Mount Lock|
|164|Pause Stream Logging|
|165|Arm/Emergency Motor Stop|
|166|Camera Record Video|
|167|Camera Zoom|
|168|Camera Manual Focus|
|169|Camera Auto Focus|
|171|Calibrate Compasses|
|172|Battery MPPT Enable|
|174|Camera Image Tracking|
|175|Camera Lens|
|177|Mount LRF enable|
|201|Roll|
|202|Pitch|
|207|MainSail|
|208|Flap|
|211|Walking Height|
|212|Mount1 Roll|
|213|Mount1 Pitch|
|214|Mount1 Yaw|
|215|Mount2 Roll|
|216|Mount2 Pitch|
|217|Mount2 Yaw|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

## BTN_FUNC3: Button Pin 3 RC Channel function

Auxiliary RC Options function executed on pin change

|Value|Meaning|
|:---:|:---:|
|0|Do Nothing|
|4|RTL|
|5|Save Trim (4.1 and lower)|
|7|Save WP|
|9|Camera Trigger|
|11|Fence Enable|
|16|AUTO Mode|
|19|Gripper Release|
|24|Auto Mission Reset|
|27|Retract Mount1|
|28|Relay1 On/Off|
|30|Lost Rover Sound|
|31|Motor Emergency Stop|
|34|Relay2 On/Off|
|35|Relay3 On/Off|
|36|Relay4 On/Off|
|40|Proximity Avoidance Enable|
|41|ArmDisarm (4.1 and lower)|
|42|SMARTRTL Mode|
|46|RC Override Enable|
|50|LearnCruise Speed|
|51|MANUAL Mode|
|52|ACRO Mode|
|53|STEERING Mode|
|54|HOLD Mode|
|55|GUIDED Mode|
|56|LOITER Mode|
|57|FOLLOW Mode|
|58|Clear Waypoints|
|59|Simple Mode|
|62|Compass Learn|
|63|Sailboat Tack|
|65|GPS Disable|
|66|Relay5 On/Off|
|67|Relay6 On/Off|
|72|CIRCLE Mode|
|74|Sailboat motoring 3pos|
|78|RunCam Control|
|79|RunCam OSD Control|
|80|VisoOdom Align|
|81|Disarm|
|90|EKF Source Set|
|94|VTX Power|
|97|Windvane home heading direction offset|
|100|KillIMU1|
|101|KillIMU2|
|102|Camera Mode Toggle|
|105|GPS Disable Yaw|
|106|Disable Airspeed Use|
|110|KillIMU3|
|112|SwitchExternalAHRS|
|113|Retract Mount2|
|153|ArmDisarm (4.2 and higher)|
|155|Set steering trim to current servo and RC|
|156|Torqeedo Clear Err|
|162|FFT Tune|
|163|Mount Lock|
|164|Pause Stream Logging|
|165|Arm/Emergency Motor Stop|
|166|Camera Record Video|
|167|Camera Zoom|
|168|Camera Manual Focus|
|169|Camera Auto Focus|
|171|Calibrate Compasses|
|172|Battery MPPT Enable|
|174|Camera Image Tracking|
|175|Camera Lens|
|177|Mount LRF enable|
|201|Roll|
|202|Pitch|
|207|MainSail|
|208|Flap|
|211|Walking Height|
|212|Mount1 Roll|
|213|Mount1 Pitch|
|214|Mount1 Yaw|
|215|Mount2 Roll|
|216|Mount2 Pitch|
|217|Mount2 Yaw|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

## BTN_FUNC4: Button Pin 4 RC Channel function

Auxiliary RC Options function executed on pin change

|Value|Meaning|
|:---:|:---:|
|0|Do Nothing|
|4|RTL|
|5|Save Trim (4.1 and lower)|
|7|Save WP|
|9|Camera Trigger|
|11|Fence Enable|
|16|AUTO Mode|
|19|Gripper Release|
|24|Auto Mission Reset|
|27|Retract Mount1|
|28|Relay1 On/Off|
|30|Lost Rover Sound|
|31|Motor Emergency Stop|
|34|Relay2 On/Off|
|35|Relay3 On/Off|
|36|Relay4 On/Off|
|40|Proximity Avoidance Enable|
|41|ArmDisarm (4.1 and lower)|
|42|SMARTRTL Mode|
|46|RC Override Enable|
|50|LearnCruise Speed|
|51|MANUAL Mode|
|52|ACRO Mode|
|53|STEERING Mode|
|54|HOLD Mode|
|55|GUIDED Mode|
|56|LOITER Mode|
|57|FOLLOW Mode|
|58|Clear Waypoints|
|59|Simple Mode|
|62|Compass Learn|
|63|Sailboat Tack|
|65|GPS Disable|
|66|Relay5 On/Off|
|67|Relay6 On/Off|
|72|CIRCLE Mode|
|74|Sailboat motoring 3pos|
|78|RunCam Control|
|79|RunCam OSD Control|
|80|VisoOdom Align|
|81|Disarm|
|90|EKF Source Set|
|94|VTX Power|
|97|Windvane home heading direction offset|
|100|KillIMU1|
|101|KillIMU2|
|102|Camera Mode Toggle|
|105|GPS Disable Yaw|
|106|Disable Airspeed Use|
|110|KillIMU3|
|112|SwitchExternalAHRS|
|113|Retract Mount2|
|153|ArmDisarm (4.2 and higher)|
|155|Set steering trim to current servo and RC|
|156|Torqeedo Clear Err|
|162|FFT Tune|
|163|Mount Lock|
|164|Pause Stream Logging|
|165|Arm/Emergency Motor Stop|
|166|Camera Record Video|
|167|Camera Zoom|
|168|Camera Manual Focus|
|169|Camera Auto Focus|
|171|Calibrate Compasses|
|172|Battery MPPT Enable|
|174|Camera Image Tracking|
|175|Camera Lens|
|177|Mount LRF enable|
|201|Roll|
|202|Pitch|
|207|MainSail|
|208|Flap|
|211|Walking Height|
|212|Mount1 Roll|
|213|Mount1 Pitch|
|214|Mount1 Yaw|
|215|Mount2 Roll|
|216|Mount2 Pitch|
|217|Mount2 Yaw|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

# CAM Parameters

## CAM_MAX_ROLL: Maximum photo roll angle.

Postpone shooting if roll is greater than limit. (0=Disable, will shoot regardless of roll).

- Units: deg

- Range: 0 180

## CAM_AUTO_ONLY: Distance-trigging in AUTO mode only

When enabled, trigging by distance is done in AUTO mode only.

|Value|Meaning|
|:---:|:---:|
|0|Always|
|1|Only when in AUTO|

# CAM1 Parameters

## CAM1_TYPE: Camera shutter (trigger) type

how to trigger the camera to take a picture

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Servo|
|2|Relay|
|3|GoPro in Solo Gimbal|
|4|Mount (Siyi/Topotek/Viewpro/Xacti)|
|5|MAVLink|
|6|MAVLinkCamV2|
|7|Scripting|

## CAM1_DURATION: Camera shutter duration held open

Duration in seconds that the camera shutter is held open

- Units: s

- Range: 0 5

## CAM1_SERVO_ON: Camera servo ON PWM value

PWM value in microseconds to move servo to when shutter is activated

- Units: PWM

- Range: 1000 2000

## CAM1_SERVO_OFF: Camera servo OFF PWM value

PWM value in microseconds to move servo to when shutter is deactivated

- Units: PWM

- Range: 1000 2000

## CAM1_TRIGG_DIST: Camera trigger distance

Distance in meters between camera triggers. If this value is non-zero then the camera will trigger whenever the position changes by this number of meters regardless of what mode the APM is in. Note that this parameter can also be set in an auto mission using the DO_SET_CAM_TRIGG_DIST command, allowing you to enable/disable the triggering of the camera during the flight.

- Units: m

- Range: 0 1000

## CAM1_RELAY_ON: Camera relay ON value

This sets whether the relay goes high or low when it triggers. Note that you should also set RELAY_DEFAULT appropriately for your camera

|Value|Meaning|
|:---:|:---:|
|0|Low|
|1|High|

## CAM1_INTRVAL_MIN: Camera minimum time interval between photos

Postpone shooting if previous picture was taken less than this many seconds ago

- Units: s

- Range: 0 10

## CAM1_FEEDBAK_PIN: Camera feedback pin

pin number to use for save accurate camera feedback messages. If set to -1 then don't use a pin flag for this, otherwise this is a pin number which if held high after a picture trigger order, will save camera messages when camera really takes a picture. A universal camera hot shoe is needed. The pin should be held high for at least 2 milliseconds for reliable trigger detection.  Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot. See also the CAMx_FEEDBCK_POL option.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

- RebootRequired: True

## CAM1_FEEDBAK_POL: Camera feedback pin polarity

Polarity for feedback pin. If this is 1 then the feedback pin should go high on trigger. If set to 0 then it should go low

|Value|Meaning|
|:---:|:---:|
|0|TriggerLow|
|1|TriggerHigh|

## CAM1_OPTIONS: Camera options

Camera options bitmask

- Bitmask: 0:Recording Starts at arming and stops at disarming

## CAM1_MNT_INST: Camera Mount instance

Mount instance camera is associated with. 0 means camera and mount have identical instance numbers e.g. camera1 and mount1

## CAM1_HFOV: Camera horizontal field of view

Camera horizontal field of view. 0 if unknown

- Units: deg

- Range: 0 360

## CAM1_VFOV: Camera vertical field of view

Camera vertical field of view. 0 if unknown

- Units: deg

- Range: 0 180

# CAM2 Parameters

## CAM2_TYPE: Camera shutter (trigger) type

how to trigger the camera to take a picture

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Servo|
|2|Relay|
|3|GoPro in Solo Gimbal|
|4|Mount (Siyi/Topotek/Viewpro/Xacti)|
|5|MAVLink|
|6|MAVLinkCamV2|
|7|Scripting|

## CAM2_DURATION: Camera shutter duration held open

Duration in seconds that the camera shutter is held open

- Units: s

- Range: 0 5

## CAM2_SERVO_ON: Camera servo ON PWM value

PWM value in microseconds to move servo to when shutter is activated

- Units: PWM

- Range: 1000 2000

## CAM2_SERVO_OFF: Camera servo OFF PWM value

PWM value in microseconds to move servo to when shutter is deactivated

- Units: PWM

- Range: 1000 2000

## CAM2_TRIGG_DIST: Camera trigger distance

Distance in meters between camera triggers. If this value is non-zero then the camera will trigger whenever the position changes by this number of meters regardless of what mode the APM is in. Note that this parameter can also be set in an auto mission using the DO_SET_CAM_TRIGG_DIST command, allowing you to enable/disable the triggering of the camera during the flight.

- Units: m

- Range: 0 1000

## CAM2_RELAY_ON: Camera relay ON value

This sets whether the relay goes high or low when it triggers. Note that you should also set RELAY_DEFAULT appropriately for your camera

|Value|Meaning|
|:---:|:---:|
|0|Low|
|1|High|

## CAM2_INTRVAL_MIN: Camera minimum time interval between photos

Postpone shooting if previous picture was taken less than this many seconds ago

- Units: s

- Range: 0 10

## CAM2_FEEDBAK_PIN: Camera feedback pin

pin number to use for save accurate camera feedback messages. If set to -1 then don't use a pin flag for this, otherwise this is a pin number which if held high after a picture trigger order, will save camera messages when camera really takes a picture. A universal camera hot shoe is needed. The pin should be held high for at least 2 milliseconds for reliable trigger detection.  Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot. See also the CAMx_FEEDBCK_POL option.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

- RebootRequired: True

## CAM2_FEEDBAK_POL: Camera feedback pin polarity

Polarity for feedback pin. If this is 1 then the feedback pin should go high on trigger. If set to 0 then it should go low

|Value|Meaning|
|:---:|:---:|
|0|TriggerLow|
|1|TriggerHigh|

## CAM2_OPTIONS: Camera options

Camera options bitmask

- Bitmask: 0:Recording Starts at arming and stops at disarming

## CAM2_MNT_INST: Camera Mount instance

Mount instance camera is associated with. 0 means camera and mount have identical instance numbers e.g. camera1 and mount1

## CAM2_HFOV: Camera horizontal field of view

Camera horizontal field of view. 0 if unknown

- Units: deg

- Range: 0 360

## CAM2_VFOV: Camera vertical field of view

Camera vertical field of view. 0 if unknown

- Units: deg

- Range: 0 180

# CAMRC Parameters

## CAM_RC_TYPE: RunCam device type

RunCam device type used to determine OSD menu structure and shutter options.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|RunCam Split Micro/RunCam with UART|
|2|RunCam Split|
|3|RunCam Split4 4k|
|4|RunCam Hybrid/RunCam Thumb Pro|
|5|Runcam 2 4k|

## CAM_RC_FEATURES: RunCam features available

*Note: This parameter is for advanced users*

The available features of the attached RunCam device. If 0 then the RunCam device will be queried for the features it supports, otherwise this setting is used.

- Bitmask: 0:Power Button,1:WiFi Button,2:Change Mode,3:5-Key OSD,4:Settings Access,5:DisplayPort,6:Start Recording,7:Stop Recording

## CAM_RC_BT_DELAY: RunCam boot delay before allowing updates

*Note: This parameter is for advanced users*

Time it takes for the RunCam to become fully ready in ms. If this is too short then commands can get out of sync.

## CAM_RC_BTN_DELAY: RunCam button delay before allowing further button presses

*Note: This parameter is for advanced users*

Time it takes for the a RunCam button press to be actived in ms. If this is too short then commands can get out of sync.

## CAM_RC_MDE_DELAY: RunCam mode delay before allowing further button presses

*Note: This parameter is for advanced users*

Time it takes for the a RunCam mode button press to be actived in ms. If a mode change first requires a video recording change then double this value is used. If this is too short then commands can get out of sync.

## CAM_RC_CONTROL: RunCam control option

*Note: This parameter is for advanced users*

Specifies the allowed actions required to enter the OSD menu and other option like autorecording

- Bitmask: 0:Stick yaw right,1:Stick roll right,2:3-position switch,3:2-position switch,4:Autorecording enabled

# CAN Parameters

## CAN_LOGLEVEL: Loglevel

*Note: This parameter is for advanced users*

Loglevel for recording initialisation and debug information from CAN Interface

- Range: 0 4

|Value|Meaning|
|:---:|:---:|
|0|Log None|
|1|Log Error|
|2|Log Warning and below|
|3|Log Info and below|
|4|Log Everything|

# CAND1 Parameters

## CAN_D1_PROTOCOL: Enable use of specific protocol over virtual driver

*Note: This parameter is for advanced users*

Enabling this option starts selected protocol that will use this virtual driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|DroneCAN|
|4|PiccoloCAN|
|6|EFI_NWPMU|
|7|USD1|
|8|KDECAN|
|10|Scripting|
|11|Benewake|
|12|Scripting2|
|13|TOFSenseP|
|14|RadarCAN (NanoRadar/Hexsoon)|

- RebootRequired: True

## CAN_D1_PROTOCOL2: Secondary protocol with 11 bit CAN addressing

*Note: This parameter is for advanced users*

Secondary protocol with 11 bit CAN addressing

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|7|USD1|
|10|Scripting|
|11|Benewake|
|12|Scripting2|
|13|TOFSenseP|
|14|RadarCAN (NanoRadar/Hexsoon)|

- RebootRequired: True

# CAND1PC Parameters

## CAN_D1_PC_ESC_BM: ESC channels

*Note: This parameter is for advanced users*

Bitmask defining which ESC (motor) channels are to be transmitted over Piccolo CAN

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D1_PC_ESC_RT: ESC output rate

*Note: This parameter is for advanced users*

Output rate of ESC command messages

- Units: Hz

- Range: 1 500

## CAN_D1_PC_SRV_BM: Servo channels

*Note: This parameter is for advanced users*

Bitmask defining which servo channels are to be transmitted over Piccolo CAN

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16

## CAN_D1_PC_SRV_RT: Servo command output rate

*Note: This parameter is for advanced users*

Output rate of servo command messages

- Units: Hz

- Range: 1 500

## CAN_D1_PC_ECU_ID: ECU Node ID

*Note: This parameter is for advanced users*

Node ID to send ECU throttle messages to. Set to zero to disable ECU throttle messages. Set to 255 to broadcast to all ECUs.

- Range: 0 255

## CAN_D1_PC_ECU_RT: ECU command output rate

*Note: This parameter is for advanced users*

Output rate of ECU command messages

- Units: Hz

- Range: 1 500

# CAND1UC Parameters

## CAN_D1_UC_NODE: Own node ID

*Note: This parameter is for advanced users*

DroneCAN node ID used by the driver itself on this network

- Range: 1 125

## CAN_D1_UC_SRV_BM: Output channels to be transmitted as servo over DroneCAN

Bitmask with one set for channel to be transmitted as a servo command over DroneCAN

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16, 16: Servo 17, 17: Servo 18, 18: Servo 19, 19: Servo 20, 20: Servo 21, 21: Servo 22, 22: Servo 23, 23: Servo 24, 24: Servo 25, 25: Servo 26, 26: Servo 27, 27: Servo 28, 28: Servo 29, 29: Servo 30, 30: Servo 31, 31: Servo 32

## CAN_D1_UC_ESC_BM: Output channels to be transmitted as ESC over DroneCAN

*Note: This parameter is for advanced users*

Bitmask with one set for channel to be transmitted as a ESC command over DroneCAN

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D1_UC_SRV_RT: Servo output rate

*Note: This parameter is for advanced users*

Maximum transmit rate for servo outputs

- Range: 1 200

- Units: Hz

## CAN_D1_UC_OPTION: DroneCAN options

*Note: This parameter is for advanced users*

Option flags

- Bitmask: 0:ClearDNADatabase,1:IgnoreDNANodeConflicts,2:EnableCanfd,3:IgnoreDNANodeUnhealthy,4:SendServoAsPWM,5:SendGNSS,6:UseHimarkServo,7:HobbyWingESC,8:EnableStats,9:EnableFlexDebug

## CAN_D1_UC_NTF_RT: Notify State rate

*Note: This parameter is for advanced users*

Maximum transmit rate for Notify State Message

- Range: 1 200

- Units: Hz

## CAN_D1_UC_ESC_OF: ESC Output channels offset

*Note: This parameter is for advanced users*

Offset for ESC numbering in DroneCAN ESC RawCommand messages. This allows for more efficient packing of ESC command messages. If your ESCs are on servo functions 5 to 8 and you set this parameter to 4 then the ESC RawCommand will be sent with the first 4 slots filled. This can be used for more efficient usage of CAN bandwidth

- Range: 0 18

## CAN_D1_UC_POOL: CAN pool size

*Note: This parameter is for advanced users*

Amount of memory in bytes to allocate for the DroneCAN memory pool. More memory is needed for higher CAN bus loads

- Range: 1024 16384

## CAN_D1_UC_ESC_RV: Bitmask for output channels for reversible ESCs over DroneCAN.

*Note: This parameter is for advanced users*

Bitmask with one set for each output channel that uses a reversible ESC over DroneCAN. Reversible ESCs use both positive and negative values in RawCommands, with positive commanding the forward direction and negative commanding the reverse direction.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D1_UC_RLY_RT: DroneCAN relay output rate

*Note: This parameter is for advanced users*

Maximum transmit rate for relay outputs, note that this rate is per message each message does 1 relay, so if with more relays will take longer to update at the same rate, a extra message will be sent when a relay changes state

- Range: 0 200

- Units: Hz

## CAN_D1_UC_SER_EN: DroneCAN Serial enable

*Note: This parameter is for advanced users*

Enable DroneCAN virtual serial ports

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## CAN_D1_UC_S1_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN remote node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D1_UC_S1_IDX: DroneCAN Serial1 index

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

- RebootRequired: True

## CAN_D1_UC_S1_BD: DroneCAN Serial default baud rate

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D1_UC_S1_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## CAN_D1_UC_S2_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN remote node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D1_UC_S2_IDX: Serial port number on remote CAN node

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_D1_UC_S2_BD: DroneCAN Serial default baud rate

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D1_UC_S2_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## CAN_D1_UC_S3_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D1_UC_S3_IDX: Serial port number on remote CAN node

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_D1_UC_S3_BD: Serial baud rate on remote CAN node

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D1_UC_S3_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

# CAND2 Parameters

## CAN_D2_PROTOCOL: Enable use of specific protocol over virtual driver

*Note: This parameter is for advanced users*

Enabling this option starts selected protocol that will use this virtual driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|DroneCAN|
|4|PiccoloCAN|
|6|EFI_NWPMU|
|7|USD1|
|8|KDECAN|
|10|Scripting|
|11|Benewake|
|12|Scripting2|
|13|TOFSenseP|
|14|RadarCAN (NanoRadar/Hexsoon)|

- RebootRequired: True

## CAN_D2_PROTOCOL2: Secondary protocol with 11 bit CAN addressing

*Note: This parameter is for advanced users*

Secondary protocol with 11 bit CAN addressing

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|7|USD1|
|10|Scripting|
|11|Benewake|
|12|Scripting2|
|13|TOFSenseP|
|14|RadarCAN (NanoRadar/Hexsoon)|

- RebootRequired: True

# CAND2PC Parameters

## CAN_D2_PC_ESC_BM: ESC channels

*Note: This parameter is for advanced users*

Bitmask defining which ESC (motor) channels are to be transmitted over Piccolo CAN

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D2_PC_ESC_RT: ESC output rate

*Note: This parameter is for advanced users*

Output rate of ESC command messages

- Units: Hz

- Range: 1 500

## CAN_D2_PC_SRV_BM: Servo channels

*Note: This parameter is for advanced users*

Bitmask defining which servo channels are to be transmitted over Piccolo CAN

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16

## CAN_D2_PC_SRV_RT: Servo command output rate

*Note: This parameter is for advanced users*

Output rate of servo command messages

- Units: Hz

- Range: 1 500

## CAN_D2_PC_ECU_ID: ECU Node ID

*Note: This parameter is for advanced users*

Node ID to send ECU throttle messages to. Set to zero to disable ECU throttle messages. Set to 255 to broadcast to all ECUs.

- Range: 0 255

## CAN_D2_PC_ECU_RT: ECU command output rate

*Note: This parameter is for advanced users*

Output rate of ECU command messages

- Units: Hz

- Range: 1 500

# CAND2UC Parameters

## CAN_D2_UC_NODE: Own node ID

*Note: This parameter is for advanced users*

DroneCAN node ID used by the driver itself on this network

- Range: 1 125

## CAN_D2_UC_SRV_BM: Output channels to be transmitted as servo over DroneCAN

Bitmask with one set for channel to be transmitted as a servo command over DroneCAN

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16, 16: Servo 17, 17: Servo 18, 18: Servo 19, 19: Servo 20, 20: Servo 21, 21: Servo 22, 22: Servo 23, 23: Servo 24, 24: Servo 25, 25: Servo 26, 26: Servo 27, 27: Servo 28, 28: Servo 29, 29: Servo 30, 30: Servo 31, 31: Servo 32

## CAN_D2_UC_ESC_BM: Output channels to be transmitted as ESC over DroneCAN

*Note: This parameter is for advanced users*

Bitmask with one set for channel to be transmitted as a ESC command over DroneCAN

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D2_UC_SRV_RT: Servo output rate

*Note: This parameter is for advanced users*

Maximum transmit rate for servo outputs

- Range: 1 200

- Units: Hz

## CAN_D2_UC_OPTION: DroneCAN options

*Note: This parameter is for advanced users*

Option flags

- Bitmask: 0:ClearDNADatabase,1:IgnoreDNANodeConflicts,2:EnableCanfd,3:IgnoreDNANodeUnhealthy,4:SendServoAsPWM,5:SendGNSS,6:UseHimarkServo,7:HobbyWingESC,8:EnableStats,9:EnableFlexDebug

## CAN_D2_UC_NTF_RT: Notify State rate

*Note: This parameter is for advanced users*

Maximum transmit rate for Notify State Message

- Range: 1 200

- Units: Hz

## CAN_D2_UC_ESC_OF: ESC Output channels offset

*Note: This parameter is for advanced users*

Offset for ESC numbering in DroneCAN ESC RawCommand messages. This allows for more efficient packing of ESC command messages. If your ESCs are on servo functions 5 to 8 and you set this parameter to 4 then the ESC RawCommand will be sent with the first 4 slots filled. This can be used for more efficient usage of CAN bandwidth

- Range: 0 18

## CAN_D2_UC_POOL: CAN pool size

*Note: This parameter is for advanced users*

Amount of memory in bytes to allocate for the DroneCAN memory pool. More memory is needed for higher CAN bus loads

- Range: 1024 16384

## CAN_D2_UC_ESC_RV: Bitmask for output channels for reversible ESCs over DroneCAN.

*Note: This parameter is for advanced users*

Bitmask with one set for each output channel that uses a reversible ESC over DroneCAN. Reversible ESCs use both positive and negative values in RawCommands, with positive commanding the forward direction and negative commanding the reverse direction.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D2_UC_RLY_RT: DroneCAN relay output rate

*Note: This parameter is for advanced users*

Maximum transmit rate for relay outputs, note that this rate is per message each message does 1 relay, so if with more relays will take longer to update at the same rate, a extra message will be sent when a relay changes state

- Range: 0 200

- Units: Hz

## CAN_D2_UC_SER_EN: DroneCAN Serial enable

*Note: This parameter is for advanced users*

Enable DroneCAN virtual serial ports

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## CAN_D2_UC_S1_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN remote node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D2_UC_S1_IDX: DroneCAN Serial1 index

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

- RebootRequired: True

## CAN_D2_UC_S1_BD: DroneCAN Serial default baud rate

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D2_UC_S1_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## CAN_D2_UC_S2_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN remote node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D2_UC_S2_IDX: Serial port number on remote CAN node

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_D2_UC_S2_BD: DroneCAN Serial default baud rate

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D2_UC_S2_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## CAN_D2_UC_S3_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D2_UC_S3_IDX: Serial port number on remote CAN node

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_D2_UC_S3_BD: Serial baud rate on remote CAN node

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D2_UC_S3_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

# CAND3 Parameters

## CAN_D3_PROTOCOL: Enable use of specific protocol over virtual driver

*Note: This parameter is for advanced users*

Enabling this option starts selected protocol that will use this virtual driver

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|DroneCAN|
|4|PiccoloCAN|
|6|EFI_NWPMU|
|7|USD1|
|8|KDECAN|
|10|Scripting|
|11|Benewake|
|12|Scripting2|
|13|TOFSenseP|
|14|RadarCAN (NanoRadar/Hexsoon)|

- RebootRequired: True

## CAN_D3_PROTOCOL2: Secondary protocol with 11 bit CAN addressing

*Note: This parameter is for advanced users*

Secondary protocol with 11 bit CAN addressing

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|7|USD1|
|10|Scripting|
|11|Benewake|
|12|Scripting2|
|13|TOFSenseP|
|14|RadarCAN (NanoRadar/Hexsoon)|

- RebootRequired: True

# CAND3PC Parameters

## CAN_D3_PC_ESC_BM: ESC channels

*Note: This parameter is for advanced users*

Bitmask defining which ESC (motor) channels are to be transmitted over Piccolo CAN

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D3_PC_ESC_RT: ESC output rate

*Note: This parameter is for advanced users*

Output rate of ESC command messages

- Units: Hz

- Range: 1 500

## CAN_D3_PC_SRV_BM: Servo channels

*Note: This parameter is for advanced users*

Bitmask defining which servo channels are to be transmitted over Piccolo CAN

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16

## CAN_D3_PC_SRV_RT: Servo command output rate

*Note: This parameter is for advanced users*

Output rate of servo command messages

- Units: Hz

- Range: 1 500

## CAN_D3_PC_ECU_ID: ECU Node ID

*Note: This parameter is for advanced users*

Node ID to send ECU throttle messages to. Set to zero to disable ECU throttle messages. Set to 255 to broadcast to all ECUs.

- Range: 0 255

## CAN_D3_PC_ECU_RT: ECU command output rate

*Note: This parameter is for advanced users*

Output rate of ECU command messages

- Units: Hz

- Range: 1 500

# CAND3UC Parameters

## CAN_D3_UC_NODE: Own node ID

*Note: This parameter is for advanced users*

DroneCAN node ID used by the driver itself on this network

- Range: 1 125

## CAN_D3_UC_SRV_BM: Output channels to be transmitted as servo over DroneCAN

Bitmask with one set for channel to be transmitted as a servo command over DroneCAN

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16, 16: Servo 17, 17: Servo 18, 18: Servo 19, 19: Servo 20, 20: Servo 21, 21: Servo 22, 22: Servo 23, 23: Servo 24, 24: Servo 25, 25: Servo 26, 26: Servo 27, 27: Servo 28, 28: Servo 29, 29: Servo 30, 30: Servo 31, 31: Servo 32

## CAN_D3_UC_ESC_BM: Output channels to be transmitted as ESC over DroneCAN

*Note: This parameter is for advanced users*

Bitmask with one set for channel to be transmitted as a ESC command over DroneCAN

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D3_UC_SRV_RT: Servo output rate

*Note: This parameter is for advanced users*

Maximum transmit rate for servo outputs

- Range: 1 200

- Units: Hz

## CAN_D3_UC_OPTION: DroneCAN options

*Note: This parameter is for advanced users*

Option flags

- Bitmask: 0:ClearDNADatabase,1:IgnoreDNANodeConflicts,2:EnableCanfd,3:IgnoreDNANodeUnhealthy,4:SendServoAsPWM,5:SendGNSS,6:UseHimarkServo,7:HobbyWingESC,8:EnableStats,9:EnableFlexDebug

## CAN_D3_UC_NTF_RT: Notify State rate

*Note: This parameter is for advanced users*

Maximum transmit rate for Notify State Message

- Range: 1 200

- Units: Hz

## CAN_D3_UC_ESC_OF: ESC Output channels offset

*Note: This parameter is for advanced users*

Offset for ESC numbering in DroneCAN ESC RawCommand messages. This allows for more efficient packing of ESC command messages. If your ESCs are on servo functions 5 to 8 and you set this parameter to 4 then the ESC RawCommand will be sent with the first 4 slots filled. This can be used for more efficient usage of CAN bandwidth

- Range: 0 18

## CAN_D3_UC_POOL: CAN pool size

*Note: This parameter is for advanced users*

Amount of memory in bytes to allocate for the DroneCAN memory pool. More memory is needed for higher CAN bus loads

- Range: 1024 16384

## CAN_D3_UC_ESC_RV: Bitmask for output channels for reversible ESCs over DroneCAN.

*Note: This parameter is for advanced users*

Bitmask with one set for each output channel that uses a reversible ESC over DroneCAN. Reversible ESCs use both positive and negative values in RawCommands, with positive commanding the forward direction and negative commanding the reverse direction.

- Bitmask: 0: ESC 1, 1: ESC 2, 2: ESC 3, 3: ESC 4, 4: ESC 5, 5: ESC 6, 6: ESC 7, 7: ESC 8, 8: ESC 9, 9: ESC 10, 10: ESC 11, 11: ESC 12, 12: ESC 13, 13: ESC 14, 14: ESC 15, 15: ESC 16, 16: ESC 17, 17: ESC 18, 18: ESC 19, 19: ESC 20, 20: ESC 21, 21: ESC 22, 22: ESC 23, 23: ESC 24, 24: ESC 25, 25: ESC 26, 26: ESC 27, 27: ESC 28, 28: ESC 29, 29: ESC 30, 30: ESC 31, 31: ESC 32

## CAN_D3_UC_RLY_RT: DroneCAN relay output rate

*Note: This parameter is for advanced users*

Maximum transmit rate for relay outputs, note that this rate is per message each message does 1 relay, so if with more relays will take longer to update at the same rate, a extra message will be sent when a relay changes state

- Range: 0 200

- Units: Hz

## CAN_D3_UC_SER_EN: DroneCAN Serial enable

*Note: This parameter is for advanced users*

Enable DroneCAN virtual serial ports

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## CAN_D3_UC_S1_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN remote node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D3_UC_S1_IDX: DroneCAN Serial1 index

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

- RebootRequired: True

## CAN_D3_UC_S1_BD: DroneCAN Serial default baud rate

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D3_UC_S1_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## CAN_D3_UC_S2_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN remote node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D3_UC_S2_IDX: Serial port number on remote CAN node

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_D3_UC_S2_BD: DroneCAN Serial default baud rate

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D3_UC_S2_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## CAN_D3_UC_S3_NOD: Serial CAN remote node number

*Note: This parameter is for advanced users*

CAN node number for serial port

- Range: 0 127

- RebootRequired: True

## CAN_D3_UC_S3_IDX: Serial port number on remote CAN node

*Note: This parameter is for advanced users*

Serial port number on remote CAN node

- Range: 0 100

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_D3_UC_S3_BD: Serial baud rate on remote CAN node

*Note: This parameter is for advanced users*

Serial baud rate on remote CAN node

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## CAN_D3_UC_S3_PRO: Serial protocol of DroneCAN serial port

*Note: This parameter is for advanced users*

Serial protocol of DroneCAN serial port

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

# CANP1 Parameters

## CAN_P1_DRIVER: Index of virtual driver to be used with physical CAN interface

Enabling this option enables use of CAN buses.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|First driver|
|2|Second driver|
|3|Third driver|

- RebootRequired: True

## CAN_P1_BITRATE: Bitrate of CAN interface

*Note: This parameter is for advanced users*

Bit rate can be set up to from 10000 to 1000000

- Range: 10000 1000000

## CAN_P1_FDBITRATE: Bitrate of CANFD interface

*Note: This parameter is for advanced users*

Bit rate can be set up to from 1000000 to 8000000

|Value|Meaning|
|:---:|:---:|
|1|1M|
|2|2M|
|4|4M|
|5|5M|
|8|8M|

## CAN_P1_OPTIONS: CAN per-interface options

*Note: This parameter is for advanced users*

CAN per-interface options

- Bitmask: 0:LogAllFrames

# CANP2 Parameters

## CAN_P2_DRIVER: Index of virtual driver to be used with physical CAN interface

Enabling this option enables use of CAN buses.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|First driver|
|2|Second driver|
|3|Third driver|

- RebootRequired: True

## CAN_P2_BITRATE: Bitrate of CAN interface

*Note: This parameter is for advanced users*

Bit rate can be set up to from 10000 to 1000000

- Range: 10000 1000000

## CAN_P2_FDBITRATE: Bitrate of CANFD interface

*Note: This parameter is for advanced users*

Bit rate can be set up to from 1000000 to 8000000

|Value|Meaning|
|:---:|:---:|
|1|1M|
|2|2M|
|4|4M|
|5|5M|
|8|8M|

## CAN_P2_OPTIONS: CAN per-interface options

*Note: This parameter is for advanced users*

CAN per-interface options

- Bitmask: 0:LogAllFrames

# CANP3 Parameters

## CAN_P3_DRIVER: Index of virtual driver to be used with physical CAN interface

Enabling this option enables use of CAN buses.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|First driver|
|2|Second driver|
|3|Third driver|

- RebootRequired: True

## CAN_P3_BITRATE: Bitrate of CAN interface

*Note: This parameter is for advanced users*

Bit rate can be set up to from 10000 to 1000000

- Range: 10000 1000000

## CAN_P3_FDBITRATE: Bitrate of CANFD interface

*Note: This parameter is for advanced users*

Bit rate can be set up to from 1000000 to 8000000

|Value|Meaning|
|:---:|:---:|
|1|1M|
|2|2M|
|4|4M|
|5|5M|
|8|8M|

## CAN_P3_OPTIONS: CAN per-interface options

*Note: This parameter is for advanced users*

CAN per-interface options

- Bitmask: 0:LogAllFrames

# CANSLCAN Parameters

## CAN_SLCAN_CPORT: SLCAN Route

CAN Interface ID to be routed to SLCAN, 0 means no routing

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|First interface|
|2|Second interface|

- RebootRequired: True

## CAN_SLCAN_SERNUM: SLCAN Serial Port

Serial Port ID to be used for temporary SLCAN iface, -1 means no temporary serial. This parameter is automatically reset on reboot or on timeout. See CAN_SLCAN_TIMOUT for timeout details

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## CAN_SLCAN_TIMOUT: SLCAN Timeout

Duration of inactivity after which SLCAN is switched back to original driver in seconds.

- Range: 0 127

## CAN_SLCAN_SDELAY: SLCAN Start Delay

Duration after which slcan starts after setting SERNUM in seconds.

- Range: 0 127

# CIRC Parameters

## CIRC_RADIUS: Circle Radius

Vehicle will circle the center at this distance

- Units: m

- Range: 0 100

- Increment: 1

## CIRC_SPEED: Circle Speed

Vehicle will move at this speed around the circle.  If set to zero WP_SPEED will be used

- Units: m/s

- Range: 0 10

- Increment: 0.1

## CIRC_DIR: Circle Direction

Circle Direction

|Value|Meaning|
|:---:|:---:|
|0|Clockwise|
|1|Counter-Clockwise|

# COMPASS Parameters

## COMPASS_OFS_X: Compass offsets in milligauss on the X axis

*Note: This parameter is for advanced users*

Offset to be added to the compass x-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_OFS_Y: Compass offsets in milligauss on the Y axis

*Note: This parameter is for advanced users*

Offset to be added to the compass y-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_OFS_Z: Compass offsets in milligauss on the Z axis

*Note: This parameter is for advanced users*

Offset to be added to the compass z-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_DEC: Compass declination

An angle to compensate between the true north and magnetic north

- Range: -3.142 3.142

- Units: rad

- Increment: 0.01

## COMPASS_LEARN: Learn compass offsets automatically

*Note: This parameter is for advanced users*

Enable or disable the automatic learning of compass offsets. You can enable learning either using a compass-only method that is suitable only for fixed wing aircraft or using the offsets learnt by the active EKF state estimator. If this option is enabled then the learnt offsets are saved when you disarm the vehicle. If InFlight learning is enabled then the compass with automatically start learning once a flight starts (must be armed). While InFlight learning is running you cannot use position control modes.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Internal-Learning|
|2|EKF-Learning|
|3|InFlight-Learning|

## COMPASS_USE: Use compass for yaw

*Note: This parameter is for advanced users*

Enable or disable the use of the compass (instead of the GPS) for determining heading

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## COMPASS_AUTODEC: Auto Declination

*Note: This parameter is for advanced users*

Enable or disable the automatic calculation of the declination based on gps location

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## COMPASS_MOTCT: Motor interference compensation type

*Note: This parameter is for advanced users*

Set motor interference compensation type to disabled, throttle or current.  Do not change manually.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Use Throttle|
|2|Use Current|

- Calibration: 1

## COMPASS_MOT_X: Motor interference compensation for body frame X axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to the compass's x-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_MOT_Y: Motor interference compensation for body frame Y axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to the compass's y-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_MOT_Z: Motor interference compensation for body frame Z axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to the compass's z-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_ORIENT: Compass orientation

*Note: This parameter is for advanced users*

The orientation of the first external compass relative to the vehicle frame. This value will be ignored unless this compass is set as an external compass. When set correctly in the northern hemisphere, pointing the nose and right side down should increase the MagX and MagY values respectively. Rolling the vehicle upside down should decrease the MagZ value. For southern hemisphere, switch increase and decrease. NOTE: For internal compasses, AHRS_ORIENT is used. The label for each option is specified in the order of rotations for that orientation. Firmware versions 4.2 and prior can use a CUSTOM (100) rotation to set the COMPASS_CUS_ROLL/PIT/YAW angles for Compass orientation. Later versions provide two general custom rotations which can be used, Custom 1 and Custom 2, with CUST_1_ROLL/PIT/YAW or CUST_2_ROLL/PIT/YAW angles.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Yaw45|
|2|Yaw90|
|3|Yaw135|
|4|Yaw180|
|5|Yaw225|
|6|Yaw270|
|7|Yaw315|
|8|Roll180|
|9|Yaw45Roll180|
|10|Yaw90Roll180|
|11|Yaw135Roll180|
|12|Pitch180|
|13|Yaw225Roll180|
|14|Yaw270Roll180|
|15|Yaw315Roll180|
|16|Roll90|
|17|Yaw45Roll90|
|18|Yaw90Roll90|
|19|Yaw135Roll90|
|20|Roll270|
|21|Yaw45Roll270|
|22|Yaw90Roll270|
|23|Yaw135Roll270|
|24|Pitch90|
|25|Pitch270|
|26|Yaw90Pitch180|
|27|Yaw270Pitch180|
|28|Pitch90Roll90|
|29|Pitch90Roll180|
|30|Pitch90Roll270|
|31|Pitch180Roll90|
|32|Pitch180Roll270|
|33|Pitch270Roll90|
|34|Pitch270Roll180|
|35|Pitch270Roll270|
|36|Yaw90Pitch180Roll90|
|37|Yaw270Roll90|
|38|Yaw293Pitch68Roll180|
|39|Pitch315|
|40|Pitch315Roll90|
|42|Roll45|
|43|Roll315|
|100|Custom 4.1 and older|
|101|Custom 1|
|102|Custom 2|

## COMPASS_EXTERNAL: Compass is attached via an external cable

*Note: This parameter is for advanced users*

Configure compass so it is attached externally. This is auto-detected on most boards. Set to 1 if the compass is externally connected. When externally connected the COMPASS_ORIENT option operates independently of the AHRS_ORIENTATION board orientation option. If set to 0 or 1 then auto-detection by bus connection can override the value. If set to 2 then auto-detection will be disabled.

|Value|Meaning|
|:---:|:---:|
|0|Internal|
|1|External|
|2|ForcedExternal|

## COMPASS_OFS2_X: Compass2 offsets in milligauss on the X axis

*Note: This parameter is for advanced users*

Offset to be added to compass2's x-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_OFS2_Y: Compass2 offsets in milligauss on the Y axis

*Note: This parameter is for advanced users*

Offset to be added to compass2's y-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_OFS2_Z: Compass2 offsets in milligauss on the Z axis

*Note: This parameter is for advanced users*

Offset to be added to compass2's z-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_MOT2_X: Motor interference compensation to compass2 for body frame X axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to compass2's x-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_MOT2_Y: Motor interference compensation to compass2 for body frame Y axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to compass2's y-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_MOT2_Z: Motor interference compensation to compass2 for body frame Z axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to compass2's z-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_OFS3_X: Compass3 offsets in milligauss on the X axis

*Note: This parameter is for advanced users*

Offset to be added to compass3's x-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_OFS3_Y: Compass3 offsets in milligauss on the Y axis

*Note: This parameter is for advanced users*

Offset to be added to compass3's y-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_OFS3_Z: Compass3 offsets in milligauss on the Z axis

*Note: This parameter is for advanced users*

Offset to be added to compass3's z-axis values to compensate for metal in the frame

- Range: -400 400

- Units: mGauss

- Increment: 1

- Calibration: 1

## COMPASS_MOT3_X: Motor interference compensation to compass3 for body frame X axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to compass3's x-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_MOT3_Y: Motor interference compensation to compass3 for body frame Y axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to compass3's y-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_MOT3_Z: Motor interference compensation to compass3 for body frame Z axis

*Note: This parameter is for advanced users*

Multiplied by the current throttle and added to compass3's z-axis values to compensate for motor interference (Offset per Amp or at Full Throttle)

- Range: -1000 1000

- Units: mGauss/A

- Increment: 1

- Calibration: 1

## COMPASS_DEV_ID: Compass device id

*Note: This parameter is for advanced users*

Compass device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_DEV_ID2: Compass2 device id

*Note: This parameter is for advanced users*

Second compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_DEV_ID3: Compass3 device id

*Note: This parameter is for advanced users*

Third compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_USE2: Compass2 used for yaw

*Note: This parameter is for advanced users*

Enable or disable the secondary compass for determining heading.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## COMPASS_ORIENT2: Compass2 orientation

*Note: This parameter is for advanced users*

The orientation of a second external compass relative to the vehicle frame. This value will be ignored unless this compass is set as an external compass. When set correctly in the northern hemisphere, pointing the nose and right side down should increase the MagX and MagY values respectively. Rolling the vehicle upside down should decrease the MagZ value. For southern hemisphere, switch increase and decrease. NOTE: For internal compasses, AHRS_ORIENT is used. The label for each option is specified in the order of rotations for that orientation. Firmware versions 4.2 and prior can use a CUSTOM (100) rotation to set the COMPASS_CUS_ROLL/PIT/YAW angles for Compass orientation. Later versions provide two general custom rotations which can be used, Custom 1 and Custom 2, with CUST_1_ROLL/PIT/YAW or CUST_2_ROLL/PIT/YAW angles.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Yaw45|
|2|Yaw90|
|3|Yaw135|
|4|Yaw180|
|5|Yaw225|
|6|Yaw270|
|7|Yaw315|
|8|Roll180|
|9|Yaw45Roll180|
|10|Yaw90Roll180|
|11|Yaw135Roll180|
|12|Pitch180|
|13|Yaw225Roll180|
|14|Yaw270Roll180|
|15|Yaw315Roll180|
|16|Roll90|
|17|Yaw45Roll90|
|18|Yaw90Roll90|
|19|Yaw135Roll90|
|20|Roll270|
|21|Yaw45Roll270|
|22|Yaw90Roll270|
|23|Yaw135Roll270|
|24|Pitch90|
|25|Pitch270|
|26|Yaw90Pitch180|
|27|Yaw270Pitch180|
|28|Pitch90Roll90|
|29|Pitch90Roll180|
|30|Pitch90Roll270|
|31|Pitch180Roll90|
|32|Pitch180Roll270|
|33|Pitch270Roll90|
|34|Pitch270Roll180|
|35|Pitch270Roll270|
|36|Yaw90Pitch180Roll90|
|37|Yaw270Roll90|
|38|Yaw293Pitch68Roll180|
|39|Pitch315|
|40|Pitch315Roll90|
|42|Roll45|
|43|Roll315|
|100|Custom 4.1 and older|
|101|Custom 1|
|102|Custom 2|

## COMPASS_EXTERN2: Compass2 is attached via an external cable

*Note: This parameter is for advanced users*

Configure second compass so it is attached externally. This is auto-detected on most boards. If set to 0 or 1 then auto-detection by bus connection can override the value. If set to 2 then auto-detection will be disabled.

|Value|Meaning|
|:---:|:---:|
|0|Internal|
|1|External|
|2|ForcedExternal|

## COMPASS_USE3: Compass3 used for yaw

*Note: This parameter is for advanced users*

Enable or disable the tertiary compass for determining heading.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## COMPASS_ORIENT3: Compass3 orientation

*Note: This parameter is for advanced users*

The orientation of a third external compass relative to the vehicle frame. This value will be ignored unless this compass is set as an external compass. When set correctly in the northern hemisphere, pointing the nose and right side down should increase the MagX and MagY values respectively. Rolling the vehicle upside down should decrease the MagZ value. For southern hemisphere, switch increase and decrease. NOTE: For internal compasses, AHRS_ORIENT is used. The label for each option is specified in the order of rotations for that orientation. Firmware versions 4.2 and prior can use a CUSTOM (100) rotation to set the COMPASS_CUS_ROLL/PIT/YAW angles for Compass orientation. Later versions provide two general custom rotations which can be used, Custom 1 and Custom 2, with CUST_1_ROLL/PIT/YAW or CUST_2_ROLL/PIT/YAW angles.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Yaw45|
|2|Yaw90|
|3|Yaw135|
|4|Yaw180|
|5|Yaw225|
|6|Yaw270|
|7|Yaw315|
|8|Roll180|
|9|Yaw45Roll180|
|10|Yaw90Roll180|
|11|Yaw135Roll180|
|12|Pitch180|
|13|Yaw225Roll180|
|14|Yaw270Roll180|
|15|Yaw315Roll180|
|16|Roll90|
|17|Yaw45Roll90|
|18|Yaw90Roll90|
|19|Yaw135Roll90|
|20|Roll270|
|21|Yaw45Roll270|
|22|Yaw90Roll270|
|23|Yaw135Roll270|
|24|Pitch90|
|25|Pitch270|
|26|Yaw90Pitch180|
|27|Yaw270Pitch180|
|28|Pitch90Roll90|
|29|Pitch90Roll180|
|30|Pitch90Roll270|
|31|Pitch180Roll90|
|32|Pitch180Roll270|
|33|Pitch270Roll90|
|34|Pitch270Roll180|
|35|Pitch270Roll270|
|36|Yaw90Pitch180Roll90|
|37|Yaw270Roll90|
|38|Yaw293Pitch68Roll180|
|39|Pitch315|
|40|Pitch315Roll90|
|42|Roll45|
|43|Roll315|
|100|Custom 4.1 and older|
|101|Custom 1|
|102|Custom 2|

## COMPASS_EXTERN3: Compass3 is attached via an external cable

*Note: This parameter is for advanced users*

Configure third compass so it is attached externally. This is auto-detected on most boards. If set to 0 or 1 then auto-detection by bus connection can override the value. If set to 2 then auto-detection will be disabled.

|Value|Meaning|
|:---:|:---:|
|0|Internal|
|1|External|
|2|ForcedExternal|

## COMPASS_DIA_X: Compass soft-iron diagonal X component

*Note: This parameter is for advanced users*

DIA_X in the compass soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA_Y: Compass soft-iron diagonal Y component

*Note: This parameter is for advanced users*

DIA_Y in the compass soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA_Z: Compass soft-iron diagonal Z component

*Note: This parameter is for advanced users*

DIA_Z in the compass soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI_X: Compass soft-iron off-diagonal X component

*Note: This parameter is for advanced users*

ODI_X in the compass soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI_Y: Compass soft-iron off-diagonal Y component

*Note: This parameter is for advanced users*

ODI_Y in the compass soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI_Z: Compass soft-iron off-diagonal Z component

*Note: This parameter is for advanced users*

ODI_Z in the compass soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA2_X: Compass2 soft-iron diagonal X component

*Note: This parameter is for advanced users*

DIA_X in the compass2 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA2_Y: Compass2 soft-iron diagonal Y component

*Note: This parameter is for advanced users*

DIA_Y in the compass2 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA2_Z: Compass2 soft-iron diagonal Z component

*Note: This parameter is for advanced users*

DIA_Z in the compass2 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI2_X: Compass2 soft-iron off-diagonal X component

*Note: This parameter is for advanced users*

ODI_X in the compass2 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI2_Y: Compass2 soft-iron off-diagonal Y component

*Note: This parameter is for advanced users*

ODI_Y in the compass2 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI2_Z: Compass2 soft-iron off-diagonal Z component

*Note: This parameter is for advanced users*

ODI_Z in the compass2 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA3_X: Compass3 soft-iron diagonal X component

*Note: This parameter is for advanced users*

DIA_X in the compass3 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA3_Y: Compass3 soft-iron diagonal Y component

*Note: This parameter is for advanced users*

DIA_Y in the compass3 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_DIA3_Z: Compass3 soft-iron diagonal Z component

*Note: This parameter is for advanced users*

DIA_Z in the compass3 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI3_X: Compass3 soft-iron off-diagonal X component

*Note: This parameter is for advanced users*

ODI_X in the compass3 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI3_Y: Compass3 soft-iron off-diagonal Y component

*Note: This parameter is for advanced users*

ODI_Y in the compass3 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_ODI3_Z: Compass3 soft-iron off-diagonal Z component

*Note: This parameter is for advanced users*

ODI_Z in the compass3 soft-iron calibration matrix: [[DIA_X, ODI_X, ODI_Y], [ODI_X, DIA_Y, ODI_Z], [ODI_Y, ODI_Z, DIA_Z]]

- Calibration: 1

## COMPASS_CAL_FIT: Compass calibration fitness

*Note: This parameter is for advanced users*

This controls the fitness level required for a successful compass calibration. A lower value makes for a stricter fit (less likely to pass). This is the value used for the primary magnetometer. Other magnetometers get double the value.

- Range: 4 32

|Value|Meaning|
|:---:|:---:|
|4|Very Strict|
|8|Strict|
|16|Default|
|32|Relaxed|

- Increment: 0.1

## COMPASS_OFFS_MAX: Compass maximum offset

*Note: This parameter is for advanced users*

This sets the maximum allowed compass offset in calibration and arming checks

- Range: 500 3000

- Increment: 1

## COMPASS_DISBLMSK: Compass disable driver type mask

*Note: This parameter is for advanced users*

This is a bitmask of driver types to disable. If a driver type is set in this mask then that driver will not try to find a sensor at startup

- Bitmask: 0:HMC5883,1:LSM303D,2:AK8963,3:BMM150,4:LSM9DS1,5:LIS3MDL,6:AK09916,7:IST8310,8:ICM20948,9:MMC3416,11:DroneCAN,12:QMC5883,14:MAG3110,15:IST8308,16:RM3100,17:MSP,18:ExternalAHRS,19:MMC5XX3,20:QMC5883P,21:BMM350,22:IIS2MDC

## COMPASS_FLTR_RNG: Range in which sample is accepted

This sets the range around the average value that new samples must be within to be accepted. This can help reduce the impact of noise on sensors that are on long I2C cables. The value is a percentage from the average value. A value of zero disables this filter.

- Units: %

- Range: 0 100

- Increment: 1

## COMPASS_AUTO_ROT: Automatically check orientation

When enabled this will automatically check the orientation of compasses on successful completion of compass calibration. If set to 2 then external compasses will have their orientation automatically corrected.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|CheckOnly|
|2|CheckAndFix|
|3|use same tolerance to auto rotate 45 deg rotations|

## COMPASS_PRIO1_ID: Compass device id with 1st order priority

*Note: This parameter is for advanced users*

Compass device id with 1st order priority, set automatically if 0. Reboot required after change.

- RebootRequired: True

## COMPASS_PRIO2_ID: Compass device id with 2nd order priority

*Note: This parameter is for advanced users*

Compass device id with 2nd order priority, set automatically if 0. Reboot required after change.

- RebootRequired: True

## COMPASS_PRIO3_ID: Compass device id with 3rd order priority

*Note: This parameter is for advanced users*

Compass device id with 3rd order priority, set automatically if 0. Reboot required after change.

- RebootRequired: True

## COMPASS_ENABLE: Enable Compass

Setting this to Enabled(1) will enable the compass. Setting this to Disabled(0) will disable the compass. Note that this is separate from COMPASS_USE. This will enable the low level senor, and will enable logging of magnetometer data. To use the compass for navigation you must also set COMPASS_USE to 1.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## COMPASS_SCALE: Compass1 scale factor

Scaling factor for first compass to compensate for sensor scaling errors. If this is 0 then no scaling is done

- Range: 0 1.3

## COMPASS_SCALE2: Compass2 scale factor

Scaling factor for 2nd compass to compensate for sensor scaling errors. If this is 0 then no scaling is done

- Range: 0 1.3

## COMPASS_SCALE3: Compass3 scale factor

Scaling factor for 3rd compass to compensate for sensor scaling errors. If this is 0 then no scaling is done

- Range: 0 1.3

## COMPASS_OPTIONS: Compass options

*Note: This parameter is for advanced users*

This sets options to change the behaviour of the compass

- Bitmask: 0:CalRequireGPS, 1: Allow missing DroneCAN compasses to be automaticaly replaced (calibration still required)

## COMPASS_DEV_ID4: Compass4 device id

*Note: This parameter is for advanced users*

Extra 4th compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_DEV_ID5: Compass5 device id

*Note: This parameter is for advanced users*

Extra 5th compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_DEV_ID6: Compass6 device id

*Note: This parameter is for advanced users*

Extra 6th compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_DEV_ID7: Compass7 device id

*Note: This parameter is for advanced users*

Extra 7th compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_DEV_ID8: Compass8 device id

*Note: This parameter is for advanced users*

Extra 8th compass's device id.  Automatically detected, do not set manually

- ReadOnly: True

## COMPASS_CUS_ROLL: Custom orientation roll offset

*Note: This parameter is for advanced users*

Compass mounting position roll offset. Positive values = roll right, negative values = roll left. This parameter is only used when COMPASS_ORIENT/2/3 is set to CUSTOM.

- Range: -180 180

- Units: deg

- Increment: 1

- RebootRequired: True

## COMPASS_CUS_PIT: Custom orientation pitch offset

*Note: This parameter is for advanced users*

Compass mounting position pitch offset. Positive values = pitch up, negative values = pitch down. This parameter is only used when COMPASS_ORIENT/2/3 is set to CUSTOM.

- Range: -180 180

- Units: deg

- Increment: 1

- RebootRequired: True

## COMPASS_CUS_YAW: Custom orientation yaw offset

*Note: This parameter is for advanced users*

Compass mounting position yaw offset. Positive values = yaw right, negative values = yaw left. This parameter is only used when COMPASS_ORIENT/2/3 is set to CUSTOM.

- Range: -180 180

- Units: deg

- Increment: 1

- RebootRequired: True

# COMPASSPMOT Parameters

## COMPASS_PMOT_EN: per-motor compass correction enable

*Note: This parameter is for advanced users*

This enables per-motor compass corrections

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## COMPASS_PMOT_EXP: per-motor exponential correction

*Note: This parameter is for advanced users*

This is the exponential correction for the power output of the motor for per-motor compass correction

- Range: 0 2

- Increment: 0.01

## COMPASS_PMOT1_X: Compass per-motor1 X

*Note: This parameter is for advanced users*

Compensation for X axis of motor1

## COMPASS_PMOT1_Y: Compass per-motor1 Y

*Note: This parameter is for advanced users*

Compensation for Y axis of motor1

## COMPASS_PMOT1_Z: Compass per-motor1 Z

*Note: This parameter is for advanced users*

Compensation for Z axis of motor1

## COMPASS_PMOT2_X: Compass per-motor2 X

*Note: This parameter is for advanced users*

Compensation for X axis of motor2

## COMPASS_PMOT2_Y: Compass per-motor2 Y

*Note: This parameter is for advanced users*

Compensation for Y axis of motor2

## COMPASS_PMOT2_Z: Compass per-motor2 Z

*Note: This parameter is for advanced users*

Compensation for Z axis of motor2

## COMPASS_PMOT3_X: Compass per-motor3 X

*Note: This parameter is for advanced users*

Compensation for X axis of motor3

## COMPASS_PMOT3_Y: Compass per-motor3 Y

*Note: This parameter is for advanced users*

Compensation for Y axis of motor3

## COMPASS_PMOT3_Z: Compass per-motor3 Z

*Note: This parameter is for advanced users*

Compensation for Z axis of motor3

## COMPASS_PMOT4_X: Compass per-motor4 X

*Note: This parameter is for advanced users*

Compensation for X axis of motor4

## COMPASS_PMOT4_Y: Compass per-motor4 Y

*Note: This parameter is for advanced users*

Compensation for Y axis of motor4

## COMPASS_PMOT4_Z: Compass per-motor4 Z

*Note: This parameter is for advanced users*

Compensation for Z axis of motor4

# CUSTROT Parameters

## CUST_ROT_ENABLE: Enable Custom rotations

This enables custom rotations

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

- RebootRequired: True

# CUSTROT1 Parameters

## CUST_ROT1_ROLL: Custom roll

Custom euler roll, euler 321 (yaw, pitch, roll) ordering

- Units: deg

- RebootRequired: True

## CUST_ROT1_PITCH: Custom pitch

Custom euler pitch, euler 321 (yaw, pitch, roll) ordering

- Units: deg

- RebootRequired: True

## CUST_ROT1_YAW: Custom yaw

Custom euler yaw, euler 321 (yaw, pitch, roll) ordering

- Units: deg

- RebootRequired: True

# CUSTROT2 Parameters

## CUST_ROT2_ROLL: Custom roll

Custom euler roll, euler 321 (yaw, pitch, roll) ordering

- Units: deg

- RebootRequired: True

## CUST_ROT2_PITCH: Custom pitch

Custom euler pitch, euler 321 (yaw, pitch, roll) ordering

- Units: deg

- RebootRequired: True

## CUST_ROT2_YAW: Custom yaw

Custom euler yaw, euler 321 (yaw, pitch, roll) ordering

- Units: deg

- RebootRequired: True

# DDS Parameters

## DDS_ENABLE: DDS enable

*Note: This parameter is for advanced users*

Enable DDS subsystem

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## DDS_UDP_PORT: DDS UDP port

UDP port number for DDS

- Range: 1 65535

- RebootRequired: True

## DDS_DOMAIN_ID: DDS DOMAIN ID

Set the ROS_DOMAIN_ID

- Range: 0 232

- RebootRequired: True

## DDS_TIMEOUT_MS: DDS ping timeout

The time in milliseconds the DDS client will wait for a response from the XRCE agent before reattempting.

- Units: ms

- Range: 1 10000

- RebootRequired: True

- Increment: 1

## DDS_MAX_RETRY: DDS ping max attempts

The maximum number of times the DDS client will attempt to ping the XRCE agent before exiting. Set to 0 to allow unlimited retries.

- Range: 0 100

- RebootRequired: True

- Increment: 1

# DDSIP Parameters

## DDS_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## DDS_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## DDS_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## DDS_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# DID Parameters

## DID_ENABLE: Enable ODID subsystem

Enable ODID subsystem

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## DID_MAVPORT: MAVLink serial port

Serial port number to send OpenDroneID MAVLink messages to. Can be -1 if using DroneCAN.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## DID_CANDRIVER: DroneCAN driver number

DroneCAN driver index, 0 to disable DroneCAN

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Driver1|
|2|Driver2|

## DID_OPTIONS: OpenDroneID options

Options for OpenDroneID subsystem

- Bitmask: 0:EnforceArming, 1:AllowNonGPSPosition, 2:LockUASIDOnFirstBasicIDRx

## DID_BARO_ACC: Barometer vertical accuraacy

*Note: This parameter is for advanced users*

Barometer Vertical Accuracy when installed in the vehicle. Note this is dependent upon installation conditions and thus disabled by default

- Units: m

# DOCK Parameters

## DOCK_SPEED: Dock mode speed

Vehicle speed limit in dock mode

- Units: m/s

- Range: 0 100

- Increment: 0.1

## DOCK_DIR: Dock mode direction of approach

*Note: This parameter is for advanced users*

Compass direction in which vehicle should approach towards dock. -1 value represents unset parameter

- Units: deg

- Range: 0 360

- Increment: 1

## DOCK_HDG_CORR_EN: Dock mode heading correction enable/disable

*Note: This parameter is for advanced users*

When enabled, the autopilot modifies the path to approach the target head-on along desired line of approch in dock mode

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## DOCK_HDG_CORR_WT: Dock mode heading correction weight

*Note: This parameter is for advanced users*

This value describes how aggressively vehicle tries to correct its heading to be on desired line of approach

- Range: 0.00 0.90

- Increment: 0.05

## DOCK_STOP_DIST: Distance from docking target when we should stop

The vehicle starts stopping when it is this distance away from docking target

- Units: m

- Range: 0 2

- Increment: 0.01

# EAHRS Parameters

## EAHRS_TYPE: AHRS type

Type of AHRS device

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|VectorNav|
|2|MicroStrain5|
|5|InertialLabs|
|7|MicroStrain7|

## EAHRS_RATE: AHRS data rate

Requested rate for AHRS device

- Units: Hz

## EAHRS_OPTIONS: External AHRS options

External AHRS options bitmask

- Bitmask: 0:Vector Nav use uncompensated values for accel gyro and mag.

## EAHRS_SENSORS: External AHRS sensors

*Note: This parameter is for advanced users*

External AHRS sensors bitmask

- Bitmask: 0:GPS,1:IMU,2:Baro,3:Compass

## EAHRS_LOG_RATE: AHRS logging rate

Logging rate for EARHS devices

- Units: Hz

# EFI Parameters

## EFI_TYPE: EFI communication type

*Note: This parameter is for advanced users*

What method of communication is used for EFI #1

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Serial-MS|
|2|NWPMU|
|3|Serial-Lutan|
|5|DroneCAN|
|6|Currawong-ECU|
|7|Scripting|
|8|Hirth|
|9|MAVLink|

- RebootRequired: True

## EFI_COEF1: EFI Calibration Coefficient 1

*Note: This parameter is for advanced users*

Used to calibrate fuel flow for MS protocol (Slope). This should be calculated from a log at constant fuel usage rate. Plot (ECYL[0].InjT*EFI.Rpm)/600.0 to get the duty_cycle. Measure actual fuel usage in cm^3/min, and set EFI_COEF1 = fuel_usage_cm3permin / duty_cycle

- Range: 0 1

## EFI_COEF2: EFI Calibration Coefficient 2

*Note: This parameter is for advanced users*

Used to calibrate fuel flow for MS protocol (Offset). This can be used to correct for a non-zero offset in the fuel consumption calculation of EFI_COEF1

- Range: 0 10

## EFI_FUEL_DENS: ECU Fuel Density

*Note: This parameter is for advanced users*

Used to calculate fuel consumption

- Units: kg/m/m/m

- Range: 0 10000

# EFITHRLIN Parameters

## EFI_THRLIN_EN: Enable throttle linearisation

*Note: This parameter is for advanced users*

Enable EFI throttle linearisation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## EFI_THRLIN_COEF1: Throttle linearisation - First Order

*Note: This parameter is for advanced users*

First Order Polynomial Coefficient. (=1, if throttle is first order polynomial trendline)

- Range: -1 1

- RebootRequired: True

## EFI_THRLIN_COEF2: Throttle linearisation - Second Order

*Note: This parameter is for advanced users*

Second Order Polynomial Coefficient (=0, if throttle is second order polynomial trendline)

- Range: -1 1

- RebootRequired: True

## EFI_THRLIN_COEF3: Throttle linearisation - Third Order

*Note: This parameter is for advanced users*

Third Order Polynomial Coefficient. (=0, if throttle is third order polynomial trendline)

- Range: -1 1

- RebootRequired: True

## EFI_THRLIN_OFS: throttle linearization offset

*Note: This parameter is for advanced users*

Offset for throttle linearization 

- Range: 0 100

- RebootRequired: True

# EK2 Parameters

## EK2_ENABLE: Enable EKF2

*Note: This parameter is for advanced users*

This enables EKF2. Enabling EKF2 only makes the maths run, it does not mean it will be used for flight control. To use it for flight control set AHRS_EKF_TYPE=2. A reboot or restart will need to be performed after changing the value of EK2_ENABLE for it to take effect.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## EK2_GPS_TYPE: GPS mode control

*Note: This parameter is for advanced users*

This controls use of GPS measurements : 0 = use 3D velocity & 2D position, 1 = use 2D velocity and 2D position, 2 = use 2D position, 3 = Inhibit GPS use - this can be useful when flying with an optical flow sensor in an environment where GPS quality is poor and subject to large multipath errors.

|Value|Meaning|
|:---:|:---:|
|0|GPS 3D Vel and 2D Pos|
|1|GPS 2D vel and 2D pos|
|2|GPS 2D pos|
|3|No GPS|

## EK2_VELNE_M_NSE: GPS horizontal velocity measurement noise (m/s)

*Note: This parameter is for advanced users*

This sets a lower limit on the speed accuracy reported by the GPS receiver that is used to set horizontal velocity observation noise. If the model of receiver used does not provide a speed accurcy estimate, then the parameter value will be used. Increasing it reduces the weighting of the GPS horizontal velocity measurements.

- Range: 0.05 5.0

- Increment: 0.05

- Units: m/s

## EK2_VELD_M_NSE: GPS vertical velocity measurement noise (m/s)

*Note: This parameter is for advanced users*

This sets a lower limit on the speed accuracy reported by the GPS receiver that is used to set vertical velocity observation noise. If the model of receiver used does not provide a speed accurcy estimate, then the parameter value will be used. Increasing it reduces the weighting of the GPS vertical velocity measurements.

- Range: 0.05 5.0

- Increment: 0.05

- Units: m/s

## EK2_VEL_I_GATE: GPS velocity innovation gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the GPS velocity measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_POSNE_M_NSE: GPS horizontal position measurement noise (m)

*Note: This parameter is for advanced users*

This sets the GPS horizontal position observation noise. Increasing it reduces the weighting of GPS horizontal position measurements.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK2_POS_I_GATE: GPS position measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the GPS position measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_GLITCH_RAD: GPS glitch radius gate size (m)

*Note: This parameter is for advanced users*

This controls the maximum radial uncertainty in position between the value predicted by the filter and the value measured by the GPS before the filter position and velocity states are reset to the GPS. Making this value larger allows the filter to ignore larger GPS glitches but also means that non-GPS errors such as IMU and compass can create a larger error in position before the filter is forced back to the GPS position.

- Range: 10 100

- Increment: 5

- Units: m

## EK2_ALT_SOURCE: Primary altitude sensor source

*Note: This parameter is for advanced users*

Primary height sensor used by the EKF. If a sensor other than Baro is selected and becomes unavailable, then the Baro sensor will be used as a fallback. NOTE: The EK2_RNG_USE_HGT parameter can be used to switch to range-finder when close to the ground in conjunction with EK2_ALT_SOURCE = 0 or 2 (Baro or GPS).

|Value|Meaning|
|:---:|:---:|
|0|Use Baro|
|1|Use Range Finder|
|2|Use GPS|
|3|Use Range Beacon|

- RebootRequired: True

## EK2_ALT_M_NSE: Altitude measurement noise (m)

*Note: This parameter is for advanced users*

This is the RMS value of noise in the altitude measurement. Increasing it reduces the weighting of the baro measurement and will make the filter respond more slowly to baro measurement errors, but will make it more sensitive to GPS and accelerometer errors.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK2_HGT_I_GATE: Height measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the height measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_HGT_DELAY: Height measurement delay (msec)

*Note: This parameter is for advanced users*

This is the number of msec that the Height measurements lag behind the inertial measurements.

- Range: 0 250

- Increment: 10

- Units: ms

- RebootRequired: True

## EK2_MAG_M_NSE: Magnetometer measurement noise (Gauss)

*Note: This parameter is for advanced users*

This is the RMS value of noise in magnetometer measurements. Increasing it reduces the weighting on these measurements.

- Range: 0.01 0.5

- Increment: 0.01

- Units: Gauss

## EK2_MAG_CAL: Magnetometer default fusion mode

*Note: This parameter is for advanced users*

This determines when the filter will use the 3-axis magnetometer fusion model that estimates both earth and body fixed magnetic field states, when it will use a simpler magnetic heading fusion model that does not use magnetic field states and when it will use an alternative method of yaw determination to the magnetometer. The 3-axis magnetometer fusion is only suitable for use when the external magnetic field environment is stable. EK2_MAG_CAL = 0 uses heading fusion on ground, 3-axis fusion in-flight, and is the default setting for Plane users. EK2_MAG_CAL = 1 uses 3-axis fusion only when manoeuvring. EK2_MAG_CAL = 2 uses heading fusion at all times, is recommended if the external magnetic field is varying and is the default for rovers. EK2_MAG_CAL = 3 uses heading fusion on the ground and 3-axis fusion after the first in-air field and yaw reset has completed, and is the default for copters. EK2_MAG_CAL = 4 uses 3-axis fusion at all times. NOTE: The fusion mode can be forced to 2 for specific EKF cores using the EK2_MAG_MASK parameter. NOTE: limited operation without a magnetometer or any other yaw sensor is possible by setting all COMPASS_USE, COMPASS_USE2, COMPASS_USE3, etc parameters to 0 with COMPASS_ENABLE set to 1. If this is done, the EK2_GSF_RUN and EK2_GSF_USE masks must be set to the same as EK2_IMU_MASK.

|Value|Meaning|
|:---:|:---:|
|0|When flying|
|1|When manoeuvring|
|2|Never|
|3|After first climb yaw reset|
|4|Always|

## EK2_MAG_I_GATE: Magnetometer measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the magnetometer measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_EAS_M_NSE: Equivalent airspeed measurement noise (m/s)

*Note: This parameter is for advanced users*

This is the RMS value of noise in equivalent airspeed measurements used by planes. Increasing it reduces the weighting of airspeed measurements and will make wind speed estimates less noisy and slower to converge. Increasing also increases navigation errors when dead-reckoning without GPS measurements.

- Range: 0.5 5.0

- Increment: 0.1

- Units: m/s

## EK2_EAS_I_GATE: Airspeed measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the airspeed measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_RNG_M_NSE: Range finder measurement noise (m)

*Note: This parameter is for advanced users*

This is the RMS value of noise in the range finder measurement. Increasing it reduces the weighting on this measurement.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK2_RNG_I_GATE: Range finder measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the range finder innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_MAX_FLOW: Maximum valid optical flow rate

*Note: This parameter is for advanced users*

This sets the magnitude maximum optical flow rate in rad/sec that will be accepted by the filter

- Range: 1.0 4.0

- Increment: 0.1

- Units: rad/s

## EK2_FLOW_M_NSE: Optical flow measurement noise (rad/s)

*Note: This parameter is for advanced users*

This is the RMS value of noise and errors in optical flow measurements. Increasing it reduces the weighting on these measurements.

- Range: 0.05 1.0

- Increment: 0.05

- Units: rad/s

## EK2_FLOW_I_GATE: Optical Flow measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the optical flow innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_FLOW_DELAY: Optical Flow measurement delay (msec)

*Note: This parameter is for advanced users*

This is the number of msec that the optical flow measurements lag behind the inertial measurements. It is the time from the end of the optical flow averaging period and does not include the time delay due to the 100msec of averaging within the flow sensor.

- Range: 0 127

- Increment: 10

- Units: ms

- RebootRequired: True

## EK2_GYRO_P_NSE: Rate gyro noise (rad/s)

*Note: This parameter is for advanced users*

This control disturbance noise controls the growth of estimated error due to gyro measurement errors excluding bias. Increasing it makes the flter trust the gyro measurements less and other measurements more.

- Range: 0.0001 0.1

- Increment: 0.0001

- Units: rad/s

## EK2_ACC_P_NSE: Accelerometer noise (m/s^2)

*Note: This parameter is for advanced users*

This control disturbance noise controls the growth of estimated error due to accelerometer measurement errors excluding bias. Increasing it makes the flter trust the accelerometer measurements less and other measurements more.

- Range: 0.01 1.0

- Increment: 0.01

- Units: m/s/s

## EK2_GBIAS_P_NSE: Rate gyro bias stability (rad/s/s)

*Note: This parameter is for advanced users*

This state  process noise controls growth of the gyro delta angle bias state error estimate. Increasing it makes rate gyro bias estimation faster and noisier.

- Range: 0.00001 0.001

- Units: rad/s/s

## EK2_GSCL_P_NSE: Rate gyro scale factor stability (1/s)

*Note: This parameter is for advanced users*

This noise controls the rate of gyro scale factor learning. Increasing it makes rate gyro scale factor estimation faster and noisier.

- Range: 0.000001 0.001

- Units: Hz

## EK2_ABIAS_P_NSE: Accelerometer bias stability (m/s^3)

*Note: This parameter is for advanced users*

This noise controls the growth of the vertical accelerometer delta velocity bias state error estimate. Increasing it makes accelerometer bias estimation faster and noisier.

- Range: 0.00001 0.005

- Units: m/s/s/s

## EK2_WIND_P_NSE: Wind velocity process noise (m/s^2)

*Note: This parameter is for advanced users*

This state process noise controls the growth of wind state error estimates. Increasing it makes wind estimation faster and noisier.

- Range: 0.01 1.0

- Increment: 0.1

- Units: m/s/s

## EK2_WIND_PSCALE: Height rate to wind process noise scaler

*Note: This parameter is for advanced users*

This controls how much the process noise on the wind states is increased when gaining or losing altitude to take into account changes in wind speed and direction with altitude. Increasing this parameter increases how rapidly the wind states adapt when changing altitude, but does make wind velocity estimation noiser.

- Range: 0.0 1.0

- Increment: 0.1

## EK2_GPS_CHECK: GPS preflight check

*Note: This parameter is for advanced users*

This is a 1 byte bitmap controlling which GPS preflight checks are performed. Set to 0 to bypass all checks. Set to 255 perform all checks. Set to 3 to check just the number of satellites and HDoP. Set to 31 for the most rigorous checks that will still allow checks to pass when the copter is moving, eg launch from a boat.

- Bitmask: 0:NSats,1:HDoP,2:speed error,3:position error,4:yaw error,5:pos drift,6:vert speed,7:horiz speed

## EK2_IMU_MASK: Bitmask of active IMUs

*Note: This parameter is for advanced users*

1 byte bitmap of IMUs to use in EKF2. A separate instance of EKF2 will be started for each IMU selected. Set to 1 to use the first IMU only (default), set to 2 to use the second IMU only, set to 3 to use the first and second IMU. Additional IMU's can be used up to a maximum of 6 if memory and processing resources permit. There may be insufficient memory and processing resources to run multiple instances. If this occurs EKF2 will fail to start.

- Bitmask: 0:FirstIMU,1:SecondIMU,2:ThirdIMU,3:FourthIMU,4:FifthIMU,5:SixthIMU

- RebootRequired: True

## EK2_CHECK_SCALE: GPS accuracy check scaler (%)

*Note: This parameter is for advanced users*

This scales the thresholds that are used to check GPS accuracy before it is used by the EKF. A value of 100 is the default. Values greater than 100 increase and values less than 100 reduce the maximum GPS error the EKF will accept. A value of 200 will double the allowable GPS error.

- Range: 50 200

- Units: %

## EK2_NOAID_M_NSE: Non-GPS operation position uncertainty (m)

*Note: This parameter is for advanced users*

This sets the amount of position variation that the EKF allows for when operating without external measurements (eg GPS or optical flow). Increasing this parameter makes the EKF attitude estimate less sensitive to vehicle manoeuvres but more sensitive to IMU errors.

- Range: 0.5 50.0

- Units: m

## EK2_YAW_M_NSE: Yaw measurement noise (rad)

*Note: This parameter is for advanced users*

This is the RMS value of noise in yaw measurements from the magnetometer. Increasing it reduces the weighting on these measurements.

- Range: 0.05 1.0

- Increment: 0.05

- Units: rad

## EK2_YAW_I_GATE: Yaw measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the magnetometer yaw measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_TAU_OUTPUT: Output complementary filter time constant (centi-sec)

*Note: This parameter is for advanced users*

Sets the time constant of the output complementary filter/predictor in centi-seconds.

- Range: 10 50

- Increment: 5

- Units: cs

## EK2_MAGE_P_NSE: Earth magnetic field process noise (gauss/s)

*Note: This parameter is for advanced users*

This state process noise controls the growth of earth magnetic field state error estimates. Increasing it makes earth magnetic field estimation faster and noisier.

- Range: 0.00001 0.01

- Units: Gauss/s

## EK2_MAGB_P_NSE: Body magnetic field process noise (gauss/s)

*Note: This parameter is for advanced users*

This state process noise controls the growth of body magnetic field state error estimates. Increasing it makes magnetometer bias error estimation faster and noisier.

- Range: 0.00001 0.01

- Units: Gauss/s

## EK2_RNG_USE_HGT: Range finder switch height percentage

*Note: This parameter is for advanced users*

Range finder can be used as the primary height source when below this percentage of its maximum range (see RNGFND_MAX_CM). This will not work unless Baro or GPS height is selected as the primary height source vis EK2_ALT_SOURCE = 0 or 2 respectively.  This feature should not be used for terrain following as it is designed  for vertical takeoff and landing with climb above  the range finder use height before commencing the mission, and with horizontal position changes below that height being limited to a flat region around the takeoff and landing point.

- Range: -1 70

- Increment: 1

- Units: %

## EK2_TERR_GRAD: Maximum terrain gradient

*Note: This parameter is for advanced users*

Specifies the maximum gradient of the terrain below the vehicle assumed when it is fusing range finder or optical flow to estimate terrain height.

- Range: 0 0.2

- Increment: 0.01

## EK2_BCN_M_NSE: Range beacon measurement noise (m)

*Note: This parameter is for advanced users*

This is the RMS value of noise in the range beacon measurement. Increasing it reduces the weighting on this measurement.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK2_BCN_I_GTE: Range beacon measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the range beacon measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK2_BCN_DELAY: Range beacon measurement delay (msec)

*Note: This parameter is for advanced users*

This is the number of msec that the range beacon measurements lag behind the inertial measurements. It is the time from the end of the optical flow averaging period and does not include the time delay due to the 100msec of averaging within the flow sensor.

- Range: 0 127

- Increment: 10

- Units: ms

- RebootRequired: True

## EK2_RNG_USE_SPD: Range finder max ground speed

*Note: This parameter is for advanced users*

The range finder will not be used as the primary height source when the horizontal ground speed is greater than this value.

- Range: 2.0 6.0

- Increment: 0.5

- Units: m/s

## EK2_MAG_MASK: Bitmask of active EKF cores that will always use heading fusion

*Note: This parameter is for advanced users*

1 byte bitmap of EKF cores that will disable magnetic field states and use simple magnetic heading fusion at all times. This parameter enables specified cores to be used as a backup for flight into an environment with high levels of external magnetic interference which may degrade the EKF attitude estimate when using 3-axis magnetometer fusion. NOTE : Use of a different magnetometer fusion algorithm on different cores makes unwanted EKF core switches due to magnetometer errors more likely.

- Bitmask: 0:FirstEKF,1:SecondEKF,2:ThirdEKF,3:FourthEKF,4:FifthEKF,5:SixthEKF

- RebootRequired: True

## EK2_OGN_HGT_MASK: Bitmask control of EKF reference height correction

*Note: This parameter is for advanced users*

When a height sensor other than GPS is used as the primary height source by the EKF, the position of the zero height datum is defined by that sensor and its frame of reference. If a GPS height measurement is also available, then the height of the WGS-84 height datum used by the EKF can be corrected so that the height returned by the getLLH() function is compensated for primary height sensor drift and change in datum over time. The first two bit positions control when the height datum will be corrected. Correction is performed using a Bayes filter and only operates when GPS quality permits. The third bit position controls where the corrections to the GPS reference datum are applied. Corrections can be applied to the local vertical position or to the reported EKF origin height (default).

- Bitmask: 0:Correct when using Baro height,1:Correct when using range finder height,2:Apply corrections to local position

- RebootRequired: True

## EK2_FLOW_USE: Optical flow use bitmask

*Note: This parameter is for advanced users*

Controls if the optical flow data is fused into the 24-state navigation estimator OR the 1-state terrain height estimator.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Navigation|
|2|Terrain|

- RebootRequired: True

## EK2_MAG_EF_LIM: EarthField error limit

*Note: This parameter is for advanced users*

This limits the difference between the learned earth magnetic field and the earth field from the world magnetic model tables. A value of zero means to disable the use of the WMM tables.

- Range: 0 500

- Units: mGauss

## EK2_HRT_FILT: Height rate filter crossover frequency

Specifies the crossover frequency of the complementary filter used to calculate the output predictor height rate derivative.

- Range: 0.1 30.0

- Units: Hz

## EK2_GSF_RUN_MASK: Bitmask of which EKF-GSF yaw estimators run

*Note: This parameter is for advanced users*

A bitmask of which EKF2 instances run an independant EKF-GSF yaw estimator to provide a backup yaw estimate that doesn't rely on magnetometer data. This estimator uses IMU, GPS and, if available, airspeed data. EKF-GSF yaw estimator data for the primary EKF2 instance will be logged as GSF0 and GSF1 messages. Use of the yaw estimate generated by this algorithm is controlled by the EK2_GSF_USE_MASK and EK2_GSF_RST_MAX parameters. To run the EKF-GSF yaw estimator in ride-along and logging only, set EK2_GSF_USE_MASK to 0. 

- Bitmask: 0:FirstEKF,1:SecondEKF,2:ThirdEKF,3:FourthEKF,4:FifthEKF,5:SixthEKF

- RebootRequired: True

## EK2_GSF_USE_MASK: Bitmask of which EKF-GSF yaw estimators are used

*Note: This parameter is for advanced users*

1 byte bitmap of which EKF2 instances will use the output from the EKF-GSF yaw estimator that has been turned on by the EK2_GSF_RUN_MASK parameter. If the inertial navigation calculation stops following the GPS, then the vehicle code can request EKF2 to attempt to resolve the issue, either by performing a yaw reset if enabled by this parameter by switching to another EKF2 instance.

- Bitmask: 0:FirstEKF,1:SecondEKF,2:ThirdEKF,3:FourthEKF,4:FifthEKF,5:SixthEKF

- RebootRequired: True

## EK2_GSF_RST_MAX: Maximum number of resets to the EKF-GSF yaw estimate allowed

*Note: This parameter is for advanced users*

Sets the maximum number of times the EKF2 will be allowed to reset its yaw to the estimate from the EKF-GSF yaw estimator. No resets will be allowed unless the use of the EKF-GSF yaw estimate is enabled via the EK2_GSF_USE_MASK parameter.

- Range: 1 10

- Increment: 1

- RebootRequired: True

## EK2_OPTIONS: Optional EKF behaviour

*Note: This parameter is for advanced users*

optional EKF2 behaviour. Disabling external navigation prevents use of external vision data in the EKF2 solution

- Bitmask: 0:DisableExternalNavigation

# EK3 Parameters

## EK3_ENABLE: Enable EKF3

*Note: This parameter is for advanced users*

This enables EKF3. Enabling EKF3 only makes the maths run, it does not mean it will be used for flight control. To use it for flight control set AHRS_EKF_TYPE=3. A reboot or restart will need to be performed after changing the value of EK3_ENABLE for it to take effect.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## EK3_VELNE_M_NSE: GPS horizontal velocity measurement noise (m/s)

*Note: This parameter is for advanced users*

This sets a lower limit on the speed accuracy reported by the GPS receiver that is used to set horizontal velocity observation noise. If the model of receiver used does not provide a speed accurcy estimate, then the parameter value will be used. Increasing it reduces the weighting of the GPS horizontal velocity measurements.

- Range: 0.05 5.0

- Increment: 0.05

- Units: m/s

## EK3_VELD_M_NSE: GPS vertical velocity measurement noise (m/s)

*Note: This parameter is for advanced users*

This sets a lower limit on the speed accuracy reported by the GPS receiver that is used to set vertical velocity observation noise. If the model of receiver used does not provide a speed accurcy estimate, then the parameter value will be used. Increasing it reduces the weighting of the GPS vertical velocity measurements.

- Range: 0.05 5.0

- Increment: 0.05

- Units: m/s

## EK3_VEL_I_GATE: GPS velocity innovation gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the GPS velocity measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted. If EK3_GLITCH_RAD set to 0 the velocity innovations will be clipped instead of rejected if they exceed the gate size and a smaller value of EK3_VEL_I_GATE not exceeding 300 is recommended to limit the effect of GPS transient errors.

- Range: 100 1000

- Increment: 25

## EK3_POSNE_M_NSE: GPS horizontal position measurement noise (m)

*Note: This parameter is for advanced users*

This sets the GPS horizontal position observation noise. Increasing it reduces the weighting of GPS horizontal position measurements.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK3_POS_I_GATE: GPS position measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the GPS position measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted. If EK3_GLITCH_RAD has been set to 0 the horizontal position innovations will be clipped instead of rejected if they exceed the gate size so a smaller value of EK3_POS_I_GATE not exceeding 300 is recommended to limit the effect of GPS transient errors.

- Range: 100 1000

- Increment: 25

## EK3_GLITCH_RAD: GPS glitch radius gate size (m)

*Note: This parameter is for advanced users*

This controls the maximum radial uncertainty in position between the value predicted by the filter and the value measured by the GPS before the filter position and velocity states are reset to the GPS. Making this value larger allows the filter to ignore larger GPS glitches but also means that non-GPS errors such as IMU and compass can create a larger error in position before the filter is forced back to the GPS position. If EK3_GLITCH_RAD set to 0 the GPS innovations will be clipped instead of rejected if they exceed the gate size set by EK3_VEL_I_GATE and EK3_POS_I_GATE which can be useful if poor quality sensor data is causing GPS rejection and loss of navigation but does make the EKF more susceptible to GPS glitches. If setting EK3_GLITCH_RAD to 0 it is recommended to reduce EK3_VEL_I_GATE and EK3_POS_I_GATE to 300.

- Range: 10 100

- Increment: 5

- Units: m

## EK3_ALT_M_NSE: Altitude measurement noise (m)

*Note: This parameter is for advanced users*

This is the RMS value of noise in the altitude measurement. Increasing it reduces the weighting of the baro measurement and will make the filter respond more slowly to baro measurement errors, but will make it more sensitive to GPS and accelerometer errors. A larger value for EK3_ALT_M_NSE may be required when operating with EK3_SRCx_POSZ = 0. This parameter also sets the noise for the 'synthetic' zero height measurement that is used when EK3_SRCx_POSZ = 0.

- Range: 0.1 100.0

- Increment: 0.1

- Units: m

## EK3_HGT_I_GATE: Height measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the height measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.  If EK3_GLITCH_RAD set to 0 the vertical position innovations will be clipped instead of rejected if they exceed the gate size and a smaller value of EK3_HGT_I_GATE not exceeding 300 is recommended to limit the effect of height sensor transient errors.

- Range: 100 1000

- Increment: 25

## EK3_HGT_DELAY: Height measurement delay (msec)

*Note: This parameter is for advanced users*

This is the number of msec that the Height measurements lag behind the inertial measurements.

- Range: 0 250

- Increment: 10

- Units: ms

- RebootRequired: True

## EK3_MAG_M_NSE: Magnetometer measurement noise (Gauss)

*Note: This parameter is for advanced users*

This is the RMS value of noise in magnetometer measurements. Increasing it reduces the weighting on these measurements.

- Range: 0.01 0.5

- Increment: 0.01

- Units: Gauss

## EK3_MAG_CAL: Magnetometer default fusion mode

*Note: This parameter is for advanced users*

This determines when the filter will use the 3-axis magnetometer fusion model that estimates both earth and body fixed magnetic field states and when it will use a simpler magnetic heading fusion model that does not use magnetic field states. The 3-axis magnetometer fusion is only suitable for use when the external magnetic field environment is stable. EK3_MAG_CAL = 0 uses heading fusion on ground, 3-axis fusion in-flight, and is the default setting for Plane users. EK3_MAG_CAL = 1 uses 3-axis fusion only when manoeuvring. EK3_MAG_CAL = 2 uses heading fusion at all times, is recommended if the external magnetic field is varying and is the default for rovers. EK3_MAG_CAL = 3 uses heading fusion on the ground and 3-axis fusion after the first in-air field and yaw reset has completed, and is the default for copters. EK3_MAG_CAL = 4 uses 3-axis fusion at all times. EK3_MAG_CAL = 5 uses an external yaw sensor with simple heading fusion. NOTE : Use of simple heading magnetometer fusion makes vehicle compass calibration and alignment errors harder for the EKF to detect which reduces the sensitivity of the Copter EKF failsafe algorithm. NOTE: The fusion mode can be forced to 2 for specific EKF cores using the EK3_MAG_MASK parameter. EK3_MAG_CAL = 6 uses an external yaw sensor with fallback to compass when the external sensor is not available if we are flying. NOTE: The fusion mode can be forced to 2 for specific EKF cores using the EK3_MAG_MASK parameter. NOTE: limited operation without a magnetometer or any other yaw sensor is possible by setting all COMPASS_USE, COMPASS_USE2, COMPASS_USE3, etc parameters to 0 and setting COMPASS_ENABLE to 0. If this is done, the EK3_GSF_RUN and EK3_GSF_USE masks must be set to the same as EK3_IMU_MASK. A yaw angle derived from IMU and GPS velocity data using a Gaussian Sum Filter (GSF) will then be used to align the yaw when flight commences and there is sufficient movement.

|Value|Meaning|
|:---:|:---:|
|0|When flying|
|1|When manoeuvring|
|2|Never|
|3|After first climb yaw reset|
|4|Always|
|5|Use external yaw sensor (Deprecated in 4.1+ see EK3_SRCn_YAW)|
|6|External yaw sensor with compass fallback (Deprecated in 4.1+ see EK3_SRCn_YAW)|

- RebootRequired: True

## EK3_MAG_I_GATE: Magnetometer measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the magnetometer measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK3_EAS_M_NSE: Equivalent airspeed measurement noise (m/s)

*Note: This parameter is for advanced users*

This is the RMS value of noise in equivalent airspeed measurements used by planes. Increasing it reduces the weighting of airspeed measurements and will make wind speed estimates less noisy and slower to converge. Increasing also increases navigation errors when dead-reckoning without GPS measurements.

- Range: 0.5 5.0

- Increment: 0.1

- Units: m/s

## EK3_EAS_I_GATE: Airspeed measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the airspeed measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK3_RNG_M_NSE: Range finder measurement noise (m)

*Note: This parameter is for advanced users*

This is the RMS value of noise in the range finder measurement. Increasing it reduces the weighting on this measurement.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK3_RNG_I_GATE: Range finder measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the range finder innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK3_MAX_FLOW: Maximum valid optical flow rate

*Note: This parameter is for advanced users*

This sets the magnitude maximum optical flow rate in rad/sec that will be accepted by the filter

- Range: 1.0 4.0

- Increment: 0.1

- Units: rad/s

## EK3_FLOW_M_NSE: Optical flow measurement noise (rad/s)

*Note: This parameter is for advanced users*

This is the RMS value of noise and errors in optical flow measurements. Increasing it reduces the weighting on these measurements.

- Range: 0.05 1.0

- Increment: 0.05

- Units: rad/s

## EK3_FLOW_I_GATE: Optical Flow measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the optical flow innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK3_FLOW_DELAY: Optical Flow measurement delay (msec)

*Note: This parameter is for advanced users*

This is the number of msec that the optical flow measurements lag behind the inertial measurements. It is the time from the end of the optical flow averaging period and does not include the time delay due to the 100msec of averaging within the flow sensor.

- Range: 0 250

- Increment: 10

- Units: ms

- RebootRequired: True

## EK3_GYRO_P_NSE: Rate gyro noise (rad/s)

*Note: This parameter is for advanced users*

This control disturbance noise controls the growth of estimated error due to gyro measurement errors excluding bias. Increasing it makes the flter trust the gyro measurements less and other measurements more.

- Range: 0.0001 0.1

- Increment: 0.0001

- Units: rad/s

## EK3_ACC_P_NSE: Accelerometer noise (m/s^2)

*Note: This parameter is for advanced users*

This control disturbance noise controls the growth of estimated error due to accelerometer measurement errors excluding bias. Increasing it makes the flter trust the accelerometer measurements less and other measurements more.

- Range: 0.01 1.0

- Increment: 0.01

- Units: m/s/s

## EK3_GBIAS_P_NSE: Rate gyro bias stability (rad/s/s)

*Note: This parameter is for advanced users*

This state  process noise controls growth of the gyro delta angle bias state error estimate. Increasing it makes rate gyro bias estimation faster and noisier.

- Range: 0.00001 0.001

- Units: rad/s/s

## EK3_ABIAS_P_NSE: Accelerometer bias stability (m/s^3)

*Note: This parameter is for advanced users*

This noise controls the growth of the vertical accelerometer delta velocity bias state error estimate. Increasing it makes accelerometer bias estimation faster and noisier.

- Range: 0.00001 0.02

- Units: m/s/s/s

## EK3_WIND_P_NSE: Wind velocity process noise (m/s^2)

*Note: This parameter is for advanced users*

This state process noise controls the growth of wind state error estimates. Increasing it makes wind estimation faster and noisier.

- Range: 0.01 2.0

- Increment: 0.1

- Units: m/s/s

## EK3_WIND_PSCALE: Height rate to wind process noise scaler

*Note: This parameter is for advanced users*

This controls how much the process noise on the wind states is increased when gaining or losing altitude to take into account changes in wind speed and direction with altitude. Increasing this parameter increases how rapidly the wind states adapt when changing altitude, but does make wind velocity estimation noiser.

- Range: 0.0 2.0

- Increment: 0.1

## EK3_GPS_CHECK: GPS preflight check

*Note: This parameter is for advanced users*

This is a 1 byte bitmap controlling which GPS preflight checks are performed. Set to 0 to bypass all checks. Set to 255 perform all checks. Set to 3 to check just the number of satellites and HDoP. Set to 31 for the most rigorous checks that will still allow checks to pass when the copter is moving, eg launch from a boat.

- Bitmask: 0:NSats,1:HDoP,2:speed error,3:position error,4:yaw error,5:pos drift,6:vert speed,7:horiz speed

## EK3_IMU_MASK: Bitmask of active IMUs

*Note: This parameter is for advanced users*

1 byte bitmap of IMUs to use in EKF3. A separate instance of EKF3 will be started for each IMU selected. Set to 1 to use the first IMU only (default), set to 2 to use the second IMU only, set to 3 to use the first and second IMU. Additional IMU's can be used up to a maximum of 6 if memory and processing resources permit. There may be insufficient memory and processing resources to run multiple instances. If this occurs EKF3 will fail to start.

- Bitmask: 0:FirstIMU,1:SecondIMU,2:ThirdIMU,3:FourthIMU,4:FifthIMU,5:SixthIMU

- RebootRequired: True

## EK3_CHECK_SCALE: GPS accuracy check scaler (%)

*Note: This parameter is for advanced users*

This scales the thresholds that are used to check GPS accuracy before it is used by the EKF. A value of 100 is the default. Values greater than 100 increase and values less than 100 reduce the maximum GPS error the EKF will accept. A value of 200 will double the allowable GPS error.

- Range: 50 200

- Units: %

## EK3_NOAID_M_NSE: Non-GPS operation position uncertainty (m)

*Note: This parameter is for advanced users*

This sets the amount of position variation that the EKF allows for when operating without external measurements (eg GPS or optical flow). Increasing this parameter makes the EKF attitude estimate less sensitive to vehicle manoeuvres but more sensitive to IMU errors.

- Range: 0.5 50.0

- Units: m

## EK3_BETA_MASK: Bitmask controlling sidelip angle fusion

*Note: This parameter is for advanced users*

1 byte bitmap controlling use of sideslip angle fusion for estimation of non wind states during operation of 'fly forward' vehicle types such as fixed wing planes. By assuming that the angle of sideslip is small, the wind velocity state estimates are corrected  whenever the EKF is not dead reckoning (e.g. has an independent velocity or position sensor such as GPS). This behaviour is on by default and cannot be disabled. When the EKF is dead reckoning, the wind states are used as a reference, enabling use of the small angle of sideslip assumption to correct non wind velocity states (eg attitude, velocity, position, etc) and improve navigation accuracy. This behaviour is on by default and cannot be disabled. The behaviour controlled by this parameter is the use of the small angle of sideslip assumption to correct non wind velocity states when the EKF is NOT dead reckoning. This is primarily of benefit to reduce the buildup of yaw angle errors during straight and level flight without a yaw sensor (e.g. magnetometer or dual antenna GPS yaw) provided aerobatic flight maneuvers with large sideslip angles are not performed. The 'always' option might be used where the yaw sensor is intentionally not fitted or disabled. The 'WhenNoYawSensor' option might be used if a yaw sensor is fitted, but protection against in-flight failure and continual rejection by the EKF is desired. For vehicles operated within visual range of the operator performing frequent turning maneuvers, setting this parameter is unnecessary.

- Bitmask: 0:Always,1:WhenNoYawSensor

- RebootRequired: True

## EK3_YAW_M_NSE: Yaw measurement noise (rad)

*Note: This parameter is for advanced users*

This is the RMS value of noise in yaw measurements from the magnetometer. Increasing it reduces the weighting on these measurements.

- Range: 0.05 1.0

- Increment: 0.05

- Units: rad

## EK3_YAW_I_GATE: Yaw measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the magnetometer yaw measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK3_TAU_OUTPUT: Output complementary filter time constant (centi-sec)

*Note: This parameter is for advanced users*

Sets the time constant of the output complementary filter/predictor in centi-seconds.

- Range: 10 50

- Increment: 5

- Units: cs

## EK3_MAGE_P_NSE: Earth magnetic field process noise (gauss/s)

*Note: This parameter is for advanced users*

This state process noise controls the growth of earth magnetic field state error estimates. Increasing it makes earth magnetic field estimation faster and noisier.

- Range: 0.00001 0.01

- Units: Gauss/s

## EK3_MAGB_P_NSE: Body magnetic field process noise (gauss/s)

*Note: This parameter is for advanced users*

This state process noise controls the growth of body magnetic field state error estimates. Increasing it makes magnetometer bias error estimation faster and noisier.

- Range: 0.00001 0.01

- Units: Gauss/s

## EK3_RNG_USE_HGT: Range finder switch height percentage

*Note: This parameter is for advanced users*

Range finder can be used as the primary height source when below this percentage of its maximum range (see RNGFNDx_MAX_CM) and the primary height source is Baro or GPS (see EK3_SRCx_POSZ).  This feature should not be used for terrain following as it is designed for vertical takeoff and landing with climb above the range finder use height before commencing the mission, and with horizontal position changes below that height being limited to a flat region around the takeoff and landing point.

- Range: -1 70

- Increment: 1

- Units: %

## EK3_TERR_GRAD: Maximum terrain gradient

*Note: This parameter is for advanced users*

Specifies the maximum gradient of the terrain below the vehicle when it is using range finder as a height reference

- Range: 0 0.2

- Increment: 0.01

## EK3_BCN_M_NSE: Range beacon measurement noise (m)

*Note: This parameter is for advanced users*

This is the RMS value of noise in the range beacon measurement. Increasing it reduces the weighting on this measurement.

- Range: 0.1 10.0

- Increment: 0.1

- Units: m

## EK3_BCN_I_GTE: Range beacon measurement gate size

*Note: This parameter is for advanced users*

This sets the percentage number of standard deviations applied to the range beacon measurement innovation consistency check. Decreasing it makes it more likely that good measurements will be rejected. Increasing it makes it more likely that bad measurements will be accepted.

- Range: 100 1000

- Increment: 25

## EK3_BCN_DELAY: Range beacon measurement delay (msec)

*Note: This parameter is for advanced users*

This is the number of msec that the range beacon measurements lag behind the inertial measurements.

- Range: 0 250

- Increment: 10

- Units: ms

- RebootRequired: True

## EK3_RNG_USE_SPD: Range finder max ground speed

*Note: This parameter is for advanced users*

The range finder will not be used as the primary height source when the horizontal ground speed is greater than this value.

- Range: 2.0 6.0

- Increment: 0.5

- Units: m/s

## EK3_ACC_BIAS_LIM: Accelerometer bias limit

*Note: This parameter is for advanced users*

The accelerometer bias state will be limited to +- this value

- Range: 0.5 2.5

- Increment: 0.1

- Units: m/s/s

## EK3_MAG_MASK: Bitmask of active EKF cores that will always use heading fusion

*Note: This parameter is for advanced users*

1 byte bitmap of EKF cores that will disable magnetic field states and use simple magnetic heading fusion at all times. This parameter enables specified cores to be used as a backup for flight into an environment with high levels of external magnetic interference which may degrade the EKF attitude estimate when using 3-axis magnetometer fusion. NOTE : Use of a different magnetometer fusion algorithm on different cores makes unwanted EKF core switches due to magnetometer errors more likely.

- Bitmask: 0:FirstEKF,1:SecondEKF,2:ThirdEKF,3:FourthEKF,4:FifthEKF,5:SixthEKF

- RebootRequired: True

## EK3_OGN_HGT_MASK: Bitmask control of EKF reference height correction

*Note: This parameter is for advanced users*

When a height sensor other than GPS is used as the primary height source by the EKF, the position of the zero height datum is defined by that sensor and its frame of reference. If a GPS height measurement is also available, then the height of the WGS-84 height datum used by the EKF can be corrected so that the height returned by the getLLH() function is compensated for primary height sensor drift and change in datum over time. The first two bit positions control when the height datum will be corrected. Correction is performed using a Bayes filter and only operates when GPS quality permits. The third bit position controls where the corrections to the GPS reference datum are applied. Corrections can be applied to the local vertical position or to the reported EKF origin height (default).

- Bitmask: 0:Correct when using Baro height,1:Correct when using range finder height,2:Apply corrections to local position

- RebootRequired: True

## EK3_VIS_VERR_MIN: Visual odometry minimum velocity error

*Note: This parameter is for advanced users*

This is the 1-STD odometry velocity observation error that will be assumed when maximum quality is reported by the sensor. When quality is between max and min, the error will be calculated using linear interpolation between VIS_VERR_MIN and VIS_VERR_MAX.

- Range: 0.05 0.5

- Increment: 0.05

- Units: m/s

## EK3_VIS_VERR_MAX: Visual odometry maximum velocity error

*Note: This parameter is for advanced users*

This is the 1-STD odometry velocity observation error that will be assumed when minimum quality is reported by the sensor. When quality is between max and min, the error will be calculated using linear interpolation between VIS_VERR_MIN and VIS_VERR_MAX.

- Range: 0.5 5.0

- Increment: 0.1

- Units: m/s

## EK3_WENC_VERR: Wheel odometry velocity error

*Note: This parameter is for advanced users*

This is the 1-STD odometry velocity observation error that will be assumed when wheel encoder data is being fused.

- Range: 0.01 1.0

- Increment: 0.1

- Units: m/s

## EK3_FLOW_USE: Optical flow use bitmask

*Note: This parameter is for advanced users*

Controls if the optical flow data is fused into the 24-state navigation estimator OR the 1-state terrain height estimator.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Navigation|
|2|Terrain|

- RebootRequired: True

## EK3_HRT_FILT: Height rate filter crossover frequency

Specifies the crossover frequency of the complementary filter used to calculate the output predictor height rate derivative.

- Range: 0.1 30.0

- Units: Hz

## EK3_MAG_EF_LIM: EarthField error limit

*Note: This parameter is for advanced users*

This limits the difference between the learned earth magnetic field and the earth field from the world magnetic model tables. A value of zero means to disable the use of the WMM tables.

- Range: 0 500

- Units: mGauss

## EK3_GSF_RUN_MASK: Bitmask of which EKF-GSF yaw estimators run

*Note: This parameter is for advanced users*

1 byte bitmap of which EKF3 instances run an independant EKF-GSF yaw estimator to provide a backup yaw estimate that doesn't rely on magnetometer data. This estimator uses IMU, GPS and, if available, airspeed data. EKF-GSF yaw estimator data for the primary EKF3 instance will be logged as GSF0 and GSF1 messages. Use of the yaw estimate generated by this algorithm is controlled by the EK3_GSF_USE_MASK and EK3_GSF_RST_MAX parameters. To run the EKF-GSF yaw estimator in ride-along and logging only, set EK3_GSF_USE to 0. 

- Bitmask: 0:FirstEKF,1:SecondEKF,2:ThirdEKF,3:FourthEKF,4:FifthEKF,5:SixthEKF

- RebootRequired: True

## EK3_GSF_USE_MASK: Bitmask of which EKF-GSF yaw estimators are used

*Note: This parameter is for advanced users*

A bitmask of which EKF3 instances will use the output from the EKF-GSF yaw estimator that has been turned on by the EK3_GSF_RUN_MASK parameter. If the inertial navigation calculation stops following the GPS, then the vehicle code can request EKF3 to attempt to resolve the issue, either by performing a yaw reset if enabled by this parameter by switching to another EKF3 instance.

- Bitmask: 0:FirstEKF,1:SecondEKF,2:ThirdEKF,3:FourthEKF,4:FifthEKF,5:SixthEKF

- RebootRequired: True

## EK3_GSF_RST_MAX: Maximum number of resets to the EKF-GSF yaw estimate allowed

*Note: This parameter is for advanced users*

Sets the maximum number of times the EKF3 will be allowed to reset its yaw to the estimate from the EKF-GSF yaw estimator. No resets will be allowed unless the use of the EKF-GSF yaw estimate is enabled via the EK3_GSF_USE_MASK parameter.

- Range: 1 10

- Increment: 1

- RebootRequired: True

## EK3_ERR_THRESH: EKF3 Lane Relative Error Sensitivity Threshold

*Note: This parameter is for advanced users*

lanes have to be consistently better than the primary by at least this threshold to reduce their overall relativeCoreError, lowering this makes lane switching more sensitive to smaller error differences

- Range: 0.05 1

- Increment: 0.05

## EK3_AFFINITY: EKF3 Sensor Affinity Options

*Note: This parameter is for advanced users*

These options control the affinity between sensor instances and EKF cores

- Bitmask: 0:EnableGPSAffinity,1:EnableBaroAffinity,2:EnableCompassAffinity,3:EnableAirspeedAffinity

- RebootRequired: True

## EK3_DRAG_BCOEF_X: Ballistic coefficient for X axis drag

*Note: This parameter is for advanced users*

Ratio of mass to drag coefficient measured along the X body axis. This parameter enables estimation of wind drift for vehicles with bluff bodies and without propulsion forces in the X and Y direction (eg multicopters). The drag produced by this effect scales with speed squared.  Set to a postive value > 1.0 to enable. A starting value is the mass in Kg divided by the frontal area. The predicted drag from the rotors is specified separately by the EK3_DRAG_MCOEF parameter.

- Range: 0.0 1000.0

- Units: kg/m/m

## EK3_DRAG_BCOEF_Y: Ballistic coefficient for Y axis drag

*Note: This parameter is for advanced users*

Ratio of mass to drag coefficient measured along the Y body axis. This parameter enables estimation of wind drift for vehicles with bluff bodies and without propulsion forces in the X and Y direction (eg multicopters). The drag produced by this effect scales with speed squared.  Set to a postive value > 1.0 to enable. A starting value is the mass in Kg divided by the side area. The predicted drag from the rotors is specified separately by the EK3_DRAG_MCOEF parameter.

- Range: 50.0 1000.0

- Units: kg/m/m

## EK3_DRAG_M_NSE: Observation noise for drag acceleration

*Note: This parameter is for advanced users*

This sets the amount of noise used when fusing X and Y acceleration as an observation that enables esitmation of wind velocity for multi-rotor vehicles. This feature is enabled by the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters

- Range: 0.1 2.0

- Increment: 0.1

- Units: m/s/s

## EK3_DRAG_MCOEF: Momentum coefficient for propeller drag

*Note: This parameter is for advanced users*

This parameter is used to predict the drag produced by the rotors when flying a multi-copter, enabling estimation of wind drift. The drag produced by this effect scales with speed not speed squared and is produced because some of the air velocity normal to the rotors axis of rotation is lost when passing through the rotor disc which changes the momentum of the airflow causing drag. For unducted rotors the effect is roughly proportional to the area of the propeller blades when viewed side on and changes with different propellers. It is higher for ducted rotors. For example if flying at 15 m/s at sea level conditions produces a rotor induced drag acceleration of 1.5 m/s/s, then EK3_DRAG_MCOEF would be set to 0.1 = (1.5/15.0). Set EK3_MCOEF to a postive value to enable wind estimation using this drag effect. To account for the drag produced by the body which scales with speed squared, see documentation for the EK3_DRAG_BCOEF_X and EK3_DRAG_BCOEF_Y parameters.

- Range: 0.0 1.0

- Increment: 0.01

- Units: 1/s

## EK3_OGNM_TEST_SF: On ground not moving test scale factor

*Note: This parameter is for advanced users*

This parameter is adjust the sensitivity of the on ground not moving test which is used to assist with learning the yaw gyro bias and stopping yaw drift before flight when operating without a yaw sensor. Bigger values allow the detection of a not moving condition with noiser IMU data. Check the XKFM data logged when the vehicle is on ground not moving and adjust the value of OGNM_TEST_SF to be slightly higher than the maximum value of the XKFM.ADR, XKFM.ALR, XKFM.GDR and XKFM.GLR test levels.

- Range: 1.0 10.0

- Increment: 0.5

## EK3_GND_EFF_DZ: Baro height ground effect dead zone

*Note: This parameter is for advanced users*

This parameter sets the size of the dead zone that is applied to negative baro height spikes that can occur when taking off or landing when a vehicle with lift rotors is operating in ground effect ground effect. Set to about 0.5m less than the amount of negative offset in baro height that occurs just prior to takeoff when lift motors are spooling up. Set to 0 if no ground effect is present.

- Range: 0.0 10.0

- Increment: 0.5

## EK3_PRIMARY: Primary core number

*Note: This parameter is for advanced users*

The core number (index in IMU mask) that will be used as the primary EKF core on startup. While disarmed the EKF will force the use of this core. A value of 0 corresponds to the first IMU in EK3_IMU_MASK.

- Range: 0 2

- Increment: 1

## EK3_LOG_LEVEL: Logging Level

*Note: This parameter is for advanced users*

Determines how verbose the EKF3 streaming logging is. A value of 0 provides full logging(default), a value of 1 only XKF4 scaled innovations are logged, a value of 2 both XKF4 and GSF are logged, and a value of 3 disables all streaming logging of EKF3.

- Range: 0 3

- Increment: 1

## EK3_GPS_VACC_MAX: GPS vertical accuracy threshold

*Note: This parameter is for advanced users*

Vertical accuracy threshold for GPS as the altitude source. The GPS will not be used as an altitude source if the reported vertical accuracy of the GPS is larger than this threshold, falling back to baro instead. Set to zero to deactivate the threshold check.

- Range: 0.0 10.0

- Increment: 0.1

- Units: m

## EK3_OPTIONS: Optional EKF behaviour

*Note: This parameter is for advanced users*

This controls optional EKF behaviour. Setting JammingExpected will change the EKF nehaviour such that if dead reckoning navigation is possible it will require the preflight alignment GPS quality checks controlled by EK3_GPS_CHECK and EK3_CHECK_SCALE to pass before resuming GPS use if GPS lock is lost for more than 2 seconds to prevent bad

- Bitmask: 0:JammingExpected

# EK3SRC Parameters

## EK3_SRC1_POSXY: Position Horizontal Source (Primary)

*Note: This parameter is for advanced users*

Position Horizontal Source (Primary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC1_VELXY: Velocity Horizontal Source

*Note: This parameter is for advanced users*

Velocity Horizontal Source

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|5|OpticalFlow|
|6|ExternalNav|
|7|WheelEncoder|

## EK3_SRC1_POSZ: Position Vertical Source

*Note: This parameter is for advanced users*

Position Vertical Source

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Baro|
|2|RangeFinder|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC1_VELZ: Velocity Vertical Source

*Note: This parameter is for advanced users*

Velocity Vertical Source

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC1_YAW: Yaw Source

*Note: This parameter is for advanced users*

Yaw Source

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Compass|
|2|GPS|
|3|GPS with Compass Fallback|
|6|ExternalNav|
|8|GSF|

## EK3_SRC2_POSXY: Position Horizontal Source (Secondary)

*Note: This parameter is for advanced users*

Position Horizontal Source (Secondary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC2_VELXY: Velocity Horizontal Source (Secondary)

*Note: This parameter is for advanced users*

Velocity Horizontal Source (Secondary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|5|OpticalFlow|
|6|ExternalNav|
|7|WheelEncoder|

## EK3_SRC2_POSZ: Position Vertical Source (Secondary)

*Note: This parameter is for advanced users*

Position Vertical Source (Secondary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Baro|
|2|RangeFinder|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC2_VELZ: Velocity Vertical Source (Secondary)

*Note: This parameter is for advanced users*

Velocity Vertical Source (Secondary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC2_YAW: Yaw Source (Secondary)

*Note: This parameter is for advanced users*

Yaw Source (Secondary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Compass|
|2|GPS|
|3|GPS with Compass Fallback|
|6|ExternalNav|
|8|GSF|

## EK3_SRC3_POSXY: Position Horizontal Source (Tertiary)

*Note: This parameter is for advanced users*

Position Horizontal Source (Tertiary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC3_VELXY: Velocity Horizontal Source (Tertiary)

*Note: This parameter is for advanced users*

Velocity Horizontal Source (Tertiary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|5|OpticalFlow|
|6|ExternalNav|
|7|WheelEncoder|

## EK3_SRC3_POSZ: Position Vertical Source (Tertiary)

*Note: This parameter is for advanced users*

Position Vertical Source (Tertiary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Baro|
|2|RangeFinder|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC3_VELZ: Velocity Vertical Source (Tertiary)

*Note: This parameter is for advanced users*

Velocity Vertical Source (Tertiary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|3|GPS|
|4|Beacon|
|6|ExternalNav|

## EK3_SRC3_YAW: Yaw Source (Tertiary)

*Note: This parameter is for advanced users*

Yaw Source (Tertiary)

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Compass|
|2|GPS|
|3|GPS with Compass Fallback|
|6|ExternalNav|
|8|GSF|

## EK3_SRC_OPTIONS: EKF Source Options

*Note: This parameter is for advanced users*

EKF Source Options

- Bitmask: 0:FuseAllVelocities, 1:AlignExtNavPosWhenUsingOptFlow

# ESCTLM Parameters

## ESC_TLM_MAV_OFS: ESC Telemetry mavlink offset

Offset to apply to ESC numbers when reporting as ESC_TELEMETRY packets over MAVLink. This allows high numbered motors to be displayed as low numbered ESCs for convenience on GCS displays. A value of 4 would send ESC on output 5 as ESC number 1 in ESC_TELEMETRY packets

- Increment: 1

- Range: 0 31

# FENCE Parameters

## FENCE_ENABLE: Fence enable/disable

Allows you to enable (1) or disable (0) the fence functionality. Fences can still be enabled and disabled via mavlink or an RC option, but these changes are not persisted.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## FENCE_TYPE: Fence Type

Configured fence types held as bitmask. Max altitide, Circle and Polygon fences will be immediately enabled if configured. Min altitude fence will only be enabled once the minimum altitude is reached.

- Bitmask: 1:Circle Centered on Home,2:Inclusion/Exclusion Circles+Polygons

## FENCE_ACTION: Fence Action

What action should be taken when fence is breached

|Value|Meaning|
|:---:|:---:|
|0|Report Only|
|1|RTL or Hold|
|2|Hold|
|3|SmartRTL or RTL or Hold|
|4|SmartRTL or Hold|

## FENCE_RADIUS: Circular Fence Radius

Circle fence radius which when breached will cause an RTL

- Units: m

- Range: 30 10000

## FENCE_MARGIN: Fence Margin

Distance that autopilot's should maintain from the fence to avoid a breach

- Units: m

- Range: 1 10

## FENCE_TOTAL: Fence polygon point total

Number of polygon points saved in eeprom (do not update manually)

- Range: 1 20

# FFT Parameters

## FFT_ENABLE: Enable

*Note: This parameter is for advanced users*

Enable Gyro FFT analyser

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## FFT_MINHZ: Minimum Frequency

*Note: This parameter is for advanced users*

Lower bound of FFT frequency detection in Hz. On larger vehicles the minimum motor frequency is likely to be significantly lower than for smaller vehicles.

- Range: 20 400

- Units: Hz

## FFT_MAXHZ: Maximum Frequency

*Note: This parameter is for advanced users*

Upper bound of FFT frequency detection in Hz. On smaller vehicles the maximum motor frequency is likely to be significantly higher than for larger vehicles.

- Range: 20 495

- Units: Hz

## FFT_SAMPLE_MODE: Sample Mode

*Note: This parameter is for advanced users*

Sampling mode (and therefore rate). 0: Gyro rate sampling, 1: Fast loop rate sampling, 2: Fast loop rate / 2 sampling, 3: Fast loop rate / 3 sampling. Takes effect on reboot.

- Range: 0 4

- RebootRequired: True

## FFT_WINDOW_SIZE: FFT window size

*Note: This parameter is for advanced users*

Size of window to be used in FFT calculations. Takes effect on reboot. Must be a power of 2 and between 32 and 512. Larger windows give greater frequency resolution but poorer time resolution, consume more CPU time and may not be appropriate for all vehicles. Time and frequency resolution are given by the sample-rate / window-size. Windows of 256 are only really recommended for F7 class boards, windows of 512 or more H7 class.

- Range: 32 1024

- RebootRequired: True

## FFT_WINDOW_OLAP: FFT window overlap

*Note: This parameter is for advanced users*

Percentage of window to be overlapped before another frame is process. Takes effect on reboot. A good default is 50% overlap. Higher overlap results in more processed frames but not necessarily more temporal resolution. Lower overlap results in lost information at the frame edges.

- Range: 0 0.9

- RebootRequired: True

## FFT_FREQ_HOVER: FFT learned hover frequency

*Note: This parameter is for advanced users*

The learned hover noise frequency

- Range: 0 250

## FFT_THR_REF: FFT learned thrust reference

*Note: This parameter is for advanced users*

FFT learned thrust reference for the hover frequency and FFT minimum frequency.

- Range: 0.01 0.9

## FFT_SNR_REF: FFT SNR reference threshold

*Note: This parameter is for advanced users*

FFT SNR reference threshold in dB at which a signal is determined to be present.

- Range: 0.0 100.0

## FFT_ATT_REF: FFT attenuation for bandwidth calculation

*Note: This parameter is for advanced users*

FFT attenuation level in dB for bandwidth calculation and peak detection. The bandwidth is calculated by comparing peak power output with the attenuated version. The default of 15 has shown to be a good compromise in both simulations and real flight.

- Range: 0 100

## FFT_BW_HOVER: FFT learned bandwidth at hover

*Note: This parameter is for advanced users*

FFT learned bandwidth at hover for the attenuation frequencies.

- Range: 0 200

## FFT_HMNC_FIT: FFT harmonic fit frequency threshold

*Note: This parameter is for advanced users*

FFT harmonic fit frequency threshold percentage at which a signal of the appropriate frequency is determined to be the harmonic of another. Signals that have a harmonic relationship that varies at most by this percentage are considered harmonics of each other for the purpose of selecting the harmonic notch frequency. If a match is found then the lower frequency harmonic is always used as the basis for the dynamic harmonic notch. A value of zero completely disables harmonic matching.

- Range: 0 100

- RebootRequired: True

## FFT_HMNC_PEAK: FFT harmonic peak target

*Note: This parameter is for advanced users*

The FFT harmonic peak target that should be returned by FTN1.PkAvg. The resulting value will be used by the harmonic notch if configured to track the FFT frequency. By default the appropriate peak is auto-detected based on the harmonic fit between peaks and the energy-weighted average frequency on roll on pitch is used. Setting this to 1 will always target the highest energy peak. Setting this to 2 will target the highest energy peak that is lower in frequency than the highest energy peak. Setting this to 3 will target the highest energy peak that is higher in frequency than the highest energy peak. Setting this to 4 will target the highest energy peak on the roll axis only and only the roll frequency will be used (some vehicles have a much more pronounced peak on roll). Setting this to 5 will target the highest energy peak on the pitch axis only and only the pitch frequency will be used (some vehicles have a much more pronounced peak on roll).

|Value|Meaning|
|:---:|:---:|
|0|Auto|
|1|Center Frequency|
|2|Lower-Shoulder Frequency|
|3|Upper-Shoulder Frequency|
|4|Roll-Axis|
|5|Pitch-Axis|

## FFT_NUM_FRAMES: FFT output frames to retain and average

*Note: This parameter is for advanced users*

Number of output frequency frames to retain and average in order to calculate final frequencies. Averaging output frames can drastically reduce noise and jitter at the cost of latency as long as the input is stable. The default is to perform no averaging. For rapidly changing frequencies (e.g. smaller aircraft) fewer frames should be averaged.

- Range: 0 8

- RebootRequired: True

## FFT_OPTIONS: FFT options

*Note: This parameter is for advanced users*

FFT configuration options. Values: 1:Apply the FFT *after* the filter bank,2:Check noise at the motor frequencies using ESC data as a reference

- Bitmask: 0:Enable post-filter FFT,1:Check motor noise

- RebootRequired: True

# FILT1 Parameters

## FILT1_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT1_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT1_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT1_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT2 Parameters

## FILT2_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT2_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT2_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT2_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT3 Parameters

## FILT3_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT3_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT3_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT3_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT4 Parameters

## FILT4_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT4_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT4_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT4_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT5 Parameters

## FILT5_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT5_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT5_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT5_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT6 Parameters

## FILT6_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT6_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT6_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT6_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT7 Parameters

## FILT7_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT7_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT7_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT7_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FILT8 Parameters

## FILT8_TYPE: Filter Type

Filter Type

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Notch Filter|

- RebootRequired: True

## FILT8_NOTCH_FREQ: Notch Filter center frequency

*Note: This parameter is for advanced users*

Notch Filter center frequency in Hz.

- Range: 10 495

- Units: Hz

## FILT8_NOTCH_Q: Notch Filter quality factor

*Note: This parameter is for advanced users*

Notch Filter quality factor given by the notch centre frequency divided by its bandwidth.

- Range: 1 10

## FILT8_NOTCH_ATT: Notch Filter attenuation

*Note: This parameter is for advanced users*

Notch Filter attenuation in dB.

- Range: 5 50

- Units: dB

# FLOW Parameters

## FLOW_TYPE: Optical flow sensor type

Optical flow sensor type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|PX4Flow|
|2|Pixart|
|3|Bebop|
|4|CXOF|
|5|MAVLink|
|6|DroneCAN|
|7|MSP|
|8|UPFLOW|

- RebootRequired: True

## FLOW_FXSCALER: X axis optical flow scale factor correction

This sets the parts per thousand scale factor correction applied to the flow sensor X axis optical rate. It can be used to correct for variations in effective focal length. Each positive increment of 1 increases the scale factor applied to the X axis optical flow reading by 0.1%. Negative values reduce the scale factor.

- Range: -800 +800

- Increment: 1

## FLOW_FYSCALER: Y axis optical flow scale factor correction

This sets the parts per thousand scale factor correction applied to the flow sensor Y axis optical rate. It can be used to correct for variations in effective focal length. Each positive increment of 1 increases the scale factor applied to the Y axis optical flow reading by 0.1%. Negative values reduce the scale factor.

- Range: -800 +800

- Increment: 1

## FLOW_ORIENT_YAW: Flow sensor yaw alignment

Specifies the number of centi-degrees that the flow sensor is yawed relative to the vehicle. A sensor with its X-axis pointing to the right of the vehicle X axis has a positive yaw angle.

- Units: cdeg

- Range: -17999 +18000

- Increment: 10

## FLOW_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the optical flow sensor focal point in body frame. Positive X is forward of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## FLOW_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the optical flow sensor focal point in body frame. Positive Y is to the right of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## FLOW_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the optical flow sensor focal point in body frame. Positive Z is down from the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## FLOW_ADDR: Address on the bus

*Note: This parameter is for advanced users*

This is used to select between multiple possible I2C addresses for some sensor types. For PX4Flow you can choose 0 to 7 for the 8 possible addresses on the I2C bus.

- Range: 0 127

## FLOW_HGT_OVR: Height override of sensor above ground

*Note: This parameter is for advanced users*

This is used in rover vehicles, where the sensor is a fixed height above the ground

- Units: m

- Range: 0 2

- Increment: 0.01

# FOLL Parameters

## FOLL_ENABLE: Follow enable/disable

Enabled/disable following a target

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## FOLL_SYSID: Follow target's mavlink system id

Follow target's mavlink system id

- Range: 0 255

## FOLL_DIST_MAX: Follow distance maximum

Follow distance maximum.  targets further than this will be ignored

- Units: m

- Range: 1 1000

## FOLL_OFS_TYPE: Follow offset type

Follow offset type

|Value|Meaning|
|:---:|:---:|
|0|North-East-Down|
|1|Relative to lead vehicle heading|

## FOLL_OFS_X: Follow offsets in meters north/forward

Follow offsets in meters north/forward.  If positive, this vehicle fly ahead or north of lead vehicle.  Depends on FOLL_OFS_TYPE

- Range: -100 100

- Units: m

- Increment: 1

## FOLL_OFS_Y: Follow offsets in meters east/right

Follow offsets in meters east/right.  If positive, this vehicle will fly to the right or east of lead vehicle.  Depends on FOLL_OFS_TYPE

- Range: -100 100

- Units: m

- Increment: 1

## FOLL_OFS_Z: Follow offsets in meters down

Follow offsets in meters down.  If positive, this vehicle will fly below the lead vehicle

- Range: -100 100

- Units: m

- Increment: 1

## FOLL_YAW_BEHAVE: Follow yaw behaviour

Follow yaw behaviour

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Face Lead Vehicle|
|2|Same as Lead vehicle|
|3|Direction of Flight|

## FOLL_POS_P: Follow position error P gain

Follow position error P gain.  Converts the difference between desired vertical speed and actual speed into a desired acceleration that is passed to the throttle acceleration controller

- Range: 0.01 1.00

- Increment: 0.01

## FOLL_ALT_TYPE: Follow altitude type

Follow altitude type

|Value|Meaning|
|:---:|:---:|
|0|absolute|
|1|relative|

## FOLL_OPTIONS: Follow options

Follow options bitmask

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Mount Follows lead vehicle on mode enter|

# FRSKY Parameters

## FRSKY_UPLINK_ID: Uplink sensor id

*Note: This parameter is for advanced users*

Change the uplink sensor id (SPort only)

|Value|Meaning|
|:---:|:---:|
|-1|Disable|
|7|7|
|8|8|
|9|9|
|10|10|
|11|11|
|12|12|
|13|13|
|14|14|
|15|15|
|16|16|
|17|17|
|18|18|
|19|19|
|20|20|
|21|21|
|22|22|
|23|23|
|24|24|
|25|25|
|26|26|

## FRSKY_DNLINK1_ID: First downlink sensor id

*Note: This parameter is for advanced users*

Change the first extra downlink sensor id (SPort only)

|Value|Meaning|
|:---:|:---:|
|-1|Disable|
|7|7|
|8|8|
|9|9|
|10|10|
|11|11|
|12|12|
|13|13|
|14|14|
|15|15|
|16|16|
|17|17|
|18|18|
|19|19|
|20|20|
|21|21|
|22|22|
|23|23|
|24|24|
|25|25|
|26|26|

## FRSKY_DNLINK2_ID: Second downlink sensor id

*Note: This parameter is for advanced users*

Change the second extra downlink sensor id (SPort only)

|Value|Meaning|
|:---:|:---:|
|-1|Disable|
|7|7|
|8|8|
|9|9|
|10|10|
|11|11|
|12|12|
|13|13|
|14|14|
|15|15|
|16|16|
|17|17|
|18|18|
|19|19|
|20|20|
|21|21|
|22|22|
|23|23|
|24|24|
|25|25|
|26|26|

## FRSKY_DNLINK_ID: Default downlink sensor id

*Note: This parameter is for advanced users*

Change the default downlink sensor id (SPort only)

|Value|Meaning|
|:---:|:---:|
|-1|Disable|
|7|7|
|8|8|
|9|9|
|10|10|
|11|11|
|12|12|
|13|13|
|14|14|
|15|15|
|16|16|
|17|17|
|18|18|
|19|19|
|20|20|
|21|21|
|22|22|
|23|23|
|24|24|
|25|25|
|26|26|
|27|27|

## FRSKY_OPTIONS: FRSky Telemetry Options

A bitmask to set some FRSky Telemetry specific options

- Bitmask: 0:EnableAirspeedAndGroundspeed

# GEN Parameters

## GEN_TYPE: Generator type

Generator type

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|IE 650w 800w Fuel Cell|
|2|IE 2.4kW Fuel Cell|
|3|Richenpower|

- RebootRequired: True

## GEN_OPTIONS: Generator Options

Bitmask of options for generators

- Bitmask: 0:Suppress Maintenance-Required Warnings

# GPS Parameters

## GPS_NAVFILTER: Navigation filter setting

*Note: This parameter is for advanced users*

Navigation filter engine setting

|Value|Meaning|
|:---:|:---:|
|0|Portable|
|2|Stationary|
|3|Pedestrian|
|4|Automotive|
|5|Sea|
|6|Airborne1G|
|7|Airborne2G|
|8|Airborne4G|

## GPS_AUTO_SWITCH: Automatic Switchover Setting

*Note: This parameter is for advanced users*

Automatic switchover to GPS reporting best lock, 1:UseBest selects the GPS with highest status, if both are equal the GPS with highest satellite count is used 4:Use primary if 3D fix or better, will revert to 'UseBest' behaviour if 3D fix is lost on primary

|Value|Meaning|
|:---:|:---:|
|0|Use primary|
|1|UseBest|
|2|Blend|
|4|Use primary if 3D fix or better|

## GPS_SBAS_MODE: SBAS Mode

*Note: This parameter is for advanced users*

This sets the SBAS (satellite based augmentation system) mode if available on this GPS. If set to 2 then the SBAS mode is not changed in the GPS. Otherwise the GPS will be reconfigured to enable/disable SBAS. Disabling SBAS may be worthwhile in some parts of the world where an SBAS signal is available but the baseline is too long to be useful.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|NoChange|

## GPS_MIN_ELEV: Minimum elevation

*Note: This parameter is for advanced users*

This sets the minimum elevation of satellites above the horizon for them to be used for navigation. Setting this to -100 leaves the minimum elevation set to the GPS modules default.

- Range: -100 90

- Units: deg

## GPS_INJECT_TO: Destination for GPS_INJECT_DATA MAVLink packets

*Note: This parameter is for advanced users*

The GGS can send raw serial packets to inject data to multiple GPSes.

|Value|Meaning|
|:---:|:---:|
|0|send to first GPS|
|1|send to 2nd GPS|
|127|send to all|

## GPS_SBP_LOGMASK: Swift Binary Protocol Logging Mask

*Note: This parameter is for advanced users*

Masked with the SBP msg_type field to determine whether SBR1/SBR2 data is logged

|Value|Meaning|
|:---:|:---:|
|0|None (0x0000)|
|-1|All (0xFFFF)|
|-256|External only (0xFF00)|

## GPS_RAW_DATA: Raw data logging

*Note: This parameter is for advanced users*

Handles logging raw data; on uBlox chips that support raw data this will log RXM messages into logger; on Septentrio this will log on the equipment's SD card and when set to 2, the autopilot will try to stop logging after disarming and restart after arming

|Value|Meaning|
|:---:|:---:|
|0|Ignore|
|1|Always log|
|2|Stop logging when disarmed (SBF only)|
|5|Only log every five samples (uBlox only)|

- RebootRequired: True

## GPS_SAVE_CFG: Save GPS configuration

*Note: This parameter is for advanced users*

Determines whether the configuration for this GPS should be written to non-volatile memory on the GPS. Currently working for UBlox 6 series and above.

|Value|Meaning|
|:---:|:---:|
|0|Do not save config|
|1|Save config|
|2|Save only when needed|

## GPS_AUTO_CONFIG: Automatic GPS configuration

*Note: This parameter is for advanced users*

Controls if the autopilot should automatically configure the GPS based on the parameters and default settings

|Value|Meaning|
|:---:|:---:|
|0|Disables automatic configuration|
|1|Enable automatic configuration for Serial GPSes only|
|2|Enable automatic configuration for DroneCAN as well|

## GPS_BLEND_MASK: Multi GPS Blending Mask

*Note: This parameter is for advanced users*

Determines which of the accuracy measures Horizontal position, Vertical Position and Speed are used to calculate the weighting on each GPS receiver when soft switching has been selected by setting GPS_AUTO_SWITCH to 2(Blend)

- Bitmask: 0:Horiz Pos,1:Vert Pos,2:Speed

## GPS_DRV_OPTIONS: driver options

*Note: This parameter is for advanced users*

Additional backend specific options

- Bitmask: 0:Use UART2 for moving baseline on ublox,1:Use base station for GPS yaw on SBF,2:Use baudrate 115200,3:Use dedicated CAN port b/w GPSes for moving baseline,4:Use ellipsoid height instead of AMSL, 5:Override GPS satellite health of L5 band from L1 health, 6:Enable RTCM full parse even for a single channel, 7:Disable automatic full RTCM parsing when RTCM seen on more than one channel

## GPS_PRIMARY: Primary GPS

*Note: This parameter is for advanced users*

This GPS will be used when GPS_AUTO_SWITCH is 0 and used preferentially with GPS_AUTO_SWITCH = 4.

- Increment: 1

|Value|Meaning|
|:---:|:---:|
|0|FirstGPS|
|1|SecondGPS|

## GPS_TYPE: 1st GPS type

*Note: This parameter is for advanced users*

GPS type of 1st GPS.Renamed in 4.6 and later to GPS1_TYPE

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|AUTO|
|2|uBlox|
|5|NMEA|
|6|SiRF|
|7|HIL|
|8|SwiftNav|
|9|DroneCAN|
|10|SBF|
|11|GSOF|
|13|ERB|
|14|MAV|
|15|NOVA|
|16|HemisphereNMEA|
|17|uBlox-MovingBaseline-Base|
|18|uBlox-MovingBaseline-Rover|
|19|MSP|
|20|AllyStar|
|21|ExternalAHRS|
|22|DroneCAN-MovingBaseline-Base|
|23|DroneCAN-MovingBaseline-Rover|
|24|UnicoreNMEA|
|25|UnicoreMovingBaselineNMEA|
|26|SBF-DualAntenna|

- RebootRequired: True

## GPS_TYPE2: 2nd GPS type.Renamed in 4.6 to GPS2_TYPE

*Note: This parameter is for advanced users*

GPS type of 2nd GPS

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|AUTO|
|2|uBlox|
|5|NMEA|
|6|SiRF|
|7|HIL|
|8|SwiftNav|
|9|DroneCAN|
|10|SBF|
|11|GSOF|
|13|ERB|
|14|MAV|
|15|NOVA|
|16|HemisphereNMEA|
|17|uBlox-MovingBaseline-Base|
|18|uBlox-MovingBaseline-Rover|
|19|MSP|
|20|AllyStar|
|21|ExternalAHRS|
|22|DroneCAN-MovingBaseline-Base|
|23|DroneCAN-MovingBaseline-Rover|
|24|UnicoreNMEA|
|25|UnicoreMovingBaselineNMEA|
|26|SBF-DualAntenna|

## GPS_GNSS_MODE: GNSS system configuration

*Note: This parameter is for advanced users*

Bitmask for what GNSS system to use on the first GPS (all unchecked or zero to leave GPS as configured).Renamed in 4.6 and later to GPS1_GNSS_MODE.

- Bitmask: 0:GPS,1:SBAS,2:Galileo,3:Beidou,4:IMES,5:QZSS,6:GLONASS

## GPS_GNSS_MODE2: GNSS system configuration.

*Note: This parameter is for advanced users*

Bitmask for what GNSS system to use on the second GPS (all unchecked or zero to leave GPS as configured). Renamed in 4.6 and later to GPS2_GNSS_MODE

- Bitmask: 0:GPS,1:SBAS,2:Galileo,3:Beidou,4:IMES,5:QZSS,6:GLONASS

## GPS_RATE_MS: GPS update rate in milliseconds

*Note: This parameter is for advanced users*

Controls how often the GPS should provide a position update. Lowering below 5Hz(default) is not allowed. Raising the rate above 5Hz usually provides little benefit and for some GPS (eg Ublox M9N) can severely impact performance.Renamed in 4.6 and later to GPS1_RATE_MS

- Units: ms

|Value|Meaning|
|:---:|:---:|
|100|10Hz|
|125|8Hz|
|200|5Hz|

- Range: 50 200

## GPS_RATE_MS2: GPS 2 update rate in milliseconds

*Note: This parameter is for advanced users*

Controls how often the GPS should provide a position update. Lowering below 5Hz(default) is not allowed. Raising the rate above 5Hz usually provides little benefit and for some GPS (eg Ublox M9N) can severely impact performance.Renamed in 4.6 and later to GPS2_RATE_MS

- Units: ms

|Value|Meaning|
|:---:|:---:|
|100|10Hz|
|125|8Hz|
|200|5Hz|

- Range: 50 200

## GPS_POS1_X: Antenna X position offset

*Note: This parameter is for advanced users*

X position of the first GPS antenna in body frame. Positive X is forward of the origin. Use antenna phase centroid location if provided by the manufacturer.Renamed in 4.6 and later to GPS1_POS_X.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_POS1_Y: Antenna Y position offset

*Note: This parameter is for advanced users*

Y position of the first GPS antenna in body frame. Positive Y is to the right of the origin. Use antenna phase centroid location if provided by the manufacturer.Renamed in 4.6 and later to GPS1_POS_Y.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_POS1_Z: Antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the first GPS antenna in body frame. Positive Z is down from the origin. Use antenna phase centroid location if provided by the manufacturer.Renamed in 4.6 and later to GPS1_POS_Z.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_POS2_X: Antenna X position offset

*Note: This parameter is for advanced users*

X position of the second GPS antenna in body frame. Positive X is forward of the origin. Use antenna phase centroid location if provided by the manufacturer.Renamed in 4.6 and later to GPS2_POS_X.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_POS2_Y: Antenna Y position offset

*Note: This parameter is for advanced users*

Y position of the second GPS antenna in body frame. Positive Y is to the right of the origin. Use antenna phase centroid location if provided by the manufacturer.Renamed in 4.6 and later to GPS2_POS_Y.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_POS2_Z: Antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the second GPS antenna in body frame. Positive Z is down from the origin. Use antenna phase centroid location if provided by the manufacturer.Renamed in 4.6 and later to GPS2_POS_Z.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_DELAY_MS: GPS delay in milliseconds

*Note: This parameter is for advanced users*

Controls the amount of GPS  measurement delay that the autopilot compensates for. Set to zero to use the default delay for the detected GPS type.Renamed in 4.6 and later to GPS1_DELAY_MS.

- Units: ms

- Range: 0 250

- RebootRequired: True

## GPS_DELAY_MS2: GPS 2 delay in milliseconds

*Note: This parameter is for advanced users*

Controls the amount of GPS  measurement delay that the autopilot compensates for. Set to zero to use the default delay for the detected GPS type.Renamed in 4.6 and later to GPS2_DELAY_MS.

- Units: ms

- Range: 0 250

- RebootRequired: True

## GPS_COM_PORT: GPS physical COM port

*Note: This parameter is for advanced users*

The physical COM port on the connected device, currently only applies to SBF and GSOF GPS,Renamed in 4.6 and later to GPS1_COM_PORT.

- Range: 0 10

- Increment: 1

|Value|Meaning|
|:---:|:---:|
|0|COM1(RS232) on GSOF|
|1|COM2(TTL) on GSOF|

- RebootRequired: True

## GPS_COM_PORT2: GPS physical COM port

*Note: This parameter is for advanced users*

The physical COM port on the connected device, currently only applies to SBF and GSOF GPS.Renamed in 4.6 and later to GPS1_COM_PORT.

- Range: 0 10

- Increment: 1

- RebootRequired: True

## GPS_CAN_NODEID1: GPS Node ID 1

*Note: This parameter is for advanced users*

GPS Node id for first-discovered GPS.Renamed in 4.6 and later to GPS1_CAN_NODEID.

- ReadOnly: True

## GPS_CAN_NODEID2: GPS Node ID 2

*Note: This parameter is for advanced users*

GPS Node id for second-discovered GPS.Renamed in 4.6 and later to GPS2_CAN_NODEID.

- ReadOnly: True

# GPS1 Parameters

## GPS1_TYPE: GPS type

*Note: This parameter is for advanced users*

GPS type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|AUTO|
|2|uBlox|
|5|NMEA|
|6|SiRF|
|7|HIL|
|8|SwiftNav|
|9|DroneCAN|
|10|Septentrio(SBF)|
|11|Trimble(GSOF)|
|13|ERB|
|14|MAVLink|
|15|NOVA|
|16|HemisphereNMEA|
|17|uBlox-MovingBaseline-Base|
|18|uBlox-MovingBaseline-Rover|
|19|MSP|
|20|AllyStar|
|21|ExternalAHRS|
|22|DroneCAN-MovingBaseline-Base|
|23|DroneCAN-MovingBaseline-Rover|
|24|UnicoreNMEA|
|25|UnicoreMovingBaselineNMEA|
|26|Septentrio-DualAntenna(SBF)|

- RebootRequired: True

## GPS1_GNSS_MODE: GNSS system configuration

*Note: This parameter is for advanced users*

Bitmask for what GNSS system to use on the first GPS (all unchecked or zero to leave GPS as configured)

- Bitmask: 0:GPS,1:SBAS,2:Galileo,3:Beidou,4:IMES,5:QZSS,6:GLONASS

## GPS1_RATE_MS: GPS update rate in milliseconds

*Note: This parameter is for advanced users*

Controls how often the GPS should provide a position update. Lowering below 5Hz(default) is not allowed. Raising the rate above 5Hz usually provides little benefit and for some GPS (eg Ublox M9N) can severely impact performance.

- Units: ms

|Value|Meaning|
|:---:|:---:|
|100|10Hz|
|125|8Hz|
|200|5Hz|

- Range: 50 200

## GPS1_POS_X: Antenna X position offset

*Note: This parameter is for advanced users*

X position of the first GPS antenna in body frame. Positive X is forward of the origin. Use antenna phase centroid location if provided by the manufacturer.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS1_POS_Y: Antenna Y position offset

*Note: This parameter is for advanced users*

Y position of the first GPS antenna in body frame. Positive Y is to the right of the origin. Use antenna phase centroid location if provided by the manufacturer.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS1_POS_Z: Antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the first GPS antenna in body frame. Positive Z is down from the origin. Use antenna phase centroid location if provided by the manufacturer.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS1_DELAY_MS: GPS delay in milliseconds

*Note: This parameter is for advanced users*

Controls the amount of GPS  measurement delay that the autopilot compensates for. Set to zero to use the default delay for the detected GPS type.

- Units: ms

- Range: 0 250

- RebootRequired: True

## GPS1_COM_PORT: GPS physical COM port

*Note: This parameter is for advanced users*

The physical COM port on the connected device, currently only applies to SBF and GSOF GPS

- Range: 0 10

- Increment: 1

|Value|Meaning|
|:---:|:---:|
|0|COM1(RS232) on GSOF|
|1|COM2(TTL) on GSOF|

- RebootRequired: True

## GPS1_CAN_NODEID: Detected CAN Node ID for GPS

*Note: This parameter is for advanced users*

GPS Node id for GPS.  Detected node unless CAN_OVRIDE is set

- ReadOnly: True

## GPS1_CAN_OVRIDE: DroneCAN GPS NODE ID

*Note: This parameter is for advanced users*

GPS Node id for GPS. If 0 the gps will be automatically selected on a first-come-first-GPS basis.

# GPS1MB Parameters

## GPS1_MB_TYPE: Moving base type

*Note: This parameter is for advanced users*

Controls the type of moving base used if using moving base.This is renamed in 4.6 and later to GPSx_MB_TYPE.

|Value|Meaning|
|:---:|:---:|
|0|Relative to alternate GPS instance|
|1|RelativeToCustomBase|

- RebootRequired: True

## GPS1_MB_OFS_X: Base antenna X position offset

*Note: This parameter is for advanced users*

X position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive X is forward of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_X.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS1_MB_OFS_Y: Base antenna Y position offset    

*Note: This parameter is for advanced users*

Y position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Y is to the right of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Y.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS1_MB_OFS_Z: Base antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Z is down from the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Z.

- Units: m

- Range: -5 5

- Increment: 0.01

# GPS2 Parameters

## GPS2_TYPE: GPS type

*Note: This parameter is for advanced users*

GPS type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|AUTO|
|2|uBlox|
|5|NMEA|
|6|SiRF|
|7|HIL|
|8|SwiftNav|
|9|DroneCAN|
|10|Septentrio(SBF)|
|11|Trimble(GSOF)|
|13|ERB|
|14|MAVLink|
|15|NOVA|
|16|HemisphereNMEA|
|17|uBlox-MovingBaseline-Base|
|18|uBlox-MovingBaseline-Rover|
|19|MSP|
|20|AllyStar|
|21|ExternalAHRS|
|22|DroneCAN-MovingBaseline-Base|
|23|DroneCAN-MovingBaseline-Rover|
|24|UnicoreNMEA|
|25|UnicoreMovingBaselineNMEA|
|26|Septentrio-DualAntenna(SBF)|

- RebootRequired: True

## GPS2_GNSS_MODE: GNSS system configuration

*Note: This parameter is for advanced users*

Bitmask for what GNSS system to use on the first GPS (all unchecked or zero to leave GPS as configured)

- Bitmask: 0:GPS,1:SBAS,2:Galileo,3:Beidou,4:IMES,5:QZSS,6:GLONASS

## GPS2_RATE_MS: GPS update rate in milliseconds

*Note: This parameter is for advanced users*

Controls how often the GPS should provide a position update. Lowering below 5Hz(default) is not allowed. Raising the rate above 5Hz usually provides little benefit and for some GPS (eg Ublox M9N) can severely impact performance.

- Units: ms

|Value|Meaning|
|:---:|:---:|
|100|10Hz|
|125|8Hz|
|200|5Hz|

- Range: 50 200

## GPS2_POS_X: Antenna X position offset

*Note: This parameter is for advanced users*

X position of the first GPS antenna in body frame. Positive X is forward of the origin. Use antenna phase centroid location if provided by the manufacturer.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS2_POS_Y: Antenna Y position offset

*Note: This parameter is for advanced users*

Y position of the first GPS antenna in body frame. Positive Y is to the right of the origin. Use antenna phase centroid location if provided by the manufacturer.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS2_POS_Z: Antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the first GPS antenna in body frame. Positive Z is down from the origin. Use antenna phase centroid location if provided by the manufacturer.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS2_DELAY_MS: GPS delay in milliseconds

*Note: This parameter is for advanced users*

Controls the amount of GPS  measurement delay that the autopilot compensates for. Set to zero to use the default delay for the detected GPS type.

- Units: ms

- Range: 0 250

- RebootRequired: True

## GPS2_COM_PORT: GPS physical COM port

*Note: This parameter is for advanced users*

The physical COM port on the connected device, currently only applies to SBF and GSOF GPS

- Range: 0 10

- Increment: 1

|Value|Meaning|
|:---:|:---:|
|0|COM1(RS232) on GSOF|
|1|COM2(TTL) on GSOF|

- RebootRequired: True

## GPS2_CAN_NODEID: Detected CAN Node ID for GPS

*Note: This parameter is for advanced users*

GPS Node id for GPS.  Detected node unless CAN_OVRIDE is set

- ReadOnly: True

## GPS2_CAN_OVRIDE: DroneCAN GPS NODE ID

*Note: This parameter is for advanced users*

GPS Node id for GPS. If 0 the gps will be automatically selected on a first-come-first-GPS basis.

# GPS2MB Parameters

## GPS2_MB_TYPE: Moving base type

*Note: This parameter is for advanced users*

Controls the type of moving base used if using moving base.This is renamed in 4.6 and later to GPSx_MB_TYPE.

|Value|Meaning|
|:---:|:---:|
|0|Relative to alternate GPS instance|
|1|RelativeToCustomBase|

- RebootRequired: True

## GPS2_MB_OFS_X: Base antenna X position offset

*Note: This parameter is for advanced users*

X position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive X is forward of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_X.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS2_MB_OFS_Y: Base antenna Y position offset    

*Note: This parameter is for advanced users*

Y position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Y is to the right of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Y.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS2_MB_OFS_Z: Base antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Z is down from the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Z.

- Units: m

- Range: -5 5

- Increment: 0.01

# GPSMB1 Parameters

## GPS_MB1_TYPE: Moving base type

*Note: This parameter is for advanced users*

Controls the type of moving base used if using moving base.This is renamed in 4.6 and later to GPSx_MB_TYPE.

|Value|Meaning|
|:---:|:---:|
|0|Relative to alternate GPS instance|
|1|RelativeToCustomBase|

- RebootRequired: True

## GPS_MB1_OFS_X: Base antenna X position offset

*Note: This parameter is for advanced users*

X position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive X is forward of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_X.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_MB1_OFS_Y: Base antenna Y position offset    

*Note: This parameter is for advanced users*

Y position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Y is to the right of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Y.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_MB1_OFS_Z: Base antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Z is down from the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Z.

- Units: m

- Range: -5 5

- Increment: 0.01

# GPSMB2 Parameters

## GPS_MB2_TYPE: Moving base type

*Note: This parameter is for advanced users*

Controls the type of moving base used if using moving base.This is renamed in 4.6 and later to GPSx_MB_TYPE.

|Value|Meaning|
|:---:|:---:|
|0|Relative to alternate GPS instance|
|1|RelativeToCustomBase|

- RebootRequired: True

## GPS_MB2_OFS_X: Base antenna X position offset

*Note: This parameter is for advanced users*

X position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive X is forward of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_X.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_MB2_OFS_Y: Base antenna Y position offset    

*Note: This parameter is for advanced users*

Y position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Y is to the right of the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Y.

- Units: m

- Range: -5 5

- Increment: 0.01

## GPS_MB2_OFS_Z: Base antenna Z position offset

*Note: This parameter is for advanced users*

Z position of the base (primary) GPS antenna in body frame from the position of the 2nd antenna. Positive Z is down from the 2nd antenna. Use antenna phase centroid location if provided by the manufacturer.This is renamed in 4.6 and later to GPSx_MB_OFS_Z.

- Units: m

- Range: -5 5

- Increment: 0.01

# GRIP Parameters

## GRIP_ENABLE: Gripper Enable/Disable

Gripper enable/disable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## GRIP_TYPE: Gripper Type

Gripper enable/disable

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Servo|
|2|EPM|

## GRIP_GRAB: Gripper Grab PWM

*Note: This parameter is for advanced users*

PWM value in microseconds sent to Gripper to initiate grabbing the cargo

- Range: 1000 2000

- Units: PWM

## GRIP_RELEASE: Gripper Release PWM

*Note: This parameter is for advanced users*

PWM value in microseconds sent to Gripper to release the cargo

- Range: 1000 2000

- Units: PWM

## GRIP_NEUTRAL: Neutral PWM

*Note: This parameter is for advanced users*

PWM value in microseconds sent to grabber when not grabbing or releasing

- Range: 1000 2000

- Units: PWM

## GRIP_REGRAB: EPM Gripper Regrab interval

*Note: This parameter is for advanced users*

Time in seconds that EPM gripper will regrab the cargo to ensure grip has not weakened; 0 to disable

- Range: 0 255

- Units: s

## GRIP_CAN_ID: EPM UAVCAN Hardpoint ID

Refer to https://docs.zubax.com/opengrab_epm_v3#UAVCAN_interface

- Range: 0 255

## GRIP_AUTOCLOSE: Gripper Autoclose time

*Note: This parameter is for advanced users*

Time in seconds that gripper close the gripper after opening; 0 to disable

- Range: 0.25 255

- Units: s

# INS Parameters

## INS_GYROFFS_X: Gyro offsets of X axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of X axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYROFFS_Y: Gyro offsets of Y axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of Y axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYROFFS_Z: Gyro offsets of Z axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of Z axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYR2OFFS_X: Gyro2 offsets of X axis

*Note: This parameter is for advanced users*

Gyro2 sensor offsets of X axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYR2OFFS_Y: Gyro2 offsets of Y axis

*Note: This parameter is for advanced users*

Gyro2 sensor offsets of Y axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYR2OFFS_Z: Gyro2 offsets of Z axis

*Note: This parameter is for advanced users*

Gyro2 sensor offsets of Z axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYR3OFFS_X: Gyro3 offsets of X axis

*Note: This parameter is for advanced users*

Gyro3 sensor offsets of X axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYR3OFFS_Y: Gyro3 offsets of Y axis

*Note: This parameter is for advanced users*

Gyro3 sensor offsets of Y axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_GYR3OFFS_Z: Gyro3 offsets of Z axis

*Note: This parameter is for advanced users*

Gyro3 sensor offsets of Z axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS_ACCSCAL_X: Accelerometer scaling of X axis

*Note: This parameter is for advanced users*

Accelerometer scaling of X axis.  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACCSCAL_Y: Accelerometer scaling of Y axis

*Note: This parameter is for advanced users*

Accelerometer scaling of Y axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACCSCAL_Z: Accelerometer scaling of Z axis

*Note: This parameter is for advanced users*

Accelerometer scaling of Z axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACCOFFS_X: Accelerometer offsets of X axis

*Note: This parameter is for advanced users*

Accelerometer offsets of X axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACCOFFS_Y: Accelerometer offsets of Y axis

*Note: This parameter is for advanced users*

Accelerometer offsets of Y axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACCOFFS_Z: Accelerometer offsets of Z axis

*Note: This parameter is for advanced users*

Accelerometer offsets of Z axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACC2SCAL_X: Accelerometer2 scaling of X axis

*Note: This parameter is for advanced users*

Accelerometer2 scaling of X axis.  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACC2SCAL_Y: Accelerometer2 scaling of Y axis

*Note: This parameter is for advanced users*

Accelerometer2 scaling of Y axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACC2SCAL_Z: Accelerometer2 scaling of Z axis

*Note: This parameter is for advanced users*

Accelerometer2 scaling of Z axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACC2OFFS_X: Accelerometer2 offsets of X axis

*Note: This parameter is for advanced users*

Accelerometer2 offsets of X axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACC2OFFS_Y: Accelerometer2 offsets of Y axis

*Note: This parameter is for advanced users*

Accelerometer2 offsets of Y axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACC2OFFS_Z: Accelerometer2 offsets of Z axis

*Note: This parameter is for advanced users*

Accelerometer2 offsets of Z axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACC3SCAL_X: Accelerometer3 scaling of X axis

*Note: This parameter is for advanced users*

Accelerometer3 scaling of X axis.  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACC3SCAL_Y: Accelerometer3 scaling of Y axis

*Note: This parameter is for advanced users*

Accelerometer3 scaling of Y axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACC3SCAL_Z: Accelerometer3 scaling of Z axis

*Note: This parameter is for advanced users*

Accelerometer3 scaling of Z axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS_ACC3OFFS_X: Accelerometer3 offsets of X axis

*Note: This parameter is for advanced users*

Accelerometer3 offsets of X axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACC3OFFS_Y: Accelerometer3 offsets of Y axis

*Note: This parameter is for advanced users*

Accelerometer3 offsets of Y axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_ACC3OFFS_Z: Accelerometer3 offsets of Z axis

*Note: This parameter is for advanced users*

Accelerometer3 offsets of Z axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS_GYRO_FILTER: Gyro filter cutoff frequency

*Note: This parameter is for advanced users*

Filter cutoff frequency for gyroscopes. This can be set to a lower value to try to cope with very high vibration levels in aircraft. A value of zero means no filtering (not recommended!)

- Units: Hz

- Range: 0 256

## INS_ACCEL_FILTER: Accel filter cutoff frequency

*Note: This parameter is for advanced users*

Filter cutoff frequency for accelerometers. This can be set to a lower value to try to cope with very high vibration levels in aircraft. A value of zero means no filtering (not recommended!)

- Units: Hz

- Range: 0 256

## INS_USE: Use first IMU for attitude, velocity and position estimates

*Note: This parameter is for advanced users*

Use first IMU for attitude, velocity and position estimates

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS_USE2: Use second IMU for attitude, velocity and position estimates

*Note: This parameter is for advanced users*

Use second IMU for attitude, velocity and position estimates

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS_USE3: Use third IMU for attitude, velocity and position estimates

*Note: This parameter is for advanced users*

Use third IMU for attitude, velocity and position estimates

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS_STILL_THRESH: Stillness threshold for detecting if we are moving

*Note: This parameter is for advanced users*

Threshold to tolerate vibration to determine if vehicle is motionless. This depends on the frame type and if there is a constant vibration due to motors before launch or after landing. Total motionless is about 0.05. Suggested values: Planes/rover use 0.1, multirotors use 1, tradHeli uses 5

- Range: 0.05 50

## INS_GYR_CAL: Gyro Calibration scheme

*Note: This parameter is for advanced users*

Conrols when automatic gyro calibration is performed

|Value|Meaning|
|:---:|:---:|
|0|Never|
|1|Start-up only|

## INS_TRIM_OPTION: Accel cal trim option

*Note: This parameter is for advanced users*

Specifies how the accel cal routine determines the trims

|Value|Meaning|
|:---:|:---:|
|0|Don't adjust the trims|
|1|Assume first orientation was level|
|2|Assume ACC_BODYFIX is perfectly aligned to the vehicle|

## INS_ACC_BODYFIX: Body-fixed accelerometer

*Note: This parameter is for advanced users*

The body-fixed accelerometer to be used for trim calculation

|Value|Meaning|
|:---:|:---:|
|1|IMU 1|
|2|IMU 2|
|3|IMU 3|

## INS_POS1_X: IMU accelerometer X position

*Note: This parameter is for advanced users*

X position of the first IMU Accelerometer in body frame. Positive X is forward of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS1_Y: IMU accelerometer Y position

*Note: This parameter is for advanced users*

Y position of the first IMU accelerometer in body frame. Positive Y is to the right of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS1_Z: IMU accelerometer Z position

*Note: This parameter is for advanced users*

Z position of the first IMU accelerometer in body frame. Positive Z is down from the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS2_X: IMU accelerometer X position

*Note: This parameter is for advanced users*

X position of the second IMU accelerometer in body frame. Positive X is forward of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS2_Y: IMU accelerometer Y position

*Note: This parameter is for advanced users*

Y position of the second IMU accelerometer in body frame. Positive Y is to the right of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS2_Z: IMU accelerometer Z position

*Note: This parameter is for advanced users*

Z position of the second IMU accelerometer in body frame. Positive Z is down from the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS3_X: IMU accelerometer X position

*Note: This parameter is for advanced users*

X position of the third IMU accelerometer in body frame. Positive X is forward of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -10 10

## INS_POS3_Y: IMU accelerometer Y position

*Note: This parameter is for advanced users*

Y position of the third IMU accelerometer in body frame. Positive Y is to the right of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_POS3_Z: IMU accelerometer Z position

*Note: This parameter is for advanced users*

Z position of the third IMU accelerometer in body frame. Positive Z is down from the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS_GYR_ID: Gyro ID

*Note: This parameter is for advanced users*

Gyro sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS_GYR2_ID: Gyro2 ID

*Note: This parameter is for advanced users*

Gyro2 sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS_GYR3_ID: Gyro3 ID

*Note: This parameter is for advanced users*

Gyro3 sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS_ACC_ID: Accelerometer ID

*Note: This parameter is for advanced users*

Accelerometer sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS_ACC2_ID: Accelerometer2 ID

*Note: This parameter is for advanced users*

Accelerometer2 sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS_ACC3_ID: Accelerometer3 ID

*Note: This parameter is for advanced users*

Accelerometer3 sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS_FAST_SAMPLE: Fast sampling mask

*Note: This parameter is for advanced users*

Mask of IMUs to enable fast sampling on, if available

- Bitmask: 0:FirstIMU,1:SecondIMU,2:ThirdIMU

## INS_ENABLE_MASK: IMU enable mask

*Note: This parameter is for advanced users*

Bitmask of IMUs to enable. It can be used to prevent startup of specific detected IMUs

- Bitmask: 0:FirstIMU,1:SecondIMU,2:ThirdIMU,3:FourthIMU,4:FifthIMU,5:SixthIMU,6:SeventhIMU

## INS_GYRO_RATE: Gyro rate for IMUs with Fast Sampling enabled

*Note: This parameter is for advanced users*

Gyro rate for IMUs with fast sampling enabled. The gyro rate is the sample rate at which the IMU filters operate and needs to be at least double the maximum filter frequency. If the sensor does not support the selected rate the next highest supported rate will be used. For IMUs which do not support fast sampling this setting is ignored and the default gyro rate of 1Khz is used.

|Value|Meaning|
|:---:|:---:|
|0|1kHz|
|1|2kHz|
|2|4kHz|
|3|8kHz|

- RebootRequired: True

## INS_ACC1_CALTEMP: Calibration temperature for 1st accelerometer

*Note: This parameter is for advanced users*

Temperature that the 1st accelerometer was calibrated at

- Units: degC

- Calibration: 1

## INS_GYR1_CALTEMP: Calibration temperature for 1st gyroscope

*Note: This parameter is for advanced users*

Temperature that the 1st gyroscope was calibrated at

- Units: degC

- Calibration: 1

## INS_ACC2_CALTEMP: Calibration temperature for 2nd accelerometer

*Note: This parameter is for advanced users*

Temperature that the 2nd accelerometer was calibrated at

- Units: degC

- Calibration: 1

## INS_GYR2_CALTEMP: Calibration temperature for 2nd gyroscope

*Note: This parameter is for advanced users*

Temperature that the 2nd gyroscope was calibrated at

- Units: degC

- Calibration: 1

## INS_ACC3_CALTEMP: Calibration temperature for 3rd accelerometer

*Note: This parameter is for advanced users*

Temperature that the 3rd accelerometer was calibrated at

- Units: degC

- Calibration: 1

## INS_GYR3_CALTEMP: Calibration temperature for 3rd gyroscope

*Note: This parameter is for advanced users*

Temperature that the 3rd gyroscope was calibrated at

- Units: degC

- Calibration: 1

## INS_TCAL_OPTIONS: Options for temperature calibration

*Note: This parameter is for advanced users*

This enables optional temperature calibration features. Setting of the Persist bits will save the temperature and/or accelerometer calibration parameters in the bootloader sector on the next update of the bootloader.

- Bitmask: 0:PersistTemps, 1:PersistAccels

## INS_RAW_LOG_OPT: Raw logging options

*Note: This parameter is for advanced users*

Raw logging options bitmask

- Bitmask: 0:Log primary gyro only, 1:Log all gyros, 2:Post filter, 3: Pre and post filter

# INS4 Parameters

## INS4_USE: Use first IMU for attitude, velocity and position estimates

*Note: This parameter is for advanced users*

Use first IMU for attitude, velocity and position estimates

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS4_ACC_ID: Accelerometer ID

*Note: This parameter is for advanced users*

Accelerometer sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS4_ACCSCAL_X: Accelerometer scaling of X axis

*Note: This parameter is for advanced users*

Accelerometer scaling of X axis.  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS4_ACCSCAL_Y: Accelerometer scaling of Y axis

*Note: This parameter is for advanced users*

Accelerometer scaling of Y axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS4_ACCSCAL_Z: Accelerometer scaling of Z axis

*Note: This parameter is for advanced users*

Accelerometer scaling of Z axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS4_ACCOFFS_X: Accelerometer offsets of X axis

*Note: This parameter is for advanced users*

Accelerometer offsets of X axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS4_ACCOFFS_Y: Accelerometer offsets of Y axis

*Note: This parameter is for advanced users*

Accelerometer offsets of Y axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS4_ACCOFFS_Z: Accelerometer offsets of Z axis

*Note: This parameter is for advanced users*

Accelerometer offsets of Z axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS4_POS_X: IMU accelerometer X position

*Note: This parameter is for advanced users*

X position of the first IMU Accelerometer in body frame. Positive X is forward of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS4_POS_Y: IMU accelerometer Y position

*Note: This parameter is for advanced users*

Y position of the first IMU accelerometer in body frame. Positive Y is to the right of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS4_POS_Z: IMU accelerometer Z position

*Note: This parameter is for advanced users*

Z position of the first IMU accelerometer in body frame. Positive Z is down from the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS4_ACC_CALTEMP: Calibration temperature for accelerometer

*Note: This parameter is for advanced users*

Temperature that the accelerometer was calibrated at

- Units: degC

- Calibration: 1

## INS4_GYR_ID: Gyro ID

*Note: This parameter is for advanced users*

Gyro sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS4_GYROFFS_X: Gyro offsets of X axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of X axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS4_GYROFFS_Y: Gyro offsets of Y axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of Y axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS4_GYROFFS_Z: Gyro offsets of Z axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of Z axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS4_GYR_CALTEMP: Calibration temperature for gyroscope

*Note: This parameter is for advanced users*

Temperature that the gyroscope was calibrated at

- Units: degC

- Calibration: 1

# INS4TCAL Parameters

## INS4_TCAL_ENABLE: Enable temperature calibration

*Note: This parameter is for advanced users*

Enable the use of temperature calibration parameters for this IMU. For automatic learning set to 2 and also set the INS_TCALn_TMAX to the target temperature, then reboot

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|LearnCalibration|

- RebootRequired: True

## INS4_TCAL_TMIN: Temperature calibration min

*Note: This parameter is for advanced users*

The minimum temperature that the calibration is valid for

- Range: -70 80

- Units: degC

- Calibration: 1

## INS4_TCAL_TMAX: Temperature calibration max

*Note: This parameter is for advanced users*

The maximum temperature that the calibration is valid for. This must be at least 10 degrees above TMIN for calibration

- Range: -70 80

- Units: degC

- Calibration: 1

## INS4_TCAL_ACC1_X: Accelerometer 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC1_Y: Accelerometer 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC1_Z: Accelerometer 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC2_X: Accelerometer 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC2_Y: Accelerometer 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC2_Z: Accelerometer 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC3_X: Accelerometer 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC3_Y: Accelerometer 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_ACC3_Z: Accelerometer 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR1_X: Gyroscope 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR1_Y: Gyroscope 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR1_Z: Gyroscope 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR2_X: Gyroscope 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR2_Y: Gyroscope 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR2_Z: Gyroscope 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR3_X: Gyroscope 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR3_Y: Gyroscope 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS4_TCAL_GYR3_Z: Gyroscope 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

# INS5 Parameters

## INS5_USE: Use first IMU for attitude, velocity and position estimates

*Note: This parameter is for advanced users*

Use first IMU for attitude, velocity and position estimates

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS5_ACC_ID: Accelerometer ID

*Note: This parameter is for advanced users*

Accelerometer sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS5_ACCSCAL_X: Accelerometer scaling of X axis

*Note: This parameter is for advanced users*

Accelerometer scaling of X axis.  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS5_ACCSCAL_Y: Accelerometer scaling of Y axis

*Note: This parameter is for advanced users*

Accelerometer scaling of Y axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS5_ACCSCAL_Z: Accelerometer scaling of Z axis

*Note: This parameter is for advanced users*

Accelerometer scaling of Z axis  Calculated during acceleration calibration routine

- Range: 0.8 1.2

- Calibration: 1

## INS5_ACCOFFS_X: Accelerometer offsets of X axis

*Note: This parameter is for advanced users*

Accelerometer offsets of X axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS5_ACCOFFS_Y: Accelerometer offsets of Y axis

*Note: This parameter is for advanced users*

Accelerometer offsets of Y axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS5_ACCOFFS_Z: Accelerometer offsets of Z axis

*Note: This parameter is for advanced users*

Accelerometer offsets of Z axis. This is setup using the acceleration calibration or level operations

- Units: m/s/s

- Range: -3.5 3.5

- Calibration: 1

## INS5_POS_X: IMU accelerometer X position

*Note: This parameter is for advanced users*

X position of the first IMU Accelerometer in body frame. Positive X is forward of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS5_POS_Y: IMU accelerometer Y position

*Note: This parameter is for advanced users*

Y position of the first IMU accelerometer in body frame. Positive Y is to the right of the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS5_POS_Z: IMU accelerometer Z position

*Note: This parameter is for advanced users*

Z position of the first IMU accelerometer in body frame. Positive Z is down from the origin. Attention: The IMU should be located as close to the vehicle c.g. as practical so that the value of this parameter is minimised. Failure to do so can result in noisy navigation velocity measurements due to vibration and IMU gyro noise. If the IMU cannot be moved and velocity noise is a problem, a location closer to the IMU can be used as the body frame origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## INS5_ACC_CALTEMP: Calibration temperature for accelerometer

*Note: This parameter is for advanced users*

Temperature that the accelerometer was calibrated at

- Units: degC

- Calibration: 1

## INS5_GYR_ID: Gyro ID

*Note: This parameter is for advanced users*

Gyro sensor ID, taking into account its type, bus and instance

- ReadOnly: True

## INS5_GYROFFS_X: Gyro offsets of X axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of X axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS5_GYROFFS_Y: Gyro offsets of Y axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of Y axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS5_GYROFFS_Z: Gyro offsets of Z axis

*Note: This parameter is for advanced users*

Gyro sensor offsets of Z axis. This is setup on each boot during gyro calibrations

- Units: rad/s

- Calibration: 1

## INS5_GYR_CALTEMP: Calibration temperature for gyroscope

*Note: This parameter is for advanced users*

Temperature that the gyroscope was calibrated at

- Units: degC

- Calibration: 1

# INS5TCAL Parameters

## INS5_TCAL_ENABLE: Enable temperature calibration

*Note: This parameter is for advanced users*

Enable the use of temperature calibration parameters for this IMU. For automatic learning set to 2 and also set the INS_TCALn_TMAX to the target temperature, then reboot

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|LearnCalibration|

- RebootRequired: True

## INS5_TCAL_TMIN: Temperature calibration min

*Note: This parameter is for advanced users*

The minimum temperature that the calibration is valid for

- Range: -70 80

- Units: degC

- Calibration: 1

## INS5_TCAL_TMAX: Temperature calibration max

*Note: This parameter is for advanced users*

The maximum temperature that the calibration is valid for. This must be at least 10 degrees above TMIN for calibration

- Range: -70 80

- Units: degC

- Calibration: 1

## INS5_TCAL_ACC1_X: Accelerometer 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC1_Y: Accelerometer 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC1_Z: Accelerometer 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC2_X: Accelerometer 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC2_Y: Accelerometer 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC2_Z: Accelerometer 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC3_X: Accelerometer 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC3_Y: Accelerometer 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_ACC3_Z: Accelerometer 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR1_X: Gyroscope 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR1_Y: Gyroscope 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR1_Z: Gyroscope 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR2_X: Gyroscope 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR2_Y: Gyroscope 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR2_Z: Gyroscope 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR3_X: Gyroscope 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR3_Y: Gyroscope 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS5_TCAL_GYR3_Z: Gyroscope 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

# INSHNTC2 Parameters

## INS_HNTC2_ENABLE: Harmonic Notch Filter enable

*Note: This parameter is for advanced users*

Harmonic Notch Filter enable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS_HNTC2_FREQ: Harmonic Notch Filter base frequency

*Note: This parameter is for advanced users*

Harmonic Notch Filter base center frequency in Hz. This is the center frequency for static notches, the center frequency for Throttle based notches at the reference thrust value, and the minimum limit of center frequency variation for all other notch types. This should always be set lower than half the backend gyro rate (which is typically 1Khz). 

- Range: 10 495

- Units: Hz

## INS_HNTC2_BW: Harmonic Notch Filter bandwidth

*Note: This parameter is for advanced users*

Harmonic Notch Filter bandwidth in Hz. This is typically set to half the base frequency. The ratio of base frequency to bandwidth determines the notch quality factor and is fixed across harmonics.

- Range: 5 250

- Units: Hz

## INS_HNTC2_ATT: Harmonic Notch Filter attenuation

*Note: This parameter is for advanced users*

Harmonic Notch Filter attenuation in dB. Values greater than 40dB will typically produce a hard notch rather than a modest attenuation of motor noise.

- Range: 5 50

- Units: dB

## INS_HNTC2_HMNCS: Harmonic Notch Filter harmonics

*Note: This parameter is for advanced users*

Bitmask of harmonic frequencies to apply Harmonic Notch Filter to. This option takes effect on the next reboot. A value of 0 disables this filter. The first harmonic refers to the base frequency.

- Bitmask: 0:  1st harmonic, 1:  2nd harmonic, 2:  3rd harmonic, 3:  4th harmonic, 4:  5th harmonic, 5:  6th harmonic, 6:  7th harmonic, 7:  8th harmonic, 8:  9th harmonic, 9:  10th harmonic, 10: 11th harmonic, 11: 12th harmonic, 12: 13th harmonic, 13: 14th harmonic, 14: 15th harmonic, 15: 16th harmonic

- RebootRequired: True

## INS_HNTC2_REF: Harmonic Notch Filter reference value

*Note: This parameter is for advanced users*

A reference value of zero disables dynamic updates on the Harmonic Notch Filter and a positive value enables dynamic updates on the Harmonic Notch Filter.  For throttle-based scaling, this parameter is the reference value associated with the specified frequency to facilitate frequency scaling of the Harmonic Notch Filter. For RPM and ESC telemetry based tracking, this parameter is set to 1 to enable the Harmonic Notch Filter using the RPM sensor or ESC telemetry set to measure rotor speed.  The sensor data is converted to Hz automatically for use in the Harmonic Notch Filter.  This reference value may also be used to scale the sensor data, if required.  For example, rpm sensor data is required to measure heli motor RPM. Therefore the reference value can be used to scale the RPM sensor to the rotor RPM.

- Range: 0.0 1.0

- RebootRequired: True

## INS_HNTC2_MODE: Harmonic Notch Filter dynamic frequency tracking mode

*Note: This parameter is for advanced users*

Harmonic Notch Filter dynamic frequency tracking mode. Dynamic updates can be throttle, RPM sensor, ESC telemetry or dynamic FFT based. Throttle-based harmonic notch cannot be used on fixed wing only planes. It can for Copters, QuaadPlane(while in VTOL modes), and Rovers.

- Range: 0 5

|Value|Meaning|
|:---:|:---:|
|0|Fixed|
|1|Throttle|
|2|RPM Sensor|
|3|ESC Telemetry|
|4|Dynamic FFT|
|5|Second RPM Sensor|

## INS_HNTC2_OPTS: Harmonic Notch Filter options

*Note: This parameter is for advanced users*

Harmonic Notch Filter options. Triple and double-notches can provide deeper attenuation across a wider bandwidth with reduced latency than single notches and are suitable for larger aircraft. Multi-Source attaches a harmonic notch to each detected noise frequency instead of simply being multiples of the base frequency, in the case of FFT it will attach notches to each of three detected noise peaks, in the case of ESC it will attach notches to each of four motor RPM values. Loop rate update changes the notch center frequency at the scheduler loop rate rather than at the default of 200Hz. If both double and triple notches are specified only double notches will take effect.

- Bitmask: 0:Double notch,1:Multi-Source,2:Update at loop rate,3:EnableOnAllIMUs,4:Triple notch, 5:Use min freq on RPM source failure

- RebootRequired: True

## INS_HNTC2_FM_RAT: Throttle notch min freqency ratio

*Note: This parameter is for advanced users*

The minimum ratio below the configured frequency to take throttle based notch filters when flying at a throttle level below the reference throttle. Note that lower frequency notch filters will have more phase lag. If you want throttle based notch filtering to be effective at a throttle up to 30% below the configured notch frequency then set this parameter to 0.7. The default of 1.0 means the notch will not go below the frequency in the FREQ parameter.

- Range: 0.1 1.0

# INSHNTCH Parameters

## INS_HNTCH_ENABLE: Harmonic Notch Filter enable

*Note: This parameter is for advanced users*

Harmonic Notch Filter enable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## INS_HNTCH_FREQ: Harmonic Notch Filter base frequency

*Note: This parameter is for advanced users*

Harmonic Notch Filter base center frequency in Hz. This is the center frequency for static notches, the center frequency for Throttle based notches at the reference thrust value, and the minimum limit of center frequency variation for all other notch types. This should always be set lower than half the backend gyro rate (which is typically 1Khz). 

- Range: 10 495

- Units: Hz

## INS_HNTCH_BW: Harmonic Notch Filter bandwidth

*Note: This parameter is for advanced users*

Harmonic Notch Filter bandwidth in Hz. This is typically set to half the base frequency. The ratio of base frequency to bandwidth determines the notch quality factor and is fixed across harmonics.

- Range: 5 250

- Units: Hz

## INS_HNTCH_ATT: Harmonic Notch Filter attenuation

*Note: This parameter is for advanced users*

Harmonic Notch Filter attenuation in dB. Values greater than 40dB will typically produce a hard notch rather than a modest attenuation of motor noise.

- Range: 5 50

- Units: dB

## INS_HNTCH_HMNCS: Harmonic Notch Filter harmonics

*Note: This parameter is for advanced users*

Bitmask of harmonic frequencies to apply Harmonic Notch Filter to. This option takes effect on the next reboot. A value of 0 disables this filter. The first harmonic refers to the base frequency.

- Bitmask: 0:  1st harmonic, 1:  2nd harmonic, 2:  3rd harmonic, 3:  4th harmonic, 4:  5th harmonic, 5:  6th harmonic, 6:  7th harmonic, 7:  8th harmonic, 8:  9th harmonic, 9:  10th harmonic, 10: 11th harmonic, 11: 12th harmonic, 12: 13th harmonic, 13: 14th harmonic, 14: 15th harmonic, 15: 16th harmonic

- RebootRequired: True

## INS_HNTCH_REF: Harmonic Notch Filter reference value

*Note: This parameter is for advanced users*

A reference value of zero disables dynamic updates on the Harmonic Notch Filter and a positive value enables dynamic updates on the Harmonic Notch Filter.  For throttle-based scaling, this parameter is the reference value associated with the specified frequency to facilitate frequency scaling of the Harmonic Notch Filter. For RPM and ESC telemetry based tracking, this parameter is set to 1 to enable the Harmonic Notch Filter using the RPM sensor or ESC telemetry set to measure rotor speed.  The sensor data is converted to Hz automatically for use in the Harmonic Notch Filter.  This reference value may also be used to scale the sensor data, if required.  For example, rpm sensor data is required to measure heli motor RPM. Therefore the reference value can be used to scale the RPM sensor to the rotor RPM.

- Range: 0.0 1.0

- RebootRequired: True

## INS_HNTCH_MODE: Harmonic Notch Filter dynamic frequency tracking mode

*Note: This parameter is for advanced users*

Harmonic Notch Filter dynamic frequency tracking mode. Dynamic updates can be throttle, RPM sensor, ESC telemetry or dynamic FFT based. Throttle-based harmonic notch cannot be used on fixed wing only planes. It can for Copters, QuaadPlane(while in VTOL modes), and Rovers.

- Range: 0 5

|Value|Meaning|
|:---:|:---:|
|0|Fixed|
|1|Throttle|
|2|RPM Sensor|
|3|ESC Telemetry|
|4|Dynamic FFT|
|5|Second RPM Sensor|

## INS_HNTCH_OPTS: Harmonic Notch Filter options

*Note: This parameter is for advanced users*

Harmonic Notch Filter options. Triple and double-notches can provide deeper attenuation across a wider bandwidth with reduced latency than single notches and are suitable for larger aircraft. Multi-Source attaches a harmonic notch to each detected noise frequency instead of simply being multiples of the base frequency, in the case of FFT it will attach notches to each of three detected noise peaks, in the case of ESC it will attach notches to each of four motor RPM values. Loop rate update changes the notch center frequency at the scheduler loop rate rather than at the default of 200Hz. If both double and triple notches are specified only double notches will take effect.

- Bitmask: 0:Double notch,1:Multi-Source,2:Update at loop rate,3:EnableOnAllIMUs,4:Triple notch, 5:Use min freq on RPM source failure

- RebootRequired: True

## INS_HNTCH_FM_RAT: Throttle notch min freqency ratio

*Note: This parameter is for advanced users*

The minimum ratio below the configured frequency to take throttle based notch filters when flying at a throttle level below the reference throttle. Note that lower frequency notch filters will have more phase lag. If you want throttle based notch filtering to be effective at a throttle up to 30% below the configured notch frequency then set this parameter to 0.7. The default of 1.0 means the notch will not go below the frequency in the FREQ parameter.

- Range: 0.1 1.0

# INSLOG Parameters

## INS_LOG_BAT_CNT: sample count per batch

*Note: This parameter is for advanced users*

Number of samples to take when logging streams of IMU sensor readings.  Will be rounded down to a multiple of 32. This option takes effect on the next reboot.

- Increment: 32

- RebootRequired: True

## INS_LOG_BAT_MASK: Sensor Bitmask

*Note: This parameter is for advanced users*

Bitmap of which IMUs to log batch data for. This option takes effect on the next reboot.

- Bitmask: 0:IMU1,1:IMU2,2:IMU3

- RebootRequired: True

## INS_LOG_BAT_OPT: Batch Logging Options Mask

*Note: This parameter is for advanced users*

Options for the BatchSampler.

- Bitmask: 0:Sensor-Rate Logging (sample at full sensor rate seen by AP), 1: Sample post-filtering, 2: Sample pre- and post-filter

## INS_LOG_BAT_LGIN: logging interval

Interval between pushing samples to the AP_Logger log

- Units: ms

- Increment: 10

## INS_LOG_BAT_LGCT: logging count

Number of samples to push to count every INS_LOG_BAT_LGIN

- Increment: 1

# INSTCAL1 Parameters

## INS_TCAL1_ENABLE: Enable temperature calibration

*Note: This parameter is for advanced users*

Enable the use of temperature calibration parameters for this IMU. For automatic learning set to 2 and also set the INS_TCALn_TMAX to the target temperature, then reboot

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|LearnCalibration|

- RebootRequired: True

## INS_TCAL1_TMIN: Temperature calibration min

*Note: This parameter is for advanced users*

The minimum temperature that the calibration is valid for

- Range: -70 80

- Units: degC

- Calibration: 1

## INS_TCAL1_TMAX: Temperature calibration max

*Note: This parameter is for advanced users*

The maximum temperature that the calibration is valid for. This must be at least 10 degrees above TMIN for calibration

- Range: -70 80

- Units: degC

- Calibration: 1

## INS_TCAL1_ACC1_X: Accelerometer 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC1_Y: Accelerometer 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC1_Z: Accelerometer 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC2_X: Accelerometer 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC2_Y: Accelerometer 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC2_Z: Accelerometer 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC3_X: Accelerometer 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC3_Y: Accelerometer 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_ACC3_Z: Accelerometer 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR1_X: Gyroscope 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR1_Y: Gyroscope 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR1_Z: Gyroscope 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR2_X: Gyroscope 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR2_Y: Gyroscope 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR2_Z: Gyroscope 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR3_X: Gyroscope 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR3_Y: Gyroscope 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL1_GYR3_Z: Gyroscope 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

# INSTCAL2 Parameters

## INS_TCAL2_ENABLE: Enable temperature calibration

*Note: This parameter is for advanced users*

Enable the use of temperature calibration parameters for this IMU. For automatic learning set to 2 and also set the INS_TCALn_TMAX to the target temperature, then reboot

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|LearnCalibration|

- RebootRequired: True

## INS_TCAL2_TMIN: Temperature calibration min

*Note: This parameter is for advanced users*

The minimum temperature that the calibration is valid for

- Range: -70 80

- Units: degC

- Calibration: 1

## INS_TCAL2_TMAX: Temperature calibration max

*Note: This parameter is for advanced users*

The maximum temperature that the calibration is valid for. This must be at least 10 degrees above TMIN for calibration

- Range: -70 80

- Units: degC

- Calibration: 1

## INS_TCAL2_ACC1_X: Accelerometer 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC1_Y: Accelerometer 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC1_Z: Accelerometer 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC2_X: Accelerometer 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC2_Y: Accelerometer 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC2_Z: Accelerometer 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC3_X: Accelerometer 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC3_Y: Accelerometer 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_ACC3_Z: Accelerometer 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR1_X: Gyroscope 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR1_Y: Gyroscope 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR1_Z: Gyroscope 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR2_X: Gyroscope 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR2_Y: Gyroscope 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR2_Z: Gyroscope 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR3_X: Gyroscope 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR3_Y: Gyroscope 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL2_GYR3_Z: Gyroscope 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

# INSTCAL3 Parameters

## INS_TCAL3_ENABLE: Enable temperature calibration

*Note: This parameter is for advanced users*

Enable the use of temperature calibration parameters for this IMU. For automatic learning set to 2 and also set the INS_TCALn_TMAX to the target temperature, then reboot

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|LearnCalibration|

- RebootRequired: True

## INS_TCAL3_TMIN: Temperature calibration min

*Note: This parameter is for advanced users*

The minimum temperature that the calibration is valid for

- Range: -70 80

- Units: degC

- Calibration: 1

## INS_TCAL3_TMAX: Temperature calibration max

*Note: This parameter is for advanced users*

The maximum temperature that the calibration is valid for. This must be at least 10 degrees above TMIN for calibration

- Range: -70 80

- Units: degC

- Calibration: 1

## INS_TCAL3_ACC1_X: Accelerometer 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC1_Y: Accelerometer 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC1_Z: Accelerometer 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC2_X: Accelerometer 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC2_Y: Accelerometer 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC2_Z: Accelerometer 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC3_X: Accelerometer 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC3_Y: Accelerometer 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_ACC3_Z: Accelerometer 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR1_X: Gyroscope 1st order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR1_Y: Gyroscope 1st order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR1_Z: Gyroscope 1st order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 1st order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR2_X: Gyroscope 2nd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR2_Y: Gyroscope 2nd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR2_Z: Gyroscope 2nd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 2nd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR3_X: Gyroscope 3rd order temperature coefficient X axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR3_Y: Gyroscope 3rd order temperature coefficient Y axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

## INS_TCAL3_GYR3_Z: Gyroscope 3rd order temperature coefficient Z axis

*Note: This parameter is for advanced users*

This is the 3rd order temperature coefficient from a temperature calibration

- Calibration: 1

# KDE Parameters

## KDE_NPOLE: Number of motor poles

Sets the number of motor poles to calculate the correct RPM value

# LOG Parameters

## LOG_BACKEND_TYPE: AP_Logger Backend Storage type

Bitmap of what Logger backend types to enable. Block-based logging is available on SITL and boards with dataflash chips. Multiple backends can be selected.

- Bitmask: 0:File,1:MAVLink,2:Block

## LOG_FILE_BUFSIZE: Logging File and Block Backend buffer size max (in kilobytes)

The File and Block backends use a buffer to store data before writing to the block device.  Raising this value may reduce "gaps" in your SD card logging but increases memory usage.  This buffer size may be reduced to free up available memory

- Units: kB

- Range: 4 200

## LOG_DISARMED: Enable logging while disarmed

If LOG_DISARMED is set to 1 then logging will be enabled at all times including when disarmed. Logging before arming can make for very large logfiles but can help a lot when tracking down startup issues and is necessary if logging of EKF replay data is selected via the LOG_REPLAY parameter. If LOG_DISARMED is set to 2, then logging will be enabled when disarmed, but not if a USB connection is detected. This can be used to prevent unwanted data logs being generated when the vehicle is connected via USB for log downloading or parameter changes. If LOG_DISARMED is set to 3 then logging will happen while disarmed, but if the vehicle never arms then the logs using the filesystem backend will be discarded on the next boot.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|
|2|Disabled on USB connection|
|3|Discard log on reboot if never armed|

## LOG_REPLAY: Enable logging of information needed for Replay

If LOG_REPLAY is set to 1 then the EKF2 and EKF3 state estimators will log detailed information needed for diagnosing problems with the Kalman filter. LOG_DISARMED must be set to 1 or 2 or else the log will not contain the pre-flight data required for replay testing of the EKF's. It is suggested that you also raise LOG_FILE_BUFSIZE to give more buffer space for logging and use a high quality microSD card to ensure no sensor data is lost.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## LOG_FILE_DSRMROT: Stop logging to current file on disarm

When set, the current log file is closed when the vehicle is disarmed.  If LOG_DISARMED is set then a fresh log will be opened. Applies to the File and Block logging backends.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## LOG_MAV_BUFSIZE: Maximum AP_Logger MAVLink Backend buffer size

*Note: This parameter is for advanced users*

Maximum amount of memory to allocate to AP_Logger-over-mavlink

- Units: kB

## LOG_FILE_TIMEOUT: Timeout before giving up on file writes

This controls the amount of time before failing writes to a log file cause the file to be closed and logging stopped.

- Units: s

## LOG_FILE_MB_FREE: Old logs on the SD card will be deleted to maintain this amount of free space

Set this such that the free space is larger than your largest typical flight log

- Units: MB

- Range: 10 1000

## LOG_FILE_RATEMAX: Maximum logging rate for file backend

This sets the maximum rate that streaming log messages will be logged to the file backend. A value of zero means that rate limiting is disabled.

- Units: Hz

- Range: 0 1000

- Increment: 0.1

## LOG_MAV_RATEMAX: Maximum logging rate for mavlink backend

This sets the maximum rate that streaming log messages will be logged to the mavlink backend. A value of zero means that rate limiting is disabled.

- Units: Hz

- Range: 0 1000

- Increment: 0.1

## LOG_BLK_RATEMAX: Maximum logging rate for block backend

This sets the maximum rate that streaming log messages will be logged to the block backend. A value of zero means that rate limiting is disabled.

- Units: Hz

- Range: 0 1000

- Increment: 0.1

## LOG_DARM_RATEMAX: Maximum logging rate when disarmed

This sets the maximum rate that streaming log messages will be logged to any backend when disarmed. A value of zero means that the normal backend rate limit is applied.

- Units: Hz

- Range: 0 1000

- Increment: 0.1

## LOG_MAX_FILES: Maximum number of log files

*Note: This parameter is for advanced users*

This sets the maximum number of log file that will be written on dataflash or sd card before starting to rotate log number. Limit is capped at 500 logs.

- Range: 2 500

- Increment: 1

- RebootRequired: True

# MIS Parameters

## MIS_TOTAL: Total mission commands

*Note: This parameter is for advanced users*

The number of mission mission items that has been loaded by the ground station. Do not change this manually.

- Range: 0 32766

- Increment: 1

- ReadOnly: True

## MIS_RESTART: Mission Restart when entering Auto mode

*Note: This parameter is for advanced users*

Controls mission starting point when entering Auto mode (either restart from beginning of mission or resume from last command run)

|Value|Meaning|
|:---:|:---:|
|0|Resume Mission|
|1|Restart Mission|

## MIS_OPTIONS: Mission options bitmask

*Note: This parameter is for advanced users*

Bitmask of what options to use in missions.

- Bitmask: 0:Clear Mission on reboot

# MNT1 Parameters

## MNT1_TYPE: Mount Type

Mount Type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Servo|
|2|3DR Solo|
|3|Alexmos Serial|
|4|SToRM32 MAVLink|
|5|SToRM32 Serial|
|6|Gremsy|
|7|BrushlessPWM|
|8|Siyi|
|9|Scripting|
|10|Xacti|
|11|Viewpro|
|12|Topotek|
|13|CADDX|

- RebootRequired: True

## MNT1_DEFLT_MODE: Mount default operating mode

Mount default operating mode on startup and after control is returned from autopilot

|Value|Meaning|
|:---:|:---:|
|0|Retracted|
|1|Neutral|
|2|MavLink Targeting|
|3|RC Targeting|
|4|GPS Point|
|5|SysID Target|
|6|Home Location|

## MNT1_RC_RATE: Mount RC Rate

Pilot rate control's maximum rate.  Set to zero to use angle control

- Units: deg/s

- Range: 0 90

- Increment: 1

## MNT1_ROLL_MIN: Mount Roll angle minimum

Mount Roll angle minimum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT1_ROLL_MAX: Mount Roll angle maximum

Mount Roll angle maximum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT1_PITCH_MIN: Mount Pitch angle minimum

Mount Pitch angle minimum

- Units: deg

- Range: -90 90

- Increment: 1

## MNT1_PITCH_MAX: Mount Pitch angle maximum

Mount Pitch angle maximum

- Units: deg

- Range: -90 90

- Increment: 1

## MNT1_YAW_MIN: Mount Yaw angle minimum

Mount Yaw angle minimum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT1_YAW_MAX: Mount Yaw angle maximum

Mount Yaw angle maximum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT1_RETRACT_X: Mount roll angle when in retracted position

Mount roll angle when in retracted position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT1_RETRACT_Y: Mount pitch angle when in retracted position

Mount pitch angle when in retracted position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT1_RETRACT_Z: Mount yaw angle when in retracted position

Mount yaw angle when in retracted position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT1_NEUTRAL_X: Mount roll angle when in neutral position

Mount roll angle when in neutral position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT1_NEUTRAL_Y: Mount pitch angle when in neutral position

Mount pitch angle when in neutral position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT1_NEUTRAL_Z: Mount yaw angle when in neutral position

Mount yaw angle when in neutral position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT1_LEAD_RLL: Mount Roll stabilization lead time

Servo mount roll angle output leads the vehicle angle by this amount of time based on current roll rate. Increase until the servo is responsive but does not overshoot

- Units: s

- Range: 0.0 0.2

- Increment: .005

## MNT1_LEAD_PTCH: Mount Pitch stabilization lead time

Servo mount pitch angle output leads the vehicle angle by this amount of time based on current pitch rate. Increase until the servo is responsive but does not overshoot

- Units: s

- Range: 0.0 0.2

- Increment: .005

## MNT1_SYSID_DFLT: Mount Target sysID

Default Target sysID for the mount to point to

- RebootRequired: True

## MNT1_DEVID: Mount Device ID

*Note: This parameter is for advanced users*

Mount device ID, taking into account its type, bus and instance

## MNT1_OPTIONS: Mount options

Mount options bitmask

- Bitmask: 0:RC lock state from previous mode

# MNT2 Parameters

## MNT2_TYPE: Mount Type

Mount Type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Servo|
|2|3DR Solo|
|3|Alexmos Serial|
|4|SToRM32 MAVLink|
|5|SToRM32 Serial|
|6|Gremsy|
|7|BrushlessPWM|
|8|Siyi|
|9|Scripting|
|10|Xacti|
|11|Viewpro|
|12|Topotek|
|13|CADDX|

- RebootRequired: True

## MNT2_DEFLT_MODE: Mount default operating mode

Mount default operating mode on startup and after control is returned from autopilot

|Value|Meaning|
|:---:|:---:|
|0|Retracted|
|1|Neutral|
|2|MavLink Targeting|
|3|RC Targeting|
|4|GPS Point|
|5|SysID Target|
|6|Home Location|

## MNT2_RC_RATE: Mount RC Rate

Pilot rate control's maximum rate.  Set to zero to use angle control

- Units: deg/s

- Range: 0 90

- Increment: 1

## MNT2_ROLL_MIN: Mount Roll angle minimum

Mount Roll angle minimum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT2_ROLL_MAX: Mount Roll angle maximum

Mount Roll angle maximum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT2_PITCH_MIN: Mount Pitch angle minimum

Mount Pitch angle minimum

- Units: deg

- Range: -90 90

- Increment: 1

## MNT2_PITCH_MAX: Mount Pitch angle maximum

Mount Pitch angle maximum

- Units: deg

- Range: -90 90

- Increment: 1

## MNT2_YAW_MIN: Mount Yaw angle minimum

Mount Yaw angle minimum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT2_YAW_MAX: Mount Yaw angle maximum

Mount Yaw angle maximum

- Units: deg

- Range: -180 180

- Increment: 1

## MNT2_RETRACT_X: Mount roll angle when in retracted position

Mount roll angle when in retracted position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT2_RETRACT_Y: Mount pitch angle when in retracted position

Mount pitch angle when in retracted position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT2_RETRACT_Z: Mount yaw angle when in retracted position

Mount yaw angle when in retracted position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT2_NEUTRAL_X: Mount roll angle when in neutral position

Mount roll angle when in neutral position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT2_NEUTRAL_Y: Mount pitch angle when in neutral position

Mount pitch angle when in neutral position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT2_NEUTRAL_Z: Mount yaw angle when in neutral position

Mount yaw angle when in neutral position

- Units: deg

- Range: -180.0 180.0

- Increment: 1

## MNT2_LEAD_RLL: Mount Roll stabilization lead time

Servo mount roll angle output leads the vehicle angle by this amount of time based on current roll rate. Increase until the servo is responsive but does not overshoot

- Units: s

- Range: 0.0 0.2

- Increment: .005

## MNT2_LEAD_PTCH: Mount Pitch stabilization lead time

Servo mount pitch angle output leads the vehicle angle by this amount of time based on current pitch rate. Increase until the servo is responsive but does not overshoot

- Units: s

- Range: 0.0 0.2

- Increment: .005

## MNT2_SYSID_DFLT: Mount Target sysID

Default Target sysID for the mount to point to

- RebootRequired: True

## MNT2_DEVID: Mount Device ID

*Note: This parameter is for advanced users*

Mount device ID, taking into account its type, bus and instance

## MNT2_OPTIONS: Mount options

Mount options bitmask

- Bitmask: 0:RC lock state from previous mode

# MOT Parameters

## MOT_PWM_TYPE: Motor Output PWM type

*Note: This parameter is for advanced users*

This selects the output PWM type as regular PWM, OneShot, Brushed motor support using PWM (duty cycle) with separated direction signal, Brushed motor support with separate throttle and direction PWM (duty cyle)

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|OneShot|
|2|OneShot125|
|3|BrushedWithRelay|
|4|BrushedBiPolar|
|5|DShot150|
|6|DShot300|
|7|DShot600|
|8|DShot1200|

- RebootRequired: True

## MOT_PWM_FREQ: Motor Output PWM freq for brushed motors

*Note: This parameter is for advanced users*

Motor Output PWM freq for brushed motors

- Units: kHz

- Range: 1 20

- Increment: 1

- RebootRequired: True

## MOT_SAFE_DISARM: Motor PWM output disabled when disarmed

*Note: This parameter is for advanced users*

Disables motor PWM output when disarmed

|Value|Meaning|
|:---:|:---:|
|0|PWM enabled while disarmed|
|1|PWM disabled while disarmed|

## MOT_THR_MIN: Throttle minimum

Throttle minimum percentage the autopilot will apply. This is useful for handling a deadzone around low throttle and for preventing internal combustion motors cutting out during missions.

- Units: %

- Range: 0 20

- Increment: 1

## MOT_THR_MAX: Throttle maximum

Throttle maximum percentage the autopilot will apply. This can be used to prevent overheating an ESC or motor on an electric rover

- Units: %

- Range: 30 100

- Increment: 1

## MOT_SLEWRATE: Throttle slew rate

Throttle slew rate as a percentage of total range per second. A value of 100 allows the motor to change over its full range in one second.  A value of zero disables the limit.  Note some NiMH powered rovers require a lower setting of 40 to reduce current demand to avoid brownouts.

- Units: %/s

- Range: 0 1000

- Increment: 1

## MOT_THST_EXPO: Thrust Curve Expo

*Note: This parameter is for advanced users*

Thrust curve exponent (-1 to +1 with 0 being linear)

- Range: -1.0 1.0

## MOT_SPD_SCA_BASE: Motor speed scaling base speed

*Note: This parameter is for advanced users*

Speed above which steering is scaled down when using regular steering/throttle vehicles.  zero to disable speed scaling

- Units: m/s

- Range: 0 10

## MOT_STR_THR_MIX: Motor steering vs throttle prioritisation

*Note: This parameter is for advanced users*

Steering vs Throttle priorisation.  Higher numbers prioritise steering, lower numbers prioritise throttle.  Only valid for Skid Steering vehicles

- Range: 0.2 1.0

## MOT_VEC_ANGLEMAX: Vector thrust angle max

The angle between steering's middle position and maximum position when using vectored thrust (boats only)

- Units: deg

- Range: 0 90

## MOT_THST_ASYM: Motor Thrust Asymmetry

*Note: This parameter is for advanced users*

Thrust Asymetry. Used for skid-steering. 2.0 means your motors move twice as fast forward than they do backwards.

- Range: 1.0 10.0

# MSP Parameters

## MSP_OSD_NCELLS: Cell count override

Used for average cell voltage calculation

|Value|Meaning|
|:---:|:---:|
|0|Auto|
|1|1|
|2|2|
|3|3|
|4|4|
|5|5|
|6|6|
|7|7|
|8|8|
|9|9|
|10|10|
|11|11|
|12|12|
|13|13|
|14|14|

## MSP_OPTIONS: MSP OSD Options

A bitmask to set some MSP specific options: EnableTelemetryMode-allows "push" mode telemetry when only rx line of OSD ic connected to autopilot,  EnableBTFLFonts-uses indexes corresponding to Betaflight fonts if OSD uses those instead of ArduPilot fonts.

- Bitmask: 0:EnableTelemetryMode, 1: unused, 2:EnableBTFLFonts

# NET Parameters

## NET_ENABLE: Networking Enable

*Note: This parameter is for advanced users*

Networking Enable

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

- RebootRequired: True

## NET_NETMASK: IP Subnet mask

*Note: This parameter is for advanced users*

Allows setting static subnet mask. The value is a count of consecutive bits. Examples: 24 = 255.255.255.0, 16 = 255.255.0.0

- Range: 0 32

- RebootRequired: True

## NET_DHCP: DHCP client

*Note: This parameter is for advanced users*

Enable/Disable DHCP client

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

- RebootRequired: True

## NET_TESTS: Test enable flags

*Note: This parameter is for advanced users*

Enable/Disable networking tests

- Bitmask: 0:UDP echo test,1:TCP echo test, 2:TCP discard test, 3:TCP reflect test

- RebootRequired: True

## NET_OPTIONS: Networking options

*Note: This parameter is for advanced users*

Networking options

- Bitmask: 0:EnablePPP Ethernet gateway, 1:Enable CAN1 multicast endpoint, 2:Enable CAN2 multicast endpoint, 3:Enable CAN1 multicast bridged, 4:Enable CAN2 multicast bridged

- RebootRequired: True

# NETGWADDR Parameters

## NET_GWADDR0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_GWADDR1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_GWADDR2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_GWADDR3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETIPADDR Parameters

## NET_IPADDR0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_IPADDR1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_IPADDR2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_IPADDR3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETMACADDR Parameters

## NET_MACADDR0: MAC Address 1st byte

*Note: This parameter is for advanced users*

MAC address 1st byte

- Range: 0 255

- RebootRequired: True

## NET_MACADDR1: MAC Address 2nd byte

*Note: This parameter is for advanced users*

MAC address 2nd byte

- Range: 0 255

- RebootRequired: True

## NET_MACADDR2: MAC Address 3rd byte

*Note: This parameter is for advanced users*

MAC address 3rd byte

- Range: 0 255

- RebootRequired: True

## NET_MACADDR3: MAC Address 4th byte

*Note: This parameter is for advanced users*

MAC address 4th byte

- Range: 0 255

- RebootRequired: True

## NET_MACADDR4: MAC Address 5th byte

*Note: This parameter is for advanced users*

MAC address 5th byte

- Range: 0 255

- RebootRequired: True

## NET_MACADDR5: MAC Address 6th byte

*Note: This parameter is for advanced users*

MAC address 6th byte

- Range: 0 255

- RebootRequired: True

# NETP1 Parameters

## NET_P1_TYPE: Port type

*Note: This parameter is for advanced users*

Port type for network serial port. For the two client types a valid destination IP address must be set. For the two server types either 0.0.0.0 or a local address can be used. The UDP client type will use broadcast if the IP is set to 255.255.255.255 and will use UDP multicast if the IP is in the multicast address range.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|UDP client|
|2|UDP server|
|3|TCP client|
|4|TCP server|

- RebootRequired: True

## NET_P1_PROTOCOL: Protocol

*Note: This parameter is for advanced users*

Networked serial port protocol

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## NET_P1_PORT: Port number

*Note: This parameter is for advanced users*

Port number

- Range: 0 65535

- RebootRequired: True

# NETP1IP Parameters

## NET_P1_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P1_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P1_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_P1_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETP2 Parameters

## NET_P2_TYPE: Port type

*Note: This parameter is for advanced users*

Port type for network serial port. For the two client types a valid destination IP address must be set. For the two server types either 0.0.0.0 or a local address can be used. The UDP client type will use broadcast if the IP is set to 255.255.255.255 and will use UDP multicast if the IP is in the multicast address range.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|UDP client|
|2|UDP server|
|3|TCP client|
|4|TCP server|

- RebootRequired: True

## NET_P2_PROTOCOL: Protocol

*Note: This parameter is for advanced users*

Networked serial port protocol

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## NET_P2_PORT: Port number

*Note: This parameter is for advanced users*

Port number

- Range: 0 65535

- RebootRequired: True

# NETP2IP Parameters

## NET_P2_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P2_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P2_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_P2_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETP3 Parameters

## NET_P3_TYPE: Port type

*Note: This parameter is for advanced users*

Port type for network serial port. For the two client types a valid destination IP address must be set. For the two server types either 0.0.0.0 or a local address can be used. The UDP client type will use broadcast if the IP is set to 255.255.255.255 and will use UDP multicast if the IP is in the multicast address range.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|UDP client|
|2|UDP server|
|3|TCP client|
|4|TCP server|

- RebootRequired: True

## NET_P3_PROTOCOL: Protocol

*Note: This parameter is for advanced users*

Networked serial port protocol

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## NET_P3_PORT: Port number

*Note: This parameter is for advanced users*

Port number

- Range: 0 65535

- RebootRequired: True

# NETP3IP Parameters

## NET_P3_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P3_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P3_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_P3_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETP4 Parameters

## NET_P4_TYPE: Port type

*Note: This parameter is for advanced users*

Port type for network serial port. For the two client types a valid destination IP address must be set. For the two server types either 0.0.0.0 or a local address can be used. The UDP client type will use broadcast if the IP is set to 255.255.255.255 and will use UDP multicast if the IP is in the multicast address range.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|UDP client|
|2|UDP server|
|3|TCP client|
|4|TCP server|

- RebootRequired: True

## NET_P4_PROTOCOL: Protocol

*Note: This parameter is for advanced users*

Networked serial port protocol

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## NET_P4_PORT: Port number

*Note: This parameter is for advanced users*

Port number

- Range: 0 65535

- RebootRequired: True

# NETP4IP Parameters

## NET_P4_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P4_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_P4_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_P4_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETREMPPPIP Parameters

## NET_REMPPP_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_REMPPP_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_REMPPP_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_REMPPP_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NETTESTIP Parameters

## NET_TEST_IP0: IPv4 Address 1st byte

IPv4 address. Example: 192.xxx.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_TEST_IP1: IPv4 Address 2nd byte

IPv4 address. Example: xxx.168.xxx.xxx

- Range: 0 255

- RebootRequired: True

## NET_TEST_IP2: IPv4 Address 3rd byte

IPv4 address. Example: xxx.xxx.144.xxx

- Range: 0 255

- RebootRequired: True

## NET_TEST_IP3: IPv4 Address 4th byte

IPv4 address. Example: xxx.xxx.xxx.14

- Range: 0 255

- RebootRequired: True

# NMEA Parameters

## NMEA_RATE_MS: NMEA Output rate

NMEA Output rate. This controls the interval at which all the enabled NMEA messages are sent. Most NMEA systems expect 100ms (10Hz) or slower.

- Range: 20 2000

- Increment: 1

- Units: ms

## NMEA_MSG_EN: Messages Enable bitmask

This is a bitmask of enabled NMEA messages. All messages will be sent consecutively at the same rate interval

- Bitmask: 0:GPGGA,1:GPRMC,2:PASHR

# NTF Parameters

## NTF_LED_BRIGHT: LED Brightness

*Note: This parameter is for advanced users*

Select the RGB LED brightness level. When USB is connected brightness will never be higher than low regardless of the setting.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|Low|
|2|Medium|
|3|High|

## NTF_BUZZ_TYPES: Buzzer Driver Types

*Note: This parameter is for advanced users*

Controls what types of Buzzer will be enabled

- Bitmask: 0:Built-in buzzer, 1:DShot, 2:DroneCAN

## NTF_LED_OVERRIDE: Specifies colour source for the RGBLed

*Note: This parameter is for advanced users*

Specifies the source for the colours and brightness for the LED.  OutbackChallenge conforms to the MedicalExpress (https://uavchallenge.org/medical-express/) rules, essentially "Green" is disarmed (safe-to-approach), "Red" is armed (not safe-to-approach). Traffic light is a simplified color set, red when armed, yellow when the safety switch is not surpressing outputs (but disarmed), and green when outputs are surpressed and disarmed, the LED will blink faster if disarmed and failing arming checks.

|Value|Meaning|
|:---:|:---:|
|0|Standard|
|1|MAVLink/Scripting/AP_Periph|
|2|OutbackChallenge|
|3|TrafficLight|

## NTF_DISPLAY_TYPE: Type of on-board I2C display

*Note: This parameter is for advanced users*

This sets up the type of on-board I2C display. Disabled by default.

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|ssd1306|
|2|sh1106|
|10|SITL|

## NTF_OREO_THEME: OreoLED Theme

*Note: This parameter is for advanced users*

Enable/Disable Solo Oreo LED driver, 0 to disable, 1 for Aircraft theme, 2 for Rover theme

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Aircraft|
|2|Rover|

## NTF_BUZZ_PIN: Buzzer pin

*Note: This parameter is for advanced users*

Enables to connect active buzzer to arbitrary pin. Requires 3-pin buzzer or additional MOSFET! Some the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|

## NTF_LED_TYPES: LED Driver Types

*Note: This parameter is for advanced users*

Controls what types of LEDs will be enabled

- Bitmask: 0:Built-in LED, 1:Internal ToshibaLED, 2:External ToshibaLED, 3:External PCA9685, 4:Oreo LED, 5:DroneCAN, 6:NCP5623 External, 7:NCP5623 Internal, 8:NeoPixel, 9:ProfiLED, 10:Scripting, 11:DShot, 12:ProfiLED_SPI, 13:LP5562 External, 14: LP5562 Internal, 15:IS31FL3195 External, 16: IS31FL3195 Internal, 17: DiscreteRGB, 18: NeoPixelRGB

## NTF_BUZZ_ON_LVL: Buzzer-on pin logic level

*Note: This parameter is for advanced users*

Specifies pin level that indicates buzzer should play

|Value|Meaning|
|:---:|:---:|
|0|LowIsOn|
|1|HighIsOn|

## NTF_BUZZ_VOLUME: Buzzer volume

Control the volume of the buzzer

- Range: 0 100

- Units: %

## NTF_LED_LEN: Serial LED String Length

*Note: This parameter is for advanced users*

The number of Serial LED's to use for notifications (NeoPixel's and ProfiLED)

- Range: 1 32

- RebootRequired: True

# OA Parameters

## OA_TYPE: Object Avoidance Path Planning algorithm to use

Enabled/disable path planning around obstacles

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|BendyRuler|
|2|Dijkstra|
|3|Dijkstra with BendyRuler|

## OA_MARGIN_MAX: Object Avoidance wide margin distance

Object Avoidance will ignore objects more than this many meters from vehicle

- Units: m

- Range: 0.1 100

- Increment: 1

## OA_OPTIONS: Options while recovering from Object Avoidance

Bitmask which will govern vehicles behaviour while recovering from Obstacle Avoidance (i.e Avoidance is turned off after the path ahead is clear).   

- Bitmask: 0: Reset the origin of the waypoint to the present location, 1: log Dijkstra points

# OABR Parameters

## OA_BR_LOOKAHEAD: Object Avoidance look ahead distance maximum

Object Avoidance will look this many meters ahead of vehicle

- Units: m

- Range: 1 100

- Increment: 1

## OA_BR_CONT_RATIO: Obstacle Avoidance margin ratio for BendyRuler to change bearing significantly 

 BendyRuler will avoid changing bearing unless ratio of previous margin from obstacle (or fence) to present calculated margin is atleast this much.

- Range: 1.1 2

- Increment: 0.1

## OA_BR_CONT_ANGLE: BendyRuler's bearing change resistance threshold angle   

 BendyRuler will resist changing current bearing if the change in bearing is over this angle

- Range: 20 180

- Increment: 5

# OADB Parameters

## OA_DB_SIZE: OADatabase maximum number of points

*Note: This parameter is for advanced users*

OADatabase maximum number of points. Set to 0 to disable the OA Database. Larger means more points but is more cpu intensive to process

- Range: 0 10000

- RebootRequired: True

## OA_DB_EXPIRE: OADatabase item timeout

*Note: This parameter is for advanced users*

OADatabase item timeout. The time an item will linger without any updates before it expires. Zero means never expires which is useful for a sent-once static environment but terrible for dynamic ones.

- Units: s

- Range: 0 127

- Increment: 1

## OA_DB_QUEUE_SIZE: OADatabase queue maximum number of points

*Note: This parameter is for advanced users*

OADatabase queue maximum number of points. This in an input buffer size. Larger means it can handle larger bursts of incoming data points to filter into the database. No impact on cpu, only RAM. Recommend larger for faster datalinks or for sensors that generate a lot of data.

- Range: 1 200

- RebootRequired: True

## OA_DB_OUTPUT: OADatabase output level

*Note: This parameter is for advanced users*

OADatabase output level to configure which database objects are sent to the ground station. All data is always available internally for avoidance algorithms.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Send only HIGH importance items|
|2|Send HIGH and NORMAL importance items|
|3|Send all items|

## OA_DB_BEAM_WIDTH: OADatabase beam width

*Note: This parameter is for advanced users*

Beam width of incoming lidar data

- Units: deg

- Range: 1 10

- RebootRequired: True

## OA_DB_RADIUS_MIN: OADatabase Minimum  radius

*Note: This parameter is for advanced users*

Minimum radius of objects held in database

- Units: m

- Range: 0 10

## OA_DB_DIST_MAX: OADatabase Distance Maximum

*Note: This parameter is for advanced users*

Maximum distance of objects held in database.  Set to zero to disable the limits

- Units: m

- Range: 0 10

# OSD Parameters

## OSD_TYPE: OSD type

OSD type. TXONLY makes the OSD parameter selection available to other modules even if there is no native OSD support on the board, for instance CRSF.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MAX7456|
|2|SITL|
|3|MSP|
|4|TXONLY|
|5|MSP_DISPLAYPORT|

- RebootRequired: True

## OSD_CHAN: Screen switch transmitter channel

This sets the channel used to switch different OSD screens.

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|5|Chan5|
|6|Chan6|
|7|Chan7|
|8|Chan8|
|9|Chan9|
|10|Chan10|
|11|Chan11|
|12|Chan12|
|13|Chan13|
|14|Chan14|
|15|Chan15|
|16|Chan16|

## OSD_SW_METHOD: Screen switch method

This sets the method used to switch different OSD screens.

|Value|Meaning|
|:---:|:---:|
|0|switch to next screen if channel value was changed|
|1|select screen based on pwm ranges specified for each screen|
|2|switch to next screen after low to high transition and every 1s while channel value is high|

## OSD_OPTIONS: OSD Options

This sets options that change the display

- Bitmask: 0:UseDecimalPack, 1:InvertedWindArrow, 2:InvertedAHRoll, 3:Convert feet to miles at 5280ft instead of 10000ft, 4:DisableCrosshair, 5:TranslateArrows, 6:AviationStyleAH, 7:Prefix LQ with RF Mode

## OSD_FONT: OSD Font

This sets which OSD font to use. It is an integer from 0 to the number of fonts available

- RebootRequired: True

## OSD_V_OFFSET: OSD vertical offset

Sets vertical offset of the osd inside image

- Range: 0 31

- RebootRequired: True

## OSD_H_OFFSET: OSD horizontal offset

Sets horizontal offset of the osd inside image

- Range: 0 63

- RebootRequired: True

## OSD_W_RSSI: RSSI warn level (in %)

Set level at which RSSI item will flash (in positive % or negative dBm values as applicable). 30% or -100dBm are defaults.

- Range: -128 100

## OSD_W_NSAT: NSAT warn level

Set level at which NSAT item will flash

- Range: 1 30

## OSD_W_BATVOLT: BAT_VOLT warn level

Set level at which BAT_VOLT item will flash

- Range: 0 100

## OSD_UNITS: Display Units

Sets the units to use in displaying items

|Value|Meaning|
|:---:|:---:|
|0|Metric|
|1|Imperial|
|2|SI|
|3|Aviation|

## OSD_MSG_TIME: Message display duration in seconds

Sets message duration seconds

- Range: 1 20

## OSD_ARM_SCR: Arm screen

Screen to be shown on Arm event. Zero to disable the feature.

- Range: 0 4

## OSD_DSARM_SCR: Disarm screen

Screen to be shown on disarm event. Zero to disable the feature.

- Range: 0 4

## OSD_FS_SCR: Failsafe screen

Screen to be shown on failsafe event. Zero to disable the feature.

- Range: 0 4

## OSD_BTN_DELAY: Button delay

*Note: This parameter is for advanced users*

Debounce time in ms for stick commanded parameter navigation.

- Range: 0 3000

## OSD_W_TERR: Terrain warn level

Set level below which TER_HGT item will flash. -1 disables.

- Range: -1 3000

- Units: m

## OSD_W_AVGCELLV: AVGCELLV warn level

Set level at which AVGCELLV item will flash

- Range: 0 100

## OSD_CELL_COUNT: Battery cell count

*Note: This parameter is for advanced users*

Used for average cell voltage display. -1 disables, 0 uses cell count autodetection for well charged LIPO/LIION batteries at connection, other values manually select cell count used.

- Increment: 1

## OSD_W_RESTVOLT: RESTVOLT warn level

Set level at which RESTVOLT item will flash

- Range: 0 100

## OSD_W_ACRVOLT: Avg Cell Resting Volt warn level

Set level at which ACRVOLT item will flash

- Range: 0 100

## OSD_W_LQ: RC link quality warn level (in %)

Set level at which RC_LQ item will flash (%)

- Range: 0 100

## OSD_W_SNR: RC link SNR warn level (in %)

Set level at which RC_SNR item will flash (in db)

- Range: -20 10

## OSD_SB_H_OFS: Sidebar horizontal offset

Extends the spacing between the sidebar elements by this amount of columns. Positive values increases the width to the right of the screen.

- Range: 0 20

## OSD_SB_V_EXT: Sidebar vertical extension

Increase of vertical length of the sidebar itens by this amount of lines. Applied equally both above and below the default setting.

- Range: 0 10

## OSD_TYPE2: OSD type 2

OSD type 2. TXONLY makes the OSD parameter selection available to other modules even if there is no native OSD support on the board, for instance CRSF.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MAX7456|
|2|SITL|
|3|MSP|
|4|TXONLY|
|5|MSP_DISPLAYPORT|

- RebootRequired: True

# OSD1 Parameters

## OSD1_ENABLE: Enable screen

Enable this screen

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CHAN_MIN: Transmitter switch screen minimum pwm

This sets the PWM lower limit for this screen

- Range: 900 2100

## OSD1_CHAN_MAX: Transmitter switch screen maximum pwm

This sets the PWM upper limit for this screen

- Range: 900 2100

## OSD1_ALTITUDE_EN: ALTITUDE_EN

Enables display of altitude AGL

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ALTITUDE_X: ALTITUDE_X

Horizontal position on screen

- Range: 0 59

## OSD1_ALTITUDE_Y: ALTITUDE_Y

Vertical position on screen

- Range: 0 21

## OSD1_BAT_VOLT_EN: BATVOLT_EN

Displays main battery voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_BAT_VOLT_X: BATVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD1_BAT_VOLT_Y: BATVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD1_RSSI_EN: RSSI_EN

Displays RC signal strength

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RSSI_X: RSSI_X

Horizontal position on screen

- Range: 0 59

## OSD1_RSSI_Y: RSSI_Y

Vertical position on screen

- Range: 0 21

## OSD1_CURRENT_EN: CURRENT_EN

Displays main battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CURRENT_X: CURRENT_X

Horizontal position on screen

- Range: 0 59

## OSD1_CURRENT_Y: CURRENT_Y

Vertical position on screen

- Range: 0 21

## OSD1_BATUSED_EN: BATUSED_EN

Displays primary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_BATUSED_X: BATUSED_X

Horizontal position on screen

- Range: 0 59

## OSD1_BATUSED_Y: BATUSED_Y

Vertical position on screen

- Range: 0 21

## OSD1_SATS_EN: SATS_EN

Displays number of acquired satellites

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_SATS_X: SATS_X

Horizontal position on screen

- Range: 0 59

## OSD1_SATS_Y: SATS_Y

Vertical position on screen

- Range: 0 21

## OSD1_FLTMODE_EN: FLTMODE_EN

Displays flight mode

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_FLTMODE_X: FLTMODE_X

Horizontal position on screen

- Range: 0 59

## OSD1_FLTMODE_Y: FLTMODE_Y

Vertical position on screen

- Range: 0 21

## OSD1_MESSAGE_EN: MESSAGE_EN

Displays Mavlink messages

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_MESSAGE_X: MESSAGE_X

Horizontal position on screen

- Range: 0 59

## OSD1_MESSAGE_Y: MESSAGE_Y

Vertical position on screen

- Range: 0 21

## OSD1_GSPEED_EN: GSPEED_EN

Displays GPS ground speed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_GSPEED_X: GSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD1_GSPEED_Y: GSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD1_HORIZON_EN: HORIZON_EN

Displays artificial horizon

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_HORIZON_X: HORIZON_X

Horizontal position on screen

- Range: 0 59

## OSD1_HORIZON_Y: HORIZON_Y

Vertical position on screen

- Range: 0 21

## OSD1_HOME_EN: HOME_EN

Displays distance and relative direction to HOME

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_HOME_X: HOME_X

Horizontal position on screen

- Range: 0 59

## OSD1_HOME_Y: HOME_Y

Vertical position on screen

- Range: 0 21

## OSD1_HEADING_EN: HEADING_EN

Displays heading

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_HEADING_X: HEADING_X

Horizontal position on screen

- Range: 0 59

## OSD1_HEADING_Y: HEADING_Y

Vertical position on screen

- Range: 0 21

## OSD1_THROTTLE_EN: THROTTLE_EN

Displays actual throttle percentage being sent to motor(s)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_THROTTLE_X: THROTTLE_X

Horizontal position on screen

- Range: 0 59

## OSD1_THROTTLE_Y: THROTTLE_Y

Vertical position on screen

- Range: 0 21

## OSD1_COMPASS_EN: COMPASS_EN

Enables display of compass rose

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_COMPASS_X: COMPASS_X

Horizontal position on screen

- Range: 0 59

## OSD1_COMPASS_Y: COMPASS_Y

Vertical position on screen

- Range: 0 21

## OSD1_WIND_EN: WIND_EN

Displays wind speed and relative direction, on Rover this is the apparent wind speed and direction from the windvane, if fitted

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_WIND_X: WIND_X

Horizontal position on screen

- Range: 0 59

## OSD1_WIND_Y: WIND_Y

Vertical position on screen

- Range: 0 21

## OSD1_ASPEED_EN: ASPEED_EN

Displays airspeed value being used by TECS (fused value)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ASPEED_X: ASPEED_X

Horizontal position on screen

- Range: 0 59

## OSD1_ASPEED_Y: ASPEED_Y

Vertical position on screen

- Range: 0 21

## OSD1_VSPEED_EN: VSPEED_EN

Displays climb rate

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_VSPEED_X: VSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD1_VSPEED_Y: VSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD1_ESCTEMP_EN: ESCTEMP_EN

Displays highest temp of all active ESCs, or of a specific ECS if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ESCTEMP_X: ESCTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD1_ESCTEMP_Y: ESCTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD1_ESCRPM_EN: ESCRPM_EN

Displays highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ESCRPM_X: ESCRPM_X

Horizontal position on screen

- Range: 0 59

## OSD1_ESCRPM_Y: ESCRPM_Y

Vertical position on screen

- Range: 0 21

## OSD1_ESCAMPS_EN: ESCAMPS_EN

Displays the current of the ESC with the highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ESCAMPS_X: ESCAMPS_X

Horizontal position on screen

- Range: 0 59

## OSD1_ESCAMPS_Y: ESCAMPS_Y

Vertical position on screen

- Range: 0 21

## OSD1_GPSLAT_EN: GPSLAT_EN

Displays GPS latitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_GPSLAT_X: GPSLAT_X

Horizontal position on screen

- Range: 0 59

## OSD1_GPSLAT_Y: GPSLAT_Y

Vertical position on screen

- Range: 0 21

## OSD1_GPSLONG_EN: GPSLONG_EN

Displays GPS longitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_GPSLONG_X: GPSLONG_X

Horizontal position on screen

- Range: 0 59

## OSD1_GPSLONG_Y: GPSLONG_Y

Vertical position on screen

- Range: 0 21

## OSD1_ROLL_EN: ROLL_EN

Displays degrees of roll from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ROLL_X: ROLL_X

Horizontal position on screen

- Range: 0 59

## OSD1_ROLL_Y: ROLL_Y

Vertical position on screen

- Range: 0 21

## OSD1_PITCH_EN: PITCH_EN

Displays degrees of pitch from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_PITCH_X: PITCH_X

Horizontal position on screen

- Range: 0 59

## OSD1_PITCH_Y: PITCH_Y

Vertical position on screen

- Range: 0 21

## OSD1_TEMP_EN: TEMP_EN

Displays temperature reported by primary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_TEMP_X: TEMP_X

Horizontal position on screen

- Range: 0 59

## OSD1_TEMP_Y: TEMP_Y

Vertical position on screen

- Range: 0 21

## OSD1_HDOP_EN: HDOP_EN

Displays Horizontal Dilution Of Position

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_HDOP_X: HDOP_X

Horizontal position on screen

- Range: 0 59

## OSD1_HDOP_Y: HDOP_Y

Vertical position on screen

- Range: 0 21

## OSD1_WAYPOINT_EN: WAYPOINT_EN

Displays bearing and distance to next waypoint

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_WAYPOINT_X: WAYPOINT_X

Horizontal position on screen

- Range: 0 59

## OSD1_WAYPOINT_Y: WAYPOINT_Y

Vertical position on screen

- Range: 0 21

## OSD1_XTRACK_EN: XTRACK_EN

Displays crosstrack error

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_XTRACK_X: XTRACK_X

Horizontal position on screen

- Range: 0 59

## OSD1_XTRACK_Y: XTRACK_Y

Vertical position on screen

- Range: 0 21

## OSD1_DIST_EN: DIST_EN

Displays total distance flown

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_DIST_X: DIST_X

Horizontal position on screen

- Range: 0 59

## OSD1_DIST_Y: DIST_Y

Vertical position on screen

- Range: 0 21

## OSD1_STATS_EN: STATS_EN

Displays flight stats

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_STATS_X: STATS_X

Horizontal position on screen

- Range: 0 59

## OSD1_STATS_Y: STATS_Y

Vertical position on screen

- Range: 0 21

## OSD1_FLTIME_EN: FLTIME_EN

Displays total flight time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_FLTIME_X: FLTIME_X

Horizontal position on screen

- Range: 0 59

## OSD1_FLTIME_Y: FLTIME_Y

Vertical position on screen

- Range: 0 21

## OSD1_CLIMBEFF_EN: CLIMBEFF_EN

Displays climb efficiency (climb rate/current)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CLIMBEFF_X: CLIMBEFF_X

Horizontal position on screen

- Range: 0 59

## OSD1_CLIMBEFF_Y: CLIMBEFF_Y

Vertical position on screen

- Range: 0 21

## OSD1_EFF_EN: EFF_EN

Displays flight efficiency (mAh/km or /mi)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_EFF_X: EFF_X

Horizontal position on screen

- Range: 0 59

## OSD1_EFF_Y: EFF_Y

Vertical position on screen

- Range: 0 21

## OSD1_BTEMP_EN: BTEMP_EN

Displays temperature reported by secondary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_BTEMP_X: BTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD1_BTEMP_Y: BTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD1_ATEMP_EN: ATEMP_EN

Displays temperature reported by primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ATEMP_X: ATEMP_X

Horizontal position on screen

- Range: 0 59

## OSD1_ATEMP_Y: ATEMP_Y

Vertical position on screen

- Range: 0 21

## OSD1_BAT2_VLT_EN: BAT2VLT_EN

Displays battery2 voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_BAT2_VLT_X: BAT2VLT_X

Horizontal position on screen

- Range: 0 59

## OSD1_BAT2_VLT_Y: BAT2VLT_Y

Vertical position on screen

- Range: 0 21

## OSD1_BAT2USED_EN: BAT2USED_EN

Displays secondary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_BAT2USED_X: BAT2USED_X

Horizontal position on screen

- Range: 0 59

## OSD1_BAT2USED_Y: BAT2USED_Y

Vertical position on screen

- Range: 0 21

## OSD1_ASPD2_EN: ASPD2_EN

Displays airspeed reported directly from secondary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ASPD2_X: ASPD2_X

Horizontal position on screen

- Range: 0 59

## OSD1_ASPD2_Y: ASPD2_Y

Vertical position on screen

- Range: 0 21

## OSD1_ASPD1_EN: ASPD1_EN

Displays airspeed reported directly from primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ASPD1_X: ASPD1_X

Horizontal position on screen

- Range: 0 59

## OSD1_ASPD1_Y: ASPD1_Y

Vertical position on screen

- Range: 0 21

## OSD1_CLK_EN: CLK_EN

Displays a clock panel based on AP_RTC local time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CLK_X: CLK_X

Horizontal position on screen

- Range: 0 59

## OSD1_CLK_Y: CLK_Y

Vertical position on screen

- Range: 0 21

## OSD1_SIDEBARS_EN: SIDEBARS_EN

Displays artificial horizon side bars

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_SIDEBARS_X: SIDEBARS_X

Horizontal position on screen

- Range: 0 59

## OSD1_SIDEBARS_Y: SIDEBARS_Y

Vertical position on screen

- Range: 0 21

## OSD1_CRSSHAIR_EN: CRSSHAIR_EN

Displays artificial horizon crosshair (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CRSSHAIR_X: CRSSHAIR_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD1_CRSSHAIR_Y: CRSSHAIR_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD1_HOMEDIST_EN: HOMEDIST_EN

Displays distance from HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_HOMEDIST_X: HOMEDIST_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD1_HOMEDIST_Y: HOMEDIST_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD1_HOMEDIR_EN: HOMEDIR_EN

Displays relative direction to HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_HOMEDIR_X: HOMEDIR_X

Horizontal position on screen

- Range: 0 59

## OSD1_HOMEDIR_Y: HOMEDIR_Y

Vertical position on screen

- Range: 0 21

## OSD1_POWER_EN: POWER_EN

Displays power (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_POWER_X: POWER_X

Horizontal position on screen

- Range: 0 59

## OSD1_POWER_Y: POWER_Y

Vertical position on screen

- Range: 0 21

## OSD1_CELLVOLT_EN: CELL_VOLT_EN

Displays average cell voltage (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CELLVOLT_X: CELL_VOLT_X

Horizontal position on screen

- Range: 0 59

## OSD1_CELLVOLT_Y: CELL_VOLT_Y

Vertical position on screen

- Range: 0 21

## OSD1_BATTBAR_EN: BATT_BAR_EN

Displays battery usage bar (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_BATTBAR_X: BATT_BAR_X

Horizontal position on screen

- Range: 0 59

## OSD1_BATTBAR_Y: BATT_BAR_Y

Vertical position on screen

- Range: 0 21

## OSD1_ARMING_EN: ARMING_EN

Displays arming status (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ARMING_X: ARMING_X

Horizontal position on screen

- Range: 0 59

## OSD1_ARMING_Y: ARMING_Y

Vertical position on screen

- Range: 0 21

## OSD1_PLUSCODE_EN: PLUSCODE_EN

Displays pluscode (OLC) element

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_PLUSCODE_X: PLUSCODE_X

Horizontal position on screen

- Range: 0 59

## OSD1_PLUSCODE_Y: PLUSCODE_Y

Vertical position on screen

- Range: 0 21

## OSD1_CALLSIGN_EN: CALLSIGN_EN

Displays callsign from callsign.txt on microSD card

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CALLSIGN_X: CALLSIGN_X

Horizontal position on screen

- Range: 0 59

## OSD1_CALLSIGN_Y: CALLSIGN_Y

Vertical position on screen

- Range: 0 21

## OSD1_CURRENT2_EN: CURRENT2_EN

Displays 2nd battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_CURRENT2_X: CURRENT2_X

Horizontal position on screen

- Range: 0 59

## OSD1_CURRENT2_Y: CURRENT2_Y

Vertical position on screen

- Range: 0 21

## OSD1_VTX_PWR_EN: VTX_PWR_EN

Displays VTX Power

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_VTX_PWR_X: VTX_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD1_VTX_PWR_Y: VTX_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD1_TER_HGT_EN: TER_HGT_EN

Displays Height above terrain

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_TER_HGT_X: TER_HGT_X

Horizontal position on screen

- Range: 0 59

## OSD1_TER_HGT_Y: TER_HGT_Y

Vertical position on screen

- Range: 0 21

## OSD1_AVGCELLV_EN: AVGCELLV_EN

Displays average cell voltage. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_AVGCELLV_X: AVGCELLV_X

Horizontal position on screen

- Range: 0 59

## OSD1_AVGCELLV_Y: AVGCELLV_Y

Vertical position on screen

- Range: 0 21

## OSD1_RESTVOLT_EN: RESTVOLT_EN

Displays main battery resting voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RESTVOLT_X: RESTVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD1_RESTVOLT_Y: RESTVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD1_FENCE_EN: FENCE_EN

Displays indication of fence enable and breach

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_FENCE_X: FENCE_X

Horizontal position on screen

- Range: 0 59

## OSD1_FENCE_Y: FENCE_Y

Vertical position on screen

- Range: 0 21

## OSD1_RNGF_EN: RNGF_EN

Displays a rangefinder's distance in cm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RNGF_X: RNGF_X

Horizontal position on screen

- Range: 0 59

## OSD1_RNGF_Y: RNGF_Y

Vertical position on screen

- Range: 0 21

## OSD1_ACRVOLT_EN: ACRVOLT_EN

Displays resting voltage for the average cell. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_ACRVOLT_X: ACRVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD1_ACRVOLT_Y: ACRVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD1_RPM_EN: RPM_EN

Displays main rotor revs/min

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RPM_X: RPM_X

Horizontal position on screen

- Range: 0 29

## OSD1_RPM_Y: RPM_Y

Vertical position on screen

- Range: 0 15

## OSD1_LINK_Q_EN: LINK_Q_EN

Displays Receiver link quality

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_LINK_Q_X: LINK_Q_X

Horizontal position on screen

- Range: 0 59

## OSD1_LINK_Q_Y: LINK_Q_Y

Vertical position on screen

- Range: 0 21

## OSD1_TXT_RES: Sets the overlay text resolution (MSP DisplayPort only)

Sets the overlay text resolution for this screen to either SD 30x16 or HD 50x18/60x22 (MSP DisplayPort only)

|Value|Meaning|
|:---:|:---:|
|0|30x16|
|1|50x18|
|2|60x22|

## OSD1_FONT: Sets the font index for this screen (MSP DisplayPort only)

Sets the font index for this screen (MSP DisplayPort only)

- Range: 0 21

## OSD1_RC_PWR_EN: RC_PWR_EN

Displays the RC link transmit (TX) power in mW or W, depending on level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RC_PWR_X: RC_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD1_RC_PWR_Y: RC_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD1_RSSIDBM_EN: RSSIDBM_EN

Displays RC link signal strength in dBm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RSSIDBM_X: RSSIDBM_X

Horizontal position on screen

- Range: 0 59

## OSD1_RSSIDBM_Y: RSSIDBM_Y

Vertical position on screen

- Range: 0 21

## OSD1_RC_SNR_EN: RC_SNR_EN

Displays RC link signal to noise ratio in dB

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RC_SNR_X: RC_SNR_X

Horizontal position on screen

- Range: 0 59

## OSD1_RC_SNR_Y: RC_SNR_Y

Vertical position on screen

- Range: 0 21

## OSD1_RC_ANT_EN: RC_ANT_EN

Displays the current RC link active antenna

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RC_ANT_X: RC_ANT_X

Horizontal position on screen

- Range: 0 59

## OSD1_RC_ANT_Y: RC_ANT_Y

Vertical position on screen

- Range: 0 21

## OSD1_RC_LQ_EN: RC_LQ_EN

Displays the RC link quality (uplink, 0 to 100%) and also RF mode if bit 7 of OSD_OPTIONS is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD1_RC_LQ_X: RC_LQ_X

Horizontal position on screen

- Range: 0 59

## OSD1_RC_LQ_Y: RC_LQ_Y

Vertical position on screen

- Range: 0 21

## OSD1_ESC_IDX: ESC_IDX

Index of the ESC to use for displaying ESC information. 0 means use the ESC with the highest value.

- Range: 0 32

# OSD2 Parameters

## OSD2_ENABLE: Enable screen

Enable this screen

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CHAN_MIN: Transmitter switch screen minimum pwm

This sets the PWM lower limit for this screen

- Range: 900 2100

## OSD2_CHAN_MAX: Transmitter switch screen maximum pwm

This sets the PWM upper limit for this screen

- Range: 900 2100

## OSD2_ALTITUDE_EN: ALTITUDE_EN

Enables display of altitude AGL

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ALTITUDE_X: ALTITUDE_X

Horizontal position on screen

- Range: 0 59

## OSD2_ALTITUDE_Y: ALTITUDE_Y

Vertical position on screen

- Range: 0 21

## OSD2_BAT_VOLT_EN: BATVOLT_EN

Displays main battery voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_BAT_VOLT_X: BATVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD2_BAT_VOLT_Y: BATVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD2_RSSI_EN: RSSI_EN

Displays RC signal strength

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RSSI_X: RSSI_X

Horizontal position on screen

- Range: 0 59

## OSD2_RSSI_Y: RSSI_Y

Vertical position on screen

- Range: 0 21

## OSD2_CURRENT_EN: CURRENT_EN

Displays main battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CURRENT_X: CURRENT_X

Horizontal position on screen

- Range: 0 59

## OSD2_CURRENT_Y: CURRENT_Y

Vertical position on screen

- Range: 0 21

## OSD2_BATUSED_EN: BATUSED_EN

Displays primary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_BATUSED_X: BATUSED_X

Horizontal position on screen

- Range: 0 59

## OSD2_BATUSED_Y: BATUSED_Y

Vertical position on screen

- Range: 0 21

## OSD2_SATS_EN: SATS_EN

Displays number of acquired satellites

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_SATS_X: SATS_X

Horizontal position on screen

- Range: 0 59

## OSD2_SATS_Y: SATS_Y

Vertical position on screen

- Range: 0 21

## OSD2_FLTMODE_EN: FLTMODE_EN

Displays flight mode

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_FLTMODE_X: FLTMODE_X

Horizontal position on screen

- Range: 0 59

## OSD2_FLTMODE_Y: FLTMODE_Y

Vertical position on screen

- Range: 0 21

## OSD2_MESSAGE_EN: MESSAGE_EN

Displays Mavlink messages

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_MESSAGE_X: MESSAGE_X

Horizontal position on screen

- Range: 0 59

## OSD2_MESSAGE_Y: MESSAGE_Y

Vertical position on screen

- Range: 0 21

## OSD2_GSPEED_EN: GSPEED_EN

Displays GPS ground speed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_GSPEED_X: GSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD2_GSPEED_Y: GSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD2_HORIZON_EN: HORIZON_EN

Displays artificial horizon

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_HORIZON_X: HORIZON_X

Horizontal position on screen

- Range: 0 59

## OSD2_HORIZON_Y: HORIZON_Y

Vertical position on screen

- Range: 0 21

## OSD2_HOME_EN: HOME_EN

Displays distance and relative direction to HOME

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_HOME_X: HOME_X

Horizontal position on screen

- Range: 0 59

## OSD2_HOME_Y: HOME_Y

Vertical position on screen

- Range: 0 21

## OSD2_HEADING_EN: HEADING_EN

Displays heading

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_HEADING_X: HEADING_X

Horizontal position on screen

- Range: 0 59

## OSD2_HEADING_Y: HEADING_Y

Vertical position on screen

- Range: 0 21

## OSD2_THROTTLE_EN: THROTTLE_EN

Displays actual throttle percentage being sent to motor(s)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_THROTTLE_X: THROTTLE_X

Horizontal position on screen

- Range: 0 59

## OSD2_THROTTLE_Y: THROTTLE_Y

Vertical position on screen

- Range: 0 21

## OSD2_COMPASS_EN: COMPASS_EN

Enables display of compass rose

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_COMPASS_X: COMPASS_X

Horizontal position on screen

- Range: 0 59

## OSD2_COMPASS_Y: COMPASS_Y

Vertical position on screen

- Range: 0 21

## OSD2_WIND_EN: WIND_EN

Displays wind speed and relative direction, on Rover this is the apparent wind speed and direction from the windvane, if fitted

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_WIND_X: WIND_X

Horizontal position on screen

- Range: 0 59

## OSD2_WIND_Y: WIND_Y

Vertical position on screen

- Range: 0 21

## OSD2_ASPEED_EN: ASPEED_EN

Displays airspeed value being used by TECS (fused value)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ASPEED_X: ASPEED_X

Horizontal position on screen

- Range: 0 59

## OSD2_ASPEED_Y: ASPEED_Y

Vertical position on screen

- Range: 0 21

## OSD2_VSPEED_EN: VSPEED_EN

Displays climb rate

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_VSPEED_X: VSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD2_VSPEED_Y: VSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD2_ESCTEMP_EN: ESCTEMP_EN

Displays highest temp of all active ESCs, or of a specific ECS if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ESCTEMP_X: ESCTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD2_ESCTEMP_Y: ESCTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD2_ESCRPM_EN: ESCRPM_EN

Displays highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ESCRPM_X: ESCRPM_X

Horizontal position on screen

- Range: 0 59

## OSD2_ESCRPM_Y: ESCRPM_Y

Vertical position on screen

- Range: 0 21

## OSD2_ESCAMPS_EN: ESCAMPS_EN

Displays the current of the ESC with the highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ESCAMPS_X: ESCAMPS_X

Horizontal position on screen

- Range: 0 59

## OSD2_ESCAMPS_Y: ESCAMPS_Y

Vertical position on screen

- Range: 0 21

## OSD2_GPSLAT_EN: GPSLAT_EN

Displays GPS latitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_GPSLAT_X: GPSLAT_X

Horizontal position on screen

- Range: 0 59

## OSD2_GPSLAT_Y: GPSLAT_Y

Vertical position on screen

- Range: 0 21

## OSD2_GPSLONG_EN: GPSLONG_EN

Displays GPS longitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_GPSLONG_X: GPSLONG_X

Horizontal position on screen

- Range: 0 59

## OSD2_GPSLONG_Y: GPSLONG_Y

Vertical position on screen

- Range: 0 21

## OSD2_ROLL_EN: ROLL_EN

Displays degrees of roll from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ROLL_X: ROLL_X

Horizontal position on screen

- Range: 0 59

## OSD2_ROLL_Y: ROLL_Y

Vertical position on screen

- Range: 0 21

## OSD2_PITCH_EN: PITCH_EN

Displays degrees of pitch from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_PITCH_X: PITCH_X

Horizontal position on screen

- Range: 0 59

## OSD2_PITCH_Y: PITCH_Y

Vertical position on screen

- Range: 0 21

## OSD2_TEMP_EN: TEMP_EN

Displays temperature reported by primary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_TEMP_X: TEMP_X

Horizontal position on screen

- Range: 0 59

## OSD2_TEMP_Y: TEMP_Y

Vertical position on screen

- Range: 0 21

## OSD2_HDOP_EN: HDOP_EN

Displays Horizontal Dilution Of Position

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_HDOP_X: HDOP_X

Horizontal position on screen

- Range: 0 59

## OSD2_HDOP_Y: HDOP_Y

Vertical position on screen

- Range: 0 21

## OSD2_WAYPOINT_EN: WAYPOINT_EN

Displays bearing and distance to next waypoint

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_WAYPOINT_X: WAYPOINT_X

Horizontal position on screen

- Range: 0 59

## OSD2_WAYPOINT_Y: WAYPOINT_Y

Vertical position on screen

- Range: 0 21

## OSD2_XTRACK_EN: XTRACK_EN

Displays crosstrack error

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_XTRACK_X: XTRACK_X

Horizontal position on screen

- Range: 0 59

## OSD2_XTRACK_Y: XTRACK_Y

Vertical position on screen

- Range: 0 21

## OSD2_DIST_EN: DIST_EN

Displays total distance flown

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_DIST_X: DIST_X

Horizontal position on screen

- Range: 0 59

## OSD2_DIST_Y: DIST_Y

Vertical position on screen

- Range: 0 21

## OSD2_STATS_EN: STATS_EN

Displays flight stats

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_STATS_X: STATS_X

Horizontal position on screen

- Range: 0 59

## OSD2_STATS_Y: STATS_Y

Vertical position on screen

- Range: 0 21

## OSD2_FLTIME_EN: FLTIME_EN

Displays total flight time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_FLTIME_X: FLTIME_X

Horizontal position on screen

- Range: 0 59

## OSD2_FLTIME_Y: FLTIME_Y

Vertical position on screen

- Range: 0 21

## OSD2_CLIMBEFF_EN: CLIMBEFF_EN

Displays climb efficiency (climb rate/current)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CLIMBEFF_X: CLIMBEFF_X

Horizontal position on screen

- Range: 0 59

## OSD2_CLIMBEFF_Y: CLIMBEFF_Y

Vertical position on screen

- Range: 0 21

## OSD2_EFF_EN: EFF_EN

Displays flight efficiency (mAh/km or /mi)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_EFF_X: EFF_X

Horizontal position on screen

- Range: 0 59

## OSD2_EFF_Y: EFF_Y

Vertical position on screen

- Range: 0 21

## OSD2_BTEMP_EN: BTEMP_EN

Displays temperature reported by secondary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_BTEMP_X: BTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD2_BTEMP_Y: BTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD2_ATEMP_EN: ATEMP_EN

Displays temperature reported by primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ATEMP_X: ATEMP_X

Horizontal position on screen

- Range: 0 59

## OSD2_ATEMP_Y: ATEMP_Y

Vertical position on screen

- Range: 0 21

## OSD2_BAT2_VLT_EN: BAT2VLT_EN

Displays battery2 voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_BAT2_VLT_X: BAT2VLT_X

Horizontal position on screen

- Range: 0 59

## OSD2_BAT2_VLT_Y: BAT2VLT_Y

Vertical position on screen

- Range: 0 21

## OSD2_BAT2USED_EN: BAT2USED_EN

Displays secondary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_BAT2USED_X: BAT2USED_X

Horizontal position on screen

- Range: 0 59

## OSD2_BAT2USED_Y: BAT2USED_Y

Vertical position on screen

- Range: 0 21

## OSD2_ASPD2_EN: ASPD2_EN

Displays airspeed reported directly from secondary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ASPD2_X: ASPD2_X

Horizontal position on screen

- Range: 0 59

## OSD2_ASPD2_Y: ASPD2_Y

Vertical position on screen

- Range: 0 21

## OSD2_ASPD1_EN: ASPD1_EN

Displays airspeed reported directly from primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ASPD1_X: ASPD1_X

Horizontal position on screen

- Range: 0 59

## OSD2_ASPD1_Y: ASPD1_Y

Vertical position on screen

- Range: 0 21

## OSD2_CLK_EN: CLK_EN

Displays a clock panel based on AP_RTC local time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CLK_X: CLK_X

Horizontal position on screen

- Range: 0 59

## OSD2_CLK_Y: CLK_Y

Vertical position on screen

- Range: 0 21

## OSD2_SIDEBARS_EN: SIDEBARS_EN

Displays artificial horizon side bars

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_SIDEBARS_X: SIDEBARS_X

Horizontal position on screen

- Range: 0 59

## OSD2_SIDEBARS_Y: SIDEBARS_Y

Vertical position on screen

- Range: 0 21

## OSD2_CRSSHAIR_EN: CRSSHAIR_EN

Displays artificial horizon crosshair (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CRSSHAIR_X: CRSSHAIR_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD2_CRSSHAIR_Y: CRSSHAIR_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD2_HOMEDIST_EN: HOMEDIST_EN

Displays distance from HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_HOMEDIST_X: HOMEDIST_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD2_HOMEDIST_Y: HOMEDIST_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD2_HOMEDIR_EN: HOMEDIR_EN

Displays relative direction to HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_HOMEDIR_X: HOMEDIR_X

Horizontal position on screen

- Range: 0 59

## OSD2_HOMEDIR_Y: HOMEDIR_Y

Vertical position on screen

- Range: 0 21

## OSD2_POWER_EN: POWER_EN

Displays power (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_POWER_X: POWER_X

Horizontal position on screen

- Range: 0 59

## OSD2_POWER_Y: POWER_Y

Vertical position on screen

- Range: 0 21

## OSD2_CELLVOLT_EN: CELL_VOLT_EN

Displays average cell voltage (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CELLVOLT_X: CELL_VOLT_X

Horizontal position on screen

- Range: 0 59

## OSD2_CELLVOLT_Y: CELL_VOLT_Y

Vertical position on screen

- Range: 0 21

## OSD2_BATTBAR_EN: BATT_BAR_EN

Displays battery usage bar (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_BATTBAR_X: BATT_BAR_X

Horizontal position on screen

- Range: 0 59

## OSD2_BATTBAR_Y: BATT_BAR_Y

Vertical position on screen

- Range: 0 21

## OSD2_ARMING_EN: ARMING_EN

Displays arming status (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ARMING_X: ARMING_X

Horizontal position on screen

- Range: 0 59

## OSD2_ARMING_Y: ARMING_Y

Vertical position on screen

- Range: 0 21

## OSD2_PLUSCODE_EN: PLUSCODE_EN

Displays pluscode (OLC) element

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_PLUSCODE_X: PLUSCODE_X

Horizontal position on screen

- Range: 0 59

## OSD2_PLUSCODE_Y: PLUSCODE_Y

Vertical position on screen

- Range: 0 21

## OSD2_CALLSIGN_EN: CALLSIGN_EN

Displays callsign from callsign.txt on microSD card

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CALLSIGN_X: CALLSIGN_X

Horizontal position on screen

- Range: 0 59

## OSD2_CALLSIGN_Y: CALLSIGN_Y

Vertical position on screen

- Range: 0 21

## OSD2_CURRENT2_EN: CURRENT2_EN

Displays 2nd battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_CURRENT2_X: CURRENT2_X

Horizontal position on screen

- Range: 0 59

## OSD2_CURRENT2_Y: CURRENT2_Y

Vertical position on screen

- Range: 0 21

## OSD2_VTX_PWR_EN: VTX_PWR_EN

Displays VTX Power

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_VTX_PWR_X: VTX_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD2_VTX_PWR_Y: VTX_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD2_TER_HGT_EN: TER_HGT_EN

Displays Height above terrain

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_TER_HGT_X: TER_HGT_X

Horizontal position on screen

- Range: 0 59

## OSD2_TER_HGT_Y: TER_HGT_Y

Vertical position on screen

- Range: 0 21

## OSD2_AVGCELLV_EN: AVGCELLV_EN

Displays average cell voltage. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_AVGCELLV_X: AVGCELLV_X

Horizontal position on screen

- Range: 0 59

## OSD2_AVGCELLV_Y: AVGCELLV_Y

Vertical position on screen

- Range: 0 21

## OSD2_RESTVOLT_EN: RESTVOLT_EN

Displays main battery resting voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RESTVOLT_X: RESTVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD2_RESTVOLT_Y: RESTVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD2_FENCE_EN: FENCE_EN

Displays indication of fence enable and breach

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_FENCE_X: FENCE_X

Horizontal position on screen

- Range: 0 59

## OSD2_FENCE_Y: FENCE_Y

Vertical position on screen

- Range: 0 21

## OSD2_RNGF_EN: RNGF_EN

Displays a rangefinder's distance in cm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RNGF_X: RNGF_X

Horizontal position on screen

- Range: 0 59

## OSD2_RNGF_Y: RNGF_Y

Vertical position on screen

- Range: 0 21

## OSD2_ACRVOLT_EN: ACRVOLT_EN

Displays resting voltage for the average cell. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_ACRVOLT_X: ACRVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD2_ACRVOLT_Y: ACRVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD2_RPM_EN: RPM_EN

Displays main rotor revs/min

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RPM_X: RPM_X

Horizontal position on screen

- Range: 0 29

## OSD2_RPM_Y: RPM_Y

Vertical position on screen

- Range: 0 15

## OSD2_LINK_Q_EN: LINK_Q_EN

Displays Receiver link quality

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_LINK_Q_X: LINK_Q_X

Horizontal position on screen

- Range: 0 59

## OSD2_LINK_Q_Y: LINK_Q_Y

Vertical position on screen

- Range: 0 21

## OSD2_TXT_RES: Sets the overlay text resolution (MSP DisplayPort only)

Sets the overlay text resolution for this screen to either SD 30x16 or HD 50x18/60x22 (MSP DisplayPort only)

|Value|Meaning|
|:---:|:---:|
|0|30x16|
|1|50x18|
|2|60x22|

## OSD2_FONT: Sets the font index for this screen (MSP DisplayPort only)

Sets the font index for this screen (MSP DisplayPort only)

- Range: 0 21

## OSD2_RC_PWR_EN: RC_PWR_EN

Displays the RC link transmit (TX) power in mW or W, depending on level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RC_PWR_X: RC_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD2_RC_PWR_Y: RC_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD2_RSSIDBM_EN: RSSIDBM_EN

Displays RC link signal strength in dBm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RSSIDBM_X: RSSIDBM_X

Horizontal position on screen

- Range: 0 59

## OSD2_RSSIDBM_Y: RSSIDBM_Y

Vertical position on screen

- Range: 0 21

## OSD2_RC_SNR_EN: RC_SNR_EN

Displays RC link signal to noise ratio in dB

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RC_SNR_X: RC_SNR_X

Horizontal position on screen

- Range: 0 59

## OSD2_RC_SNR_Y: RC_SNR_Y

Vertical position on screen

- Range: 0 21

## OSD2_RC_ANT_EN: RC_ANT_EN

Displays the current RC link active antenna

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RC_ANT_X: RC_ANT_X

Horizontal position on screen

- Range: 0 59

## OSD2_RC_ANT_Y: RC_ANT_Y

Vertical position on screen

- Range: 0 21

## OSD2_RC_LQ_EN: RC_LQ_EN

Displays the RC link quality (uplink, 0 to 100%) and also RF mode if bit 7 of OSD_OPTIONS is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD2_RC_LQ_X: RC_LQ_X

Horizontal position on screen

- Range: 0 59

## OSD2_RC_LQ_Y: RC_LQ_Y

Vertical position on screen

- Range: 0 21

## OSD2_ESC_IDX: ESC_IDX

Index of the ESC to use for displaying ESC information. 0 means use the ESC with the highest value.

- Range: 0 32

# OSD3 Parameters

## OSD3_ENABLE: Enable screen

Enable this screen

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CHAN_MIN: Transmitter switch screen minimum pwm

This sets the PWM lower limit for this screen

- Range: 900 2100

## OSD3_CHAN_MAX: Transmitter switch screen maximum pwm

This sets the PWM upper limit for this screen

- Range: 900 2100

## OSD3_ALTITUDE_EN: ALTITUDE_EN

Enables display of altitude AGL

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ALTITUDE_X: ALTITUDE_X

Horizontal position on screen

- Range: 0 59

## OSD3_ALTITUDE_Y: ALTITUDE_Y

Vertical position on screen

- Range: 0 21

## OSD3_BAT_VOLT_EN: BATVOLT_EN

Displays main battery voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_BAT_VOLT_X: BATVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD3_BAT_VOLT_Y: BATVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD3_RSSI_EN: RSSI_EN

Displays RC signal strength

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RSSI_X: RSSI_X

Horizontal position on screen

- Range: 0 59

## OSD3_RSSI_Y: RSSI_Y

Vertical position on screen

- Range: 0 21

## OSD3_CURRENT_EN: CURRENT_EN

Displays main battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CURRENT_X: CURRENT_X

Horizontal position on screen

- Range: 0 59

## OSD3_CURRENT_Y: CURRENT_Y

Vertical position on screen

- Range: 0 21

## OSD3_BATUSED_EN: BATUSED_EN

Displays primary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_BATUSED_X: BATUSED_X

Horizontal position on screen

- Range: 0 59

## OSD3_BATUSED_Y: BATUSED_Y

Vertical position on screen

- Range: 0 21

## OSD3_SATS_EN: SATS_EN

Displays number of acquired satellites

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_SATS_X: SATS_X

Horizontal position on screen

- Range: 0 59

## OSD3_SATS_Y: SATS_Y

Vertical position on screen

- Range: 0 21

## OSD3_FLTMODE_EN: FLTMODE_EN

Displays flight mode

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_FLTMODE_X: FLTMODE_X

Horizontal position on screen

- Range: 0 59

## OSD3_FLTMODE_Y: FLTMODE_Y

Vertical position on screen

- Range: 0 21

## OSD3_MESSAGE_EN: MESSAGE_EN

Displays Mavlink messages

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_MESSAGE_X: MESSAGE_X

Horizontal position on screen

- Range: 0 59

## OSD3_MESSAGE_Y: MESSAGE_Y

Vertical position on screen

- Range: 0 21

## OSD3_GSPEED_EN: GSPEED_EN

Displays GPS ground speed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_GSPEED_X: GSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD3_GSPEED_Y: GSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD3_HORIZON_EN: HORIZON_EN

Displays artificial horizon

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_HORIZON_X: HORIZON_X

Horizontal position on screen

- Range: 0 59

## OSD3_HORIZON_Y: HORIZON_Y

Vertical position on screen

- Range: 0 21

## OSD3_HOME_EN: HOME_EN

Displays distance and relative direction to HOME

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_HOME_X: HOME_X

Horizontal position on screen

- Range: 0 59

## OSD3_HOME_Y: HOME_Y

Vertical position on screen

- Range: 0 21

## OSD3_HEADING_EN: HEADING_EN

Displays heading

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_HEADING_X: HEADING_X

Horizontal position on screen

- Range: 0 59

## OSD3_HEADING_Y: HEADING_Y

Vertical position on screen

- Range: 0 21

## OSD3_THROTTLE_EN: THROTTLE_EN

Displays actual throttle percentage being sent to motor(s)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_THROTTLE_X: THROTTLE_X

Horizontal position on screen

- Range: 0 59

## OSD3_THROTTLE_Y: THROTTLE_Y

Vertical position on screen

- Range: 0 21

## OSD3_COMPASS_EN: COMPASS_EN

Enables display of compass rose

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_COMPASS_X: COMPASS_X

Horizontal position on screen

- Range: 0 59

## OSD3_COMPASS_Y: COMPASS_Y

Vertical position on screen

- Range: 0 21

## OSD3_WIND_EN: WIND_EN

Displays wind speed and relative direction, on Rover this is the apparent wind speed and direction from the windvane, if fitted

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_WIND_X: WIND_X

Horizontal position on screen

- Range: 0 59

## OSD3_WIND_Y: WIND_Y

Vertical position on screen

- Range: 0 21

## OSD3_ASPEED_EN: ASPEED_EN

Displays airspeed value being used by TECS (fused value)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ASPEED_X: ASPEED_X

Horizontal position on screen

- Range: 0 59

## OSD3_ASPEED_Y: ASPEED_Y

Vertical position on screen

- Range: 0 21

## OSD3_VSPEED_EN: VSPEED_EN

Displays climb rate

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_VSPEED_X: VSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD3_VSPEED_Y: VSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD3_ESCTEMP_EN: ESCTEMP_EN

Displays highest temp of all active ESCs, or of a specific ECS if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ESCTEMP_X: ESCTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD3_ESCTEMP_Y: ESCTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD3_ESCRPM_EN: ESCRPM_EN

Displays highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ESCRPM_X: ESCRPM_X

Horizontal position on screen

- Range: 0 59

## OSD3_ESCRPM_Y: ESCRPM_Y

Vertical position on screen

- Range: 0 21

## OSD3_ESCAMPS_EN: ESCAMPS_EN

Displays the current of the ESC with the highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ESCAMPS_X: ESCAMPS_X

Horizontal position on screen

- Range: 0 59

## OSD3_ESCAMPS_Y: ESCAMPS_Y

Vertical position on screen

- Range: 0 21

## OSD3_GPSLAT_EN: GPSLAT_EN

Displays GPS latitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_GPSLAT_X: GPSLAT_X

Horizontal position on screen

- Range: 0 59

## OSD3_GPSLAT_Y: GPSLAT_Y

Vertical position on screen

- Range: 0 21

## OSD3_GPSLONG_EN: GPSLONG_EN

Displays GPS longitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_GPSLONG_X: GPSLONG_X

Horizontal position on screen

- Range: 0 59

## OSD3_GPSLONG_Y: GPSLONG_Y

Vertical position on screen

- Range: 0 21

## OSD3_ROLL_EN: ROLL_EN

Displays degrees of roll from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ROLL_X: ROLL_X

Horizontal position on screen

- Range: 0 59

## OSD3_ROLL_Y: ROLL_Y

Vertical position on screen

- Range: 0 21

## OSD3_PITCH_EN: PITCH_EN

Displays degrees of pitch from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_PITCH_X: PITCH_X

Horizontal position on screen

- Range: 0 59

## OSD3_PITCH_Y: PITCH_Y

Vertical position on screen

- Range: 0 21

## OSD3_TEMP_EN: TEMP_EN

Displays temperature reported by primary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_TEMP_X: TEMP_X

Horizontal position on screen

- Range: 0 59

## OSD3_TEMP_Y: TEMP_Y

Vertical position on screen

- Range: 0 21

## OSD3_HDOP_EN: HDOP_EN

Displays Horizontal Dilution Of Position

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_HDOP_X: HDOP_X

Horizontal position on screen

- Range: 0 59

## OSD3_HDOP_Y: HDOP_Y

Vertical position on screen

- Range: 0 21

## OSD3_WAYPOINT_EN: WAYPOINT_EN

Displays bearing and distance to next waypoint

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_WAYPOINT_X: WAYPOINT_X

Horizontal position on screen

- Range: 0 59

## OSD3_WAYPOINT_Y: WAYPOINT_Y

Vertical position on screen

- Range: 0 21

## OSD3_XTRACK_EN: XTRACK_EN

Displays crosstrack error

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_XTRACK_X: XTRACK_X

Horizontal position on screen

- Range: 0 59

## OSD3_XTRACK_Y: XTRACK_Y

Vertical position on screen

- Range: 0 21

## OSD3_DIST_EN: DIST_EN

Displays total distance flown

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_DIST_X: DIST_X

Horizontal position on screen

- Range: 0 59

## OSD3_DIST_Y: DIST_Y

Vertical position on screen

- Range: 0 21

## OSD3_STATS_EN: STATS_EN

Displays flight stats

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_STATS_X: STATS_X

Horizontal position on screen

- Range: 0 59

## OSD3_STATS_Y: STATS_Y

Vertical position on screen

- Range: 0 21

## OSD3_FLTIME_EN: FLTIME_EN

Displays total flight time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_FLTIME_X: FLTIME_X

Horizontal position on screen

- Range: 0 59

## OSD3_FLTIME_Y: FLTIME_Y

Vertical position on screen

- Range: 0 21

## OSD3_CLIMBEFF_EN: CLIMBEFF_EN

Displays climb efficiency (climb rate/current)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CLIMBEFF_X: CLIMBEFF_X

Horizontal position on screen

- Range: 0 59

## OSD3_CLIMBEFF_Y: CLIMBEFF_Y

Vertical position on screen

- Range: 0 21

## OSD3_EFF_EN: EFF_EN

Displays flight efficiency (mAh/km or /mi)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_EFF_X: EFF_X

Horizontal position on screen

- Range: 0 59

## OSD3_EFF_Y: EFF_Y

Vertical position on screen

- Range: 0 21

## OSD3_BTEMP_EN: BTEMP_EN

Displays temperature reported by secondary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_BTEMP_X: BTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD3_BTEMP_Y: BTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD3_ATEMP_EN: ATEMP_EN

Displays temperature reported by primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ATEMP_X: ATEMP_X

Horizontal position on screen

- Range: 0 59

## OSD3_ATEMP_Y: ATEMP_Y

Vertical position on screen

- Range: 0 21

## OSD3_BAT2_VLT_EN: BAT2VLT_EN

Displays battery2 voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_BAT2_VLT_X: BAT2VLT_X

Horizontal position on screen

- Range: 0 59

## OSD3_BAT2_VLT_Y: BAT2VLT_Y

Vertical position on screen

- Range: 0 21

## OSD3_BAT2USED_EN: BAT2USED_EN

Displays secondary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_BAT2USED_X: BAT2USED_X

Horizontal position on screen

- Range: 0 59

## OSD3_BAT2USED_Y: BAT2USED_Y

Vertical position on screen

- Range: 0 21

## OSD3_ASPD2_EN: ASPD2_EN

Displays airspeed reported directly from secondary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ASPD2_X: ASPD2_X

Horizontal position on screen

- Range: 0 59

## OSD3_ASPD2_Y: ASPD2_Y

Vertical position on screen

- Range: 0 21

## OSD3_ASPD1_EN: ASPD1_EN

Displays airspeed reported directly from primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ASPD1_X: ASPD1_X

Horizontal position on screen

- Range: 0 59

## OSD3_ASPD1_Y: ASPD1_Y

Vertical position on screen

- Range: 0 21

## OSD3_CLK_EN: CLK_EN

Displays a clock panel based on AP_RTC local time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CLK_X: CLK_X

Horizontal position on screen

- Range: 0 59

## OSD3_CLK_Y: CLK_Y

Vertical position on screen

- Range: 0 21

## OSD3_SIDEBARS_EN: SIDEBARS_EN

Displays artificial horizon side bars

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_SIDEBARS_X: SIDEBARS_X

Horizontal position on screen

- Range: 0 59

## OSD3_SIDEBARS_Y: SIDEBARS_Y

Vertical position on screen

- Range: 0 21

## OSD3_CRSSHAIR_EN: CRSSHAIR_EN

Displays artificial horizon crosshair (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CRSSHAIR_X: CRSSHAIR_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD3_CRSSHAIR_Y: CRSSHAIR_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD3_HOMEDIST_EN: HOMEDIST_EN

Displays distance from HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_HOMEDIST_X: HOMEDIST_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD3_HOMEDIST_Y: HOMEDIST_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD3_HOMEDIR_EN: HOMEDIR_EN

Displays relative direction to HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_HOMEDIR_X: HOMEDIR_X

Horizontal position on screen

- Range: 0 59

## OSD3_HOMEDIR_Y: HOMEDIR_Y

Vertical position on screen

- Range: 0 21

## OSD3_POWER_EN: POWER_EN

Displays power (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_POWER_X: POWER_X

Horizontal position on screen

- Range: 0 59

## OSD3_POWER_Y: POWER_Y

Vertical position on screen

- Range: 0 21

## OSD3_CELLVOLT_EN: CELL_VOLT_EN

Displays average cell voltage (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CELLVOLT_X: CELL_VOLT_X

Horizontal position on screen

- Range: 0 59

## OSD3_CELLVOLT_Y: CELL_VOLT_Y

Vertical position on screen

- Range: 0 21

## OSD3_BATTBAR_EN: BATT_BAR_EN

Displays battery usage bar (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_BATTBAR_X: BATT_BAR_X

Horizontal position on screen

- Range: 0 59

## OSD3_BATTBAR_Y: BATT_BAR_Y

Vertical position on screen

- Range: 0 21

## OSD3_ARMING_EN: ARMING_EN

Displays arming status (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ARMING_X: ARMING_X

Horizontal position on screen

- Range: 0 59

## OSD3_ARMING_Y: ARMING_Y

Vertical position on screen

- Range: 0 21

## OSD3_PLUSCODE_EN: PLUSCODE_EN

Displays pluscode (OLC) element

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_PLUSCODE_X: PLUSCODE_X

Horizontal position on screen

- Range: 0 59

## OSD3_PLUSCODE_Y: PLUSCODE_Y

Vertical position on screen

- Range: 0 21

## OSD3_CALLSIGN_EN: CALLSIGN_EN

Displays callsign from callsign.txt on microSD card

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CALLSIGN_X: CALLSIGN_X

Horizontal position on screen

- Range: 0 59

## OSD3_CALLSIGN_Y: CALLSIGN_Y

Vertical position on screen

- Range: 0 21

## OSD3_CURRENT2_EN: CURRENT2_EN

Displays 2nd battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_CURRENT2_X: CURRENT2_X

Horizontal position on screen

- Range: 0 59

## OSD3_CURRENT2_Y: CURRENT2_Y

Vertical position on screen

- Range: 0 21

## OSD3_VTX_PWR_EN: VTX_PWR_EN

Displays VTX Power

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_VTX_PWR_X: VTX_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD3_VTX_PWR_Y: VTX_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD3_TER_HGT_EN: TER_HGT_EN

Displays Height above terrain

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_TER_HGT_X: TER_HGT_X

Horizontal position on screen

- Range: 0 59

## OSD3_TER_HGT_Y: TER_HGT_Y

Vertical position on screen

- Range: 0 21

## OSD3_AVGCELLV_EN: AVGCELLV_EN

Displays average cell voltage. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_AVGCELLV_X: AVGCELLV_X

Horizontal position on screen

- Range: 0 59

## OSD3_AVGCELLV_Y: AVGCELLV_Y

Vertical position on screen

- Range: 0 21

## OSD3_RESTVOLT_EN: RESTVOLT_EN

Displays main battery resting voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RESTVOLT_X: RESTVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD3_RESTVOLT_Y: RESTVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD3_FENCE_EN: FENCE_EN

Displays indication of fence enable and breach

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_FENCE_X: FENCE_X

Horizontal position on screen

- Range: 0 59

## OSD3_FENCE_Y: FENCE_Y

Vertical position on screen

- Range: 0 21

## OSD3_RNGF_EN: RNGF_EN

Displays a rangefinder's distance in cm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RNGF_X: RNGF_X

Horizontal position on screen

- Range: 0 59

## OSD3_RNGF_Y: RNGF_Y

Vertical position on screen

- Range: 0 21

## OSD3_ACRVOLT_EN: ACRVOLT_EN

Displays resting voltage for the average cell. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_ACRVOLT_X: ACRVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD3_ACRVOLT_Y: ACRVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD3_RPM_EN: RPM_EN

Displays main rotor revs/min

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RPM_X: RPM_X

Horizontal position on screen

- Range: 0 29

## OSD3_RPM_Y: RPM_Y

Vertical position on screen

- Range: 0 15

## OSD3_LINK_Q_EN: LINK_Q_EN

Displays Receiver link quality

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_LINK_Q_X: LINK_Q_X

Horizontal position on screen

- Range: 0 59

## OSD3_LINK_Q_Y: LINK_Q_Y

Vertical position on screen

- Range: 0 21

## OSD3_TXT_RES: Sets the overlay text resolution (MSP DisplayPort only)

Sets the overlay text resolution for this screen to either SD 30x16 or HD 50x18/60x22 (MSP DisplayPort only)

|Value|Meaning|
|:---:|:---:|
|0|30x16|
|1|50x18|
|2|60x22|

## OSD3_FONT: Sets the font index for this screen (MSP DisplayPort only)

Sets the font index for this screen (MSP DisplayPort only)

- Range: 0 21

## OSD3_RC_PWR_EN: RC_PWR_EN

Displays the RC link transmit (TX) power in mW or W, depending on level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RC_PWR_X: RC_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD3_RC_PWR_Y: RC_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD3_RSSIDBM_EN: RSSIDBM_EN

Displays RC link signal strength in dBm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RSSIDBM_X: RSSIDBM_X

Horizontal position on screen

- Range: 0 59

## OSD3_RSSIDBM_Y: RSSIDBM_Y

Vertical position on screen

- Range: 0 21

## OSD3_RC_SNR_EN: RC_SNR_EN

Displays RC link signal to noise ratio in dB

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RC_SNR_X: RC_SNR_X

Horizontal position on screen

- Range: 0 59

## OSD3_RC_SNR_Y: RC_SNR_Y

Vertical position on screen

- Range: 0 21

## OSD3_RC_ANT_EN: RC_ANT_EN

Displays the current RC link active antenna

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RC_ANT_X: RC_ANT_X

Horizontal position on screen

- Range: 0 59

## OSD3_RC_ANT_Y: RC_ANT_Y

Vertical position on screen

- Range: 0 21

## OSD3_RC_LQ_EN: RC_LQ_EN

Displays the RC link quality (uplink, 0 to 100%) and also RF mode if bit 7 of OSD_OPTIONS is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD3_RC_LQ_X: RC_LQ_X

Horizontal position on screen

- Range: 0 59

## OSD3_RC_LQ_Y: RC_LQ_Y

Vertical position on screen

- Range: 0 21

## OSD3_ESC_IDX: ESC_IDX

Index of the ESC to use for displaying ESC information. 0 means use the ESC with the highest value.

- Range: 0 32

# OSD4 Parameters

## OSD4_ENABLE: Enable screen

Enable this screen

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CHAN_MIN: Transmitter switch screen minimum pwm

This sets the PWM lower limit for this screen

- Range: 900 2100

## OSD4_CHAN_MAX: Transmitter switch screen maximum pwm

This sets the PWM upper limit for this screen

- Range: 900 2100

## OSD4_ALTITUDE_EN: ALTITUDE_EN

Enables display of altitude AGL

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ALTITUDE_X: ALTITUDE_X

Horizontal position on screen

- Range: 0 59

## OSD4_ALTITUDE_Y: ALTITUDE_Y

Vertical position on screen

- Range: 0 21

## OSD4_BAT_VOLT_EN: BATVOLT_EN

Displays main battery voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_BAT_VOLT_X: BATVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD4_BAT_VOLT_Y: BATVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD4_RSSI_EN: RSSI_EN

Displays RC signal strength

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RSSI_X: RSSI_X

Horizontal position on screen

- Range: 0 59

## OSD4_RSSI_Y: RSSI_Y

Vertical position on screen

- Range: 0 21

## OSD4_CURRENT_EN: CURRENT_EN

Displays main battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CURRENT_X: CURRENT_X

Horizontal position on screen

- Range: 0 59

## OSD4_CURRENT_Y: CURRENT_Y

Vertical position on screen

- Range: 0 21

## OSD4_BATUSED_EN: BATUSED_EN

Displays primary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_BATUSED_X: BATUSED_X

Horizontal position on screen

- Range: 0 59

## OSD4_BATUSED_Y: BATUSED_Y

Vertical position on screen

- Range: 0 21

## OSD4_SATS_EN: SATS_EN

Displays number of acquired satellites

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_SATS_X: SATS_X

Horizontal position on screen

- Range: 0 59

## OSD4_SATS_Y: SATS_Y

Vertical position on screen

- Range: 0 21

## OSD4_FLTMODE_EN: FLTMODE_EN

Displays flight mode

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_FLTMODE_X: FLTMODE_X

Horizontal position on screen

- Range: 0 59

## OSD4_FLTMODE_Y: FLTMODE_Y

Vertical position on screen

- Range: 0 21

## OSD4_MESSAGE_EN: MESSAGE_EN

Displays Mavlink messages

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_MESSAGE_X: MESSAGE_X

Horizontal position on screen

- Range: 0 59

## OSD4_MESSAGE_Y: MESSAGE_Y

Vertical position on screen

- Range: 0 21

## OSD4_GSPEED_EN: GSPEED_EN

Displays GPS ground speed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_GSPEED_X: GSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD4_GSPEED_Y: GSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD4_HORIZON_EN: HORIZON_EN

Displays artificial horizon

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_HORIZON_X: HORIZON_X

Horizontal position on screen

- Range: 0 59

## OSD4_HORIZON_Y: HORIZON_Y

Vertical position on screen

- Range: 0 21

## OSD4_HOME_EN: HOME_EN

Displays distance and relative direction to HOME

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_HOME_X: HOME_X

Horizontal position on screen

- Range: 0 59

## OSD4_HOME_Y: HOME_Y

Vertical position on screen

- Range: 0 21

## OSD4_HEADING_EN: HEADING_EN

Displays heading

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_HEADING_X: HEADING_X

Horizontal position on screen

- Range: 0 59

## OSD4_HEADING_Y: HEADING_Y

Vertical position on screen

- Range: 0 21

## OSD4_THROTTLE_EN: THROTTLE_EN

Displays actual throttle percentage being sent to motor(s)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_THROTTLE_X: THROTTLE_X

Horizontal position on screen

- Range: 0 59

## OSD4_THROTTLE_Y: THROTTLE_Y

Vertical position on screen

- Range: 0 21

## OSD4_COMPASS_EN: COMPASS_EN

Enables display of compass rose

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_COMPASS_X: COMPASS_X

Horizontal position on screen

- Range: 0 59

## OSD4_COMPASS_Y: COMPASS_Y

Vertical position on screen

- Range: 0 21

## OSD4_WIND_EN: WIND_EN

Displays wind speed and relative direction, on Rover this is the apparent wind speed and direction from the windvane, if fitted

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_WIND_X: WIND_X

Horizontal position on screen

- Range: 0 59

## OSD4_WIND_Y: WIND_Y

Vertical position on screen

- Range: 0 21

## OSD4_ASPEED_EN: ASPEED_EN

Displays airspeed value being used by TECS (fused value)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ASPEED_X: ASPEED_X

Horizontal position on screen

- Range: 0 59

## OSD4_ASPEED_Y: ASPEED_Y

Vertical position on screen

- Range: 0 21

## OSD4_VSPEED_EN: VSPEED_EN

Displays climb rate

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_VSPEED_X: VSPEED_X

Horizontal position on screen

- Range: 0 59

## OSD4_VSPEED_Y: VSPEED_Y

Vertical position on screen

- Range: 0 21

## OSD4_ESCTEMP_EN: ESCTEMP_EN

Displays highest temp of all active ESCs, or of a specific ECS if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ESCTEMP_X: ESCTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD4_ESCTEMP_Y: ESCTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD4_ESCRPM_EN: ESCRPM_EN

Displays highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ESCRPM_X: ESCRPM_X

Horizontal position on screen

- Range: 0 59

## OSD4_ESCRPM_Y: ESCRPM_Y

Vertical position on screen

- Range: 0 21

## OSD4_ESCAMPS_EN: ESCAMPS_EN

Displays the current of the ESC with the highest rpm of all active ESCs, or of a specific ESC if OSDx_ESC_IDX is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ESCAMPS_X: ESCAMPS_X

Horizontal position on screen

- Range: 0 59

## OSD4_ESCAMPS_Y: ESCAMPS_Y

Vertical position on screen

- Range: 0 21

## OSD4_GPSLAT_EN: GPSLAT_EN

Displays GPS latitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_GPSLAT_X: GPSLAT_X

Horizontal position on screen

- Range: 0 59

## OSD4_GPSLAT_Y: GPSLAT_Y

Vertical position on screen

- Range: 0 21

## OSD4_GPSLONG_EN: GPSLONG_EN

Displays GPS longitude

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_GPSLONG_X: GPSLONG_X

Horizontal position on screen

- Range: 0 59

## OSD4_GPSLONG_Y: GPSLONG_Y

Vertical position on screen

- Range: 0 21

## OSD4_ROLL_EN: ROLL_EN

Displays degrees of roll from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ROLL_X: ROLL_X

Horizontal position on screen

- Range: 0 59

## OSD4_ROLL_Y: ROLL_Y

Vertical position on screen

- Range: 0 21

## OSD4_PITCH_EN: PITCH_EN

Displays degrees of pitch from level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_PITCH_X: PITCH_X

Horizontal position on screen

- Range: 0 59

## OSD4_PITCH_Y: PITCH_Y

Vertical position on screen

- Range: 0 21

## OSD4_TEMP_EN: TEMP_EN

Displays temperature reported by primary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_TEMP_X: TEMP_X

Horizontal position on screen

- Range: 0 59

## OSD4_TEMP_Y: TEMP_Y

Vertical position on screen

- Range: 0 21

## OSD4_HDOP_EN: HDOP_EN

Displays Horizontal Dilution Of Position

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_HDOP_X: HDOP_X

Horizontal position on screen

- Range: 0 59

## OSD4_HDOP_Y: HDOP_Y

Vertical position on screen

- Range: 0 21

## OSD4_WAYPOINT_EN: WAYPOINT_EN

Displays bearing and distance to next waypoint

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_WAYPOINT_X: WAYPOINT_X

Horizontal position on screen

- Range: 0 59

## OSD4_WAYPOINT_Y: WAYPOINT_Y

Vertical position on screen

- Range: 0 21

## OSD4_XTRACK_EN: XTRACK_EN

Displays crosstrack error

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_XTRACK_X: XTRACK_X

Horizontal position on screen

- Range: 0 59

## OSD4_XTRACK_Y: XTRACK_Y

Vertical position on screen

- Range: 0 21

## OSD4_DIST_EN: DIST_EN

Displays total distance flown

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_DIST_X: DIST_X

Horizontal position on screen

- Range: 0 59

## OSD4_DIST_Y: DIST_Y

Vertical position on screen

- Range: 0 21

## OSD4_STATS_EN: STATS_EN

Displays flight stats

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_STATS_X: STATS_X

Horizontal position on screen

- Range: 0 59

## OSD4_STATS_Y: STATS_Y

Vertical position on screen

- Range: 0 21

## OSD4_FLTIME_EN: FLTIME_EN

Displays total flight time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_FLTIME_X: FLTIME_X

Horizontal position on screen

- Range: 0 59

## OSD4_FLTIME_Y: FLTIME_Y

Vertical position on screen

- Range: 0 21

## OSD4_CLIMBEFF_EN: CLIMBEFF_EN

Displays climb efficiency (climb rate/current)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CLIMBEFF_X: CLIMBEFF_X

Horizontal position on screen

- Range: 0 59

## OSD4_CLIMBEFF_Y: CLIMBEFF_Y

Vertical position on screen

- Range: 0 21

## OSD4_EFF_EN: EFF_EN

Displays flight efficiency (mAh/km or /mi)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_EFF_X: EFF_X

Horizontal position on screen

- Range: 0 59

## OSD4_EFF_Y: EFF_Y

Vertical position on screen

- Range: 0 21

## OSD4_BTEMP_EN: BTEMP_EN

Displays temperature reported by secondary barometer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_BTEMP_X: BTEMP_X

Horizontal position on screen

- Range: 0 59

## OSD4_BTEMP_Y: BTEMP_Y

Vertical position on screen

- Range: 0 21

## OSD4_ATEMP_EN: ATEMP_EN

Displays temperature reported by primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ATEMP_X: ATEMP_X

Horizontal position on screen

- Range: 0 59

## OSD4_ATEMP_Y: ATEMP_Y

Vertical position on screen

- Range: 0 21

## OSD4_BAT2_VLT_EN: BAT2VLT_EN

Displays battery2 voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_BAT2_VLT_X: BAT2VLT_X

Horizontal position on screen

- Range: 0 59

## OSD4_BAT2_VLT_Y: BAT2VLT_Y

Vertical position on screen

- Range: 0 21

## OSD4_BAT2USED_EN: BAT2USED_EN

Displays secondary battery mAh consumed

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_BAT2USED_X: BAT2USED_X

Horizontal position on screen

- Range: 0 59

## OSD4_BAT2USED_Y: BAT2USED_Y

Vertical position on screen

- Range: 0 21

## OSD4_ASPD2_EN: ASPD2_EN

Displays airspeed reported directly from secondary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ASPD2_X: ASPD2_X

Horizontal position on screen

- Range: 0 59

## OSD4_ASPD2_Y: ASPD2_Y

Vertical position on screen

- Range: 0 21

## OSD4_ASPD1_EN: ASPD1_EN

Displays airspeed reported directly from primary airspeed sensor

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ASPD1_X: ASPD1_X

Horizontal position on screen

- Range: 0 59

## OSD4_ASPD1_Y: ASPD1_Y

Vertical position on screen

- Range: 0 21

## OSD4_CLK_EN: CLK_EN

Displays a clock panel based on AP_RTC local time

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CLK_X: CLK_X

Horizontal position on screen

- Range: 0 59

## OSD4_CLK_Y: CLK_Y

Vertical position on screen

- Range: 0 21

## OSD4_SIDEBARS_EN: SIDEBARS_EN

Displays artificial horizon side bars

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_SIDEBARS_X: SIDEBARS_X

Horizontal position on screen

- Range: 0 59

## OSD4_SIDEBARS_Y: SIDEBARS_Y

Vertical position on screen

- Range: 0 21

## OSD4_CRSSHAIR_EN: CRSSHAIR_EN

Displays artificial horizon crosshair (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CRSSHAIR_X: CRSSHAIR_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD4_CRSSHAIR_Y: CRSSHAIR_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD4_HOMEDIST_EN: HOMEDIST_EN

Displays distance from HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_HOMEDIST_X: HOMEDIST_X

Horizontal position on screen (MSP OSD only)

- Range: 0 59

## OSD4_HOMEDIST_Y: HOMEDIST_Y

Vertical position on screen (MSP OSD only)

- Range: 0 21

## OSD4_HOMEDIR_EN: HOMEDIR_EN

Displays relative direction to HOME (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_HOMEDIR_X: HOMEDIR_X

Horizontal position on screen

- Range: 0 59

## OSD4_HOMEDIR_Y: HOMEDIR_Y

Vertical position on screen

- Range: 0 21

## OSD4_POWER_EN: POWER_EN

Displays power (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_POWER_X: POWER_X

Horizontal position on screen

- Range: 0 59

## OSD4_POWER_Y: POWER_Y

Vertical position on screen

- Range: 0 21

## OSD4_CELLVOLT_EN: CELL_VOLT_EN

Displays average cell voltage (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CELLVOLT_X: CELL_VOLT_X

Horizontal position on screen

- Range: 0 59

## OSD4_CELLVOLT_Y: CELL_VOLT_Y

Vertical position on screen

- Range: 0 21

## OSD4_BATTBAR_EN: BATT_BAR_EN

Displays battery usage bar (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_BATTBAR_X: BATT_BAR_X

Horizontal position on screen

- Range: 0 59

## OSD4_BATTBAR_Y: BATT_BAR_Y

Vertical position on screen

- Range: 0 21

## OSD4_ARMING_EN: ARMING_EN

Displays arming status (MSP OSD only)

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ARMING_X: ARMING_X

Horizontal position on screen

- Range: 0 59

## OSD4_ARMING_Y: ARMING_Y

Vertical position on screen

- Range: 0 21

## OSD4_PLUSCODE_EN: PLUSCODE_EN

Displays pluscode (OLC) element

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_PLUSCODE_X: PLUSCODE_X

Horizontal position on screen

- Range: 0 59

## OSD4_PLUSCODE_Y: PLUSCODE_Y

Vertical position on screen

- Range: 0 21

## OSD4_CALLSIGN_EN: CALLSIGN_EN

Displays callsign from callsign.txt on microSD card

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CALLSIGN_X: CALLSIGN_X

Horizontal position on screen

- Range: 0 59

## OSD4_CALLSIGN_Y: CALLSIGN_Y

Vertical position on screen

- Range: 0 21

## OSD4_CURRENT2_EN: CURRENT2_EN

Displays 2nd battery current

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_CURRENT2_X: CURRENT2_X

Horizontal position on screen

- Range: 0 59

## OSD4_CURRENT2_Y: CURRENT2_Y

Vertical position on screen

- Range: 0 21

## OSD4_VTX_PWR_EN: VTX_PWR_EN

Displays VTX Power

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_VTX_PWR_X: VTX_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD4_VTX_PWR_Y: VTX_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD4_TER_HGT_EN: TER_HGT_EN

Displays Height above terrain

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_TER_HGT_X: TER_HGT_X

Horizontal position on screen

- Range: 0 59

## OSD4_TER_HGT_Y: TER_HGT_Y

Vertical position on screen

- Range: 0 21

## OSD4_AVGCELLV_EN: AVGCELLV_EN

Displays average cell voltage. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_AVGCELLV_X: AVGCELLV_X

Horizontal position on screen

- Range: 0 59

## OSD4_AVGCELLV_Y: AVGCELLV_Y

Vertical position on screen

- Range: 0 21

## OSD4_RESTVOLT_EN: RESTVOLT_EN

Displays main battery resting voltage

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RESTVOLT_X: RESTVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD4_RESTVOLT_Y: RESTVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD4_FENCE_EN: FENCE_EN

Displays indication of fence enable and breach

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_FENCE_X: FENCE_X

Horizontal position on screen

- Range: 0 59

## OSD4_FENCE_Y: FENCE_Y

Vertical position on screen

- Range: 0 21

## OSD4_RNGF_EN: RNGF_EN

Displays a rangefinder's distance in cm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RNGF_X: RNGF_X

Horizontal position on screen

- Range: 0 59

## OSD4_RNGF_Y: RNGF_Y

Vertical position on screen

- Range: 0 21

## OSD4_ACRVOLT_EN: ACRVOLT_EN

Displays resting voltage for the average cell. WARNING: this can be inaccurate if the cell count is not detected or set properly. If the  the battery is far from fully charged the detected cell count might not be accurate if auto cell count detection is used (OSD_CELL_COUNT=0).

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_ACRVOLT_X: ACRVOLT_X

Horizontal position on screen

- Range: 0 59

## OSD4_ACRVOLT_Y: ACRVOLT_Y

Vertical position on screen

- Range: 0 21

## OSD4_RPM_EN: RPM_EN

Displays main rotor revs/min

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RPM_X: RPM_X

Horizontal position on screen

- Range: 0 29

## OSD4_RPM_Y: RPM_Y

Vertical position on screen

- Range: 0 15

## OSD4_LINK_Q_EN: LINK_Q_EN

Displays Receiver link quality

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_LINK_Q_X: LINK_Q_X

Horizontal position on screen

- Range: 0 59

## OSD4_LINK_Q_Y: LINK_Q_Y

Vertical position on screen

- Range: 0 21

## OSD4_TXT_RES: Sets the overlay text resolution (MSP DisplayPort only)

Sets the overlay text resolution for this screen to either SD 30x16 or HD 50x18/60x22 (MSP DisplayPort only)

|Value|Meaning|
|:---:|:---:|
|0|30x16|
|1|50x18|
|2|60x22|

## OSD4_FONT: Sets the font index for this screen (MSP DisplayPort only)

Sets the font index for this screen (MSP DisplayPort only)

- Range: 0 21

## OSD4_RC_PWR_EN: RC_PWR_EN

Displays the RC link transmit (TX) power in mW or W, depending on level

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RC_PWR_X: RC_PWR_X

Horizontal position on screen

- Range: 0 59

## OSD4_RC_PWR_Y: RC_PWR_Y

Vertical position on screen

- Range: 0 21

## OSD4_RSSIDBM_EN: RSSIDBM_EN

Displays RC link signal strength in dBm

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RSSIDBM_X: RSSIDBM_X

Horizontal position on screen

- Range: 0 59

## OSD4_RSSIDBM_Y: RSSIDBM_Y

Vertical position on screen

- Range: 0 21

## OSD4_RC_SNR_EN: RC_SNR_EN

Displays RC link signal to noise ratio in dB

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RC_SNR_X: RC_SNR_X

Horizontal position on screen

- Range: 0 59

## OSD4_RC_SNR_Y: RC_SNR_Y

Vertical position on screen

- Range: 0 21

## OSD4_RC_ANT_EN: RC_ANT_EN

Displays the current RC link active antenna

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RC_ANT_X: RC_ANT_X

Horizontal position on screen

- Range: 0 59

## OSD4_RC_ANT_Y: RC_ANT_Y

Vertical position on screen

- Range: 0 21

## OSD4_RC_LQ_EN: RC_LQ_EN

Displays the RC link quality (uplink, 0 to 100%) and also RF mode if bit 7 of OSD_OPTIONS is set

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD4_RC_LQ_X: RC_LQ_X

Horizontal position on screen

- Range: 0 59

## OSD4_RC_LQ_Y: RC_LQ_Y

Vertical position on screen

- Range: 0 21

## OSD4_ESC_IDX: ESC_IDX

Index of the ESC to use for displaying ESC information. 0 means use the ESC with the highest value.

- Range: 0 32

# OSD5 Parameters

## OSD5_ENABLE: Enable screen

Enable this screen

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_CHAN_MIN: Transmitter switch screen minimum pwm

This sets the PWM lower limit for this screen

- Range: 900 2100

## OSD5_CHAN_MAX: Transmitter switch screen maximum pwm

This sets the PWM upper limit for this screen

- Range: 900 2100

## OSD5_SAVE_X: SAVE_X

*Note: This parameter is for advanced users*

Horizontal position of Save button on screen

- Range: 0 25

## OSD5_SAVE_Y: SAVE_Y

*Note: This parameter is for advanced users*

Vertical position of Save button on screen

- Range: 0 15

# OSD5PARAM1 Parameters

## OSD5_PARAM1_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM1_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM1_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM1_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM1_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM1_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM1_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM1_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM1_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM1_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM2 Parameters

## OSD5_PARAM2_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM2_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM2_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM2_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM2_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM2_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM2_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM2_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM2_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM2_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM3 Parameters

## OSD5_PARAM3_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM3_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM3_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM3_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM3_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM3_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM3_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM3_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM3_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM3_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM4 Parameters

## OSD5_PARAM4_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM4_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM4_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM4_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM4_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM4_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM4_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM4_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM4_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM4_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM5 Parameters

## OSD5_PARAM5_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM5_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM5_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM5_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM5_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM5_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM5_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM5_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM5_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM5_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM6 Parameters

## OSD5_PARAM6_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM6_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM6_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM6_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM6_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM6_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM6_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM6_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM6_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM6_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM7 Parameters

## OSD5_PARAM7_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM7_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM7_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM7_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM7_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM7_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM7_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM7_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM7_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM7_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM8 Parameters

## OSD5_PARAM8_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM8_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM8_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM8_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM8_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM8_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM8_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM8_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM8_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM8_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD5PARAM9 Parameters

## OSD5_PARAM9_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD5_PARAM9_X: X position

Horizontal position on screen

- Range: 0 29

## OSD5_PARAM9_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD5_PARAM9_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD5_PARAM9_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD5_PARAM9_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD5_PARAM9_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD5_PARAM9_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD5_PARAM9_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD5_PARAM9_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6 Parameters

## OSD6_ENABLE: Enable screen

Enable this screen

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_CHAN_MIN: Transmitter switch screen minimum pwm

This sets the PWM lower limit for this screen

- Range: 900 2100

## OSD6_CHAN_MAX: Transmitter switch screen maximum pwm

This sets the PWM upper limit for this screen

- Range: 900 2100

## OSD6_SAVE_X: SAVE_X

*Note: This parameter is for advanced users*

Horizontal position of Save button on screen

- Range: 0 25

## OSD6_SAVE_Y: SAVE_Y

*Note: This parameter is for advanced users*

Vertical position of Save button on screen

- Range: 0 15

# OSD6PARAM1 Parameters

## OSD6_PARAM1_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM1_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM1_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM1_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM1_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM1_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM1_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM1_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM1_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM1_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM2 Parameters

## OSD6_PARAM2_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM2_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM2_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM2_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM2_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM2_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM2_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM2_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM2_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM2_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM3 Parameters

## OSD6_PARAM3_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM3_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM3_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM3_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM3_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM3_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM3_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM3_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM3_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM3_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM4 Parameters

## OSD6_PARAM4_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM4_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM4_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM4_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM4_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM4_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM4_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM4_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM4_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM4_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM5 Parameters

## OSD6_PARAM5_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM5_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM5_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM5_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM5_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM5_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM5_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM5_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM5_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM5_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM6 Parameters

## OSD6_PARAM6_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM6_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM6_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM6_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM6_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM6_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM6_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM6_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM6_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM6_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM7 Parameters

## OSD6_PARAM7_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM7_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM7_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM7_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM7_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM7_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM7_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM7_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM7_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM7_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM8 Parameters

## OSD6_PARAM8_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM8_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM8_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM8_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM8_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM8_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM8_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM8_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM8_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM8_TYPE: Parameter type

Type of the parameter to be displayed and modified

# OSD6PARAM9 Parameters

## OSD6_PARAM9_EN: Enable

Enable setting

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## OSD6_PARAM9_X: X position

Horizontal position on screen

- Range: 0 29

## OSD6_PARAM9_Y: Y position

Vertical position on screen

- Range: 0 15

## OSD6_PARAM9_KEY: Parameter key

Key of the parameter to be displayed and modified

## OSD6_PARAM9_IDX: Parameter index

Index of the parameter to be displayed and modified

## OSD6_PARAM9_GRP: Parameter group

Group of the parameter to be displayed and modified

## OSD6_PARAM9_MIN: Parameter minimum

Minimum value of the parameter to be displayed and modified

## OSD6_PARAM9_MAX: Parameter maximum

Maximum of the parameter to be displayed and modified

## OSD6_PARAM9_INCR: Parameter increment

Increment of the parameter to be displayed and modified

## OSD6_PARAM9_TYPE: Parameter type

Type of the parameter to be displayed and modified

# PLND Parameters

## PLND_ENABLED: Precision Land enabled/disabled

*Note: This parameter is for advanced users*

Precision Land enabled/disabled

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## PLND_TYPE: Precision Land Type

*Note: This parameter is for advanced users*

Precision Land Type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MAVLink|
|2|IRLock|
|3|SITL_Gazebo|
|4|SITL|

## PLND_YAW_ALIGN: Sensor yaw alignment

*Note: This parameter is for advanced users*

Yaw angle from body x-axis to sensor x-axis.

- Range: 0 36000

- Increment: 10

- Units: cdeg

## PLND_LAND_OFS_X: Land offset forward

*Note: This parameter is for advanced users*

Desired landing position of the camera forward of the target in vehicle body frame

- Range: -20 20

- Increment: 1

- Units: cm

## PLND_LAND_OFS_Y: Land offset right

*Note: This parameter is for advanced users*

desired landing position of the camera right of the target in vehicle body frame

- Range: -20 20

- Increment: 1

- Units: cm

## PLND_EST_TYPE: Precision Land Estimator Type

*Note: This parameter is for advanced users*

Specifies the estimation method to be used

|Value|Meaning|
|:---:|:---:|
|0|RawSensor|
|1|KalmanFilter|

## PLND_ACC_P_NSE: Kalman Filter Accelerometer Noise

*Note: This parameter is for advanced users*

Kalman Filter Accelerometer Noise, higher values weight the input from the camera more, accels less

- Range: 0.5 5

## PLND_CAM_POS_X: Camera X position offset

*Note: This parameter is for advanced users*

X position of the camera in body frame. Positive X is forward of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## PLND_CAM_POS_Y: Camera Y position offset

*Note: This parameter is for advanced users*

Y position of the camera in body frame. Positive Y is to the right of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## PLND_CAM_POS_Z: Camera Z position offset

*Note: This parameter is for advanced users*

Z position of the camera in body frame. Positive Z is down from the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## PLND_BUS: Sensor Bus

*Note: This parameter is for advanced users*

Precland sensor bus for I2C sensors.

|Value|Meaning|
|:---:|:---:|
|-1|DefaultBus|
|0|InternalI2C|
|1|ExternalI2C|

## PLND_LAG: Precision Landing sensor lag

*Note: This parameter is for advanced users*

Precision Landing sensor lag, to cope with variable landing_target latency

- Range: 0.02 0.250

- Increment: 1

- Units: s

- RebootRequired: True

## PLND_XY_DIST_MAX: Precision Landing maximum distance to target before descending

*Note: This parameter is for advanced users*

The vehicle will not start descending if the landing target is detected and it is further than this many meters away. Set 0 to always descend.

- Range: 0 10

- Units: m

## PLND_STRICT: PrecLand strictness

How strictly should the vehicle land on the target if target is lost

|Value|Meaning|
|:---:|:---:|
|0|Land Vertically (Not strict)|
|1|Retry Landing(Normal Strictness)|
|2|Do not land (just Hover) (Very Strict)|

## PLND_RET_MAX: PrecLand Maximum number of retires for a failed landing

PrecLand Maximum number of retires for a failed landing. Set to zero to disable landing retry.

- Range: 0 10

- Increment: 1

## PLND_TIMEOUT: PrecLand retry timeout

Time for which vehicle continues descend even if target is lost. After this time period, vehicle will attempt a landing retry depending on PLND_STRICT parameter.

- Range: 0 20

- Units: s

## PLND_RET_BEHAVE: PrecLand retry behaviour

Prec Land will do the action selected by this parameter if a retry to a landing is needed

|Value|Meaning|
|:---:|:---:|
|0|Go to the last location where landing target was detected|
|1|Go towards the approximate location of the detected landing target|

## PLND_ALT_MIN: PrecLand minimum alt for retry

Vehicle will continue landing vertically even if target is lost below this height. This needs a rangefinder to work. Set to zero to disable this.

- Range: 0 5

- Units: m

## PLND_ALT_MAX: PrecLand maximum alt for retry

Vehicle will continue landing vertically until this height if target is not found. Below this height if landing target is not found, landing retry/failsafe might be attempted. This needs a rangefinder to work. Set to zero to disable this.

- Range: 0 50

- Units: m

## PLND_OPTIONS: Precision Landing Extra Options

*Note: This parameter is for advanced users*

Precision Landing Extra Options

- Bitmask: 0: Moving Landing Target, 1: Allow Precision Landing after manual reposition, 2: Maintain high speed in final descent

## PLND_ORIENT: Camera Orientation

*Note: This parameter is for advanced users*

Orientation of camera/sensor on body

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|4|Back|
|25|Down|

- RebootRequired: True

# PRX Parameters

## PRX_LOG_RAW: Proximity raw distances log

*Note: This parameter is for advanced users*

Set this parameter to one if logging unfiltered(raw) distances from sensor should be enabled

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|

## PRX_FILT: Proximity filter cutoff frequency

*Note: This parameter is for advanced users*

Cutoff frequency for low pass filter applied to each face in the proximity boundary

- Units: Hz

- Range: 0 20

# PRX1 Parameters

## PRX1_TYPE: Proximity type

What type of proximity sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|7|LightwareSF40c|
|2|MAVLink|
|3|TeraRangerTower|
|4|RangeFinder|
|5|RPLidarA2|
|6|TeraRangerTowerEvo|
|8|LightwareSF45B|
|10|SITL|
|12|AirSimSITL|
|13|CygbotD1|
|14|DroneCAN|
|15|Scripting|
|16|LD06|
|17|MR72_CAN|
|18|HexsoonRadar|

- RebootRequired: True

## PRX1_ORIENT: Proximity sensor orientation

Proximity sensor orientation

|Value|Meaning|
|:---:|:---:|
|0|Default|
|1|Upside Down|

## PRX1_YAW_CORR: Proximity sensor yaw correction

Proximity sensor yaw correction

- Units: deg

- Range: -180 180

## PRX1_IGN_ANG1: Proximity sensor ignore angle 1

Proximity sensor ignore angle 1

- Units: deg

- Range: 0 360

## PRX1_IGN_WID1: Proximity sensor ignore width 1

Proximity sensor ignore width 1

- Units: deg

- Range: 0 127

## PRX1_IGN_ANG2: Proximity sensor ignore angle 2

Proximity sensor ignore angle 2

- Units: deg

- Range: 0 360

## PRX1_IGN_WID2: Proximity sensor ignore width 2

Proximity sensor ignore width 2

- Units: deg

- Range: 0 127

## PRX1_IGN_ANG3: Proximity sensor ignore angle 3

Proximity sensor ignore angle 3

- Units: deg

- Range: 0 360

## PRX1_IGN_WID3: Proximity sensor ignore width 3

Proximity sensor ignore width 3

- Units: deg

- Range: 0 127

## PRX1_IGN_ANG4: Proximity sensor ignore angle 4

Proximity sensor ignore angle 4

- Units: deg

- Range: 0 360

## PRX1_IGN_WID4: Proximity sensor ignore width 4

Proximity sensor ignore width 4

- Units: deg

- Range: 0 127

## PRX1_MIN: Proximity minimum range

*Note: This parameter is for advanced users*

Minimum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX1_MAX: Proximity maximum range

*Note: This parameter is for advanced users*

Maximum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX1_ADDR: Bus address of sensor

The bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

# PRX1 Parameters

## PRX1_RECV_ID: CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

# PRX2 Parameters

## PRX2_TYPE: Proximity type

What type of proximity sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|7|LightwareSF40c|
|2|MAVLink|
|3|TeraRangerTower|
|4|RangeFinder|
|5|RPLidarA2|
|6|TeraRangerTowerEvo|
|8|LightwareSF45B|
|10|SITL|
|12|AirSimSITL|
|13|CygbotD1|
|14|DroneCAN|
|15|Scripting|
|16|LD06|
|17|MR72_CAN|
|18|HexsoonRadar|

- RebootRequired: True

## PRX2_ORIENT: Proximity sensor orientation

Proximity sensor orientation

|Value|Meaning|
|:---:|:---:|
|0|Default|
|1|Upside Down|

## PRX2_YAW_CORR: Proximity sensor yaw correction

Proximity sensor yaw correction

- Units: deg

- Range: -180 180

## PRX2_IGN_ANG1: Proximity sensor ignore angle 1

Proximity sensor ignore angle 1

- Units: deg

- Range: 0 360

## PRX2_IGN_WID1: Proximity sensor ignore width 1

Proximity sensor ignore width 1

- Units: deg

- Range: 0 127

## PRX2_IGN_ANG2: Proximity sensor ignore angle 2

Proximity sensor ignore angle 2

- Units: deg

- Range: 0 360

## PRX2_IGN_WID2: Proximity sensor ignore width 2

Proximity sensor ignore width 2

- Units: deg

- Range: 0 127

## PRX2_IGN_ANG3: Proximity sensor ignore angle 3

Proximity sensor ignore angle 3

- Units: deg

- Range: 0 360

## PRX2_IGN_WID3: Proximity sensor ignore width 3

Proximity sensor ignore width 3

- Units: deg

- Range: 0 127

## PRX2_IGN_ANG4: Proximity sensor ignore angle 4

Proximity sensor ignore angle 4

- Units: deg

- Range: 0 360

## PRX2_IGN_WID4: Proximity sensor ignore width 4

Proximity sensor ignore width 4

- Units: deg

- Range: 0 127

## PRX2_MIN: Proximity minimum range

*Note: This parameter is for advanced users*

Minimum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX2_MAX: Proximity maximum range

*Note: This parameter is for advanced users*

Maximum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX2_ADDR: Bus address of sensor

The bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

# PRX2 Parameters

## PRX2_RECV_ID: CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

# PRX3 Parameters

## PRX3_TYPE: Proximity type

What type of proximity sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|7|LightwareSF40c|
|2|MAVLink|
|3|TeraRangerTower|
|4|RangeFinder|
|5|RPLidarA2|
|6|TeraRangerTowerEvo|
|8|LightwareSF45B|
|10|SITL|
|12|AirSimSITL|
|13|CygbotD1|
|14|DroneCAN|
|15|Scripting|
|16|LD06|
|17|MR72_CAN|
|18|HexsoonRadar|

- RebootRequired: True

## PRX3_ORIENT: Proximity sensor orientation

Proximity sensor orientation

|Value|Meaning|
|:---:|:---:|
|0|Default|
|1|Upside Down|

## PRX3_YAW_CORR: Proximity sensor yaw correction

Proximity sensor yaw correction

- Units: deg

- Range: -180 180

## PRX3_IGN_ANG1: Proximity sensor ignore angle 1

Proximity sensor ignore angle 1

- Units: deg

- Range: 0 360

## PRX3_IGN_WID1: Proximity sensor ignore width 1

Proximity sensor ignore width 1

- Units: deg

- Range: 0 127

## PRX3_IGN_ANG2: Proximity sensor ignore angle 2

Proximity sensor ignore angle 2

- Units: deg

- Range: 0 360

## PRX3_IGN_WID2: Proximity sensor ignore width 2

Proximity sensor ignore width 2

- Units: deg

- Range: 0 127

## PRX3_IGN_ANG3: Proximity sensor ignore angle 3

Proximity sensor ignore angle 3

- Units: deg

- Range: 0 360

## PRX3_IGN_WID3: Proximity sensor ignore width 3

Proximity sensor ignore width 3

- Units: deg

- Range: 0 127

## PRX3_IGN_ANG4: Proximity sensor ignore angle 4

Proximity sensor ignore angle 4

- Units: deg

- Range: 0 360

## PRX3_IGN_WID4: Proximity sensor ignore width 4

Proximity sensor ignore width 4

- Units: deg

- Range: 0 127

## PRX3_MIN: Proximity minimum range

*Note: This parameter is for advanced users*

Minimum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX3_MAX: Proximity maximum range

*Note: This parameter is for advanced users*

Maximum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX3_ADDR: Bus address of sensor

The bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

# PRX3 Parameters

## PRX3_RECV_ID: CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

# PRX4 Parameters

## PRX4_TYPE: Proximity type

What type of proximity sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|7|LightwareSF40c|
|2|MAVLink|
|3|TeraRangerTower|
|4|RangeFinder|
|5|RPLidarA2|
|6|TeraRangerTowerEvo|
|8|LightwareSF45B|
|10|SITL|
|12|AirSimSITL|
|13|CygbotD1|
|14|DroneCAN|
|15|Scripting|
|16|LD06|
|17|MR72_CAN|
|18|HexsoonRadar|

- RebootRequired: True

## PRX4_ORIENT: Proximity sensor orientation

Proximity sensor orientation

|Value|Meaning|
|:---:|:---:|
|0|Default|
|1|Upside Down|

## PRX4_YAW_CORR: Proximity sensor yaw correction

Proximity sensor yaw correction

- Units: deg

- Range: -180 180

## PRX4_IGN_ANG1: Proximity sensor ignore angle 1

Proximity sensor ignore angle 1

- Units: deg

- Range: 0 360

## PRX4_IGN_WID1: Proximity sensor ignore width 1

Proximity sensor ignore width 1

- Units: deg

- Range: 0 127

## PRX4_IGN_ANG2: Proximity sensor ignore angle 2

Proximity sensor ignore angle 2

- Units: deg

- Range: 0 360

## PRX4_IGN_WID2: Proximity sensor ignore width 2

Proximity sensor ignore width 2

- Units: deg

- Range: 0 127

## PRX4_IGN_ANG3: Proximity sensor ignore angle 3

Proximity sensor ignore angle 3

- Units: deg

- Range: 0 360

## PRX4_IGN_WID3: Proximity sensor ignore width 3

Proximity sensor ignore width 3

- Units: deg

- Range: 0 127

## PRX4_IGN_ANG4: Proximity sensor ignore angle 4

Proximity sensor ignore angle 4

- Units: deg

- Range: 0 360

## PRX4_IGN_WID4: Proximity sensor ignore width 4

Proximity sensor ignore width 4

- Units: deg

- Range: 0 127

## PRX4_MIN: Proximity minimum range

*Note: This parameter is for advanced users*

Minimum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX4_MAX: Proximity maximum range

*Note: This parameter is for advanced users*

Maximum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX4_ADDR: Bus address of sensor

The bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

# PRX4 Parameters

## PRX4_RECV_ID: CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

# PRX5 Parameters

## PRX5_TYPE: Proximity type

What type of proximity sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|7|LightwareSF40c|
|2|MAVLink|
|3|TeraRangerTower|
|4|RangeFinder|
|5|RPLidarA2|
|6|TeraRangerTowerEvo|
|8|LightwareSF45B|
|10|SITL|
|12|AirSimSITL|
|13|CygbotD1|
|14|DroneCAN|
|15|Scripting|
|16|LD06|
|17|MR72_CAN|
|18|HexsoonRadar|

- RebootRequired: True

## PRX5_ORIENT: Proximity sensor orientation

Proximity sensor orientation

|Value|Meaning|
|:---:|:---:|
|0|Default|
|1|Upside Down|

## PRX5_YAW_CORR: Proximity sensor yaw correction

Proximity sensor yaw correction

- Units: deg

- Range: -180 180

## PRX5_IGN_ANG1: Proximity sensor ignore angle 1

Proximity sensor ignore angle 1

- Units: deg

- Range: 0 360

## PRX5_IGN_WID1: Proximity sensor ignore width 1

Proximity sensor ignore width 1

- Units: deg

- Range: 0 127

## PRX5_IGN_ANG2: Proximity sensor ignore angle 2

Proximity sensor ignore angle 2

- Units: deg

- Range: 0 360

## PRX5_IGN_WID2: Proximity sensor ignore width 2

Proximity sensor ignore width 2

- Units: deg

- Range: 0 127

## PRX5_IGN_ANG3: Proximity sensor ignore angle 3

Proximity sensor ignore angle 3

- Units: deg

- Range: 0 360

## PRX5_IGN_WID3: Proximity sensor ignore width 3

Proximity sensor ignore width 3

- Units: deg

- Range: 0 127

## PRX5_IGN_ANG4: Proximity sensor ignore angle 4

Proximity sensor ignore angle 4

- Units: deg

- Range: 0 360

## PRX5_IGN_WID4: Proximity sensor ignore width 4

Proximity sensor ignore width 4

- Units: deg

- Range: 0 127

## PRX5_MIN: Proximity minimum range

*Note: This parameter is for advanced users*

Minimum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX5_MAX: Proximity maximum range

*Note: This parameter is for advanced users*

Maximum expected range for Proximity Sensor. Setting this to 0 will set value to manufacturer reported range.

- Units: m

- Range: 0 500

## PRX5_ADDR: Bus address of sensor

The bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

# PRX5 Parameters

## PRX5_RECV_ID: CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

# PSC Parameters

## PSC_POS_P: Position controller P gain

Position controller P gain.  Converts the distance to the target location into a desired speed which is then passed to the loiter latitude rate controller

- Range: 0.500 2.000

## PSC_VEL_P: Velocity (horizontal) P gain

*Note: This parameter is for advanced users*

Velocity (horizontal) P gain.  Converts the difference between desired and actual velocity to a target acceleration

- Range: 0.1 6.0

- Increment: 0.1

## PSC_VEL_I: Velocity (horizontal) I gain

*Note: This parameter is for advanced users*

Velocity (horizontal) I gain.  Corrects long-term difference between desired and actual velocity to a target acceleration

- Range: 0.00 1.00

- Increment: 0.01

## PSC_VEL_D: Velocity (horizontal) D gain

*Note: This parameter is for advanced users*

Velocity (horizontal) D gain.  Corrects short-term changes in velocity

- Range: 0.00 1.00

- Increment: 0.001

## PSC_VEL_IMAX: Velocity (horizontal) integrator maximum

*Note: This parameter is for advanced users*

Velocity (horizontal) integrator maximum.  Constrains the target acceleration that the I gain will output

- Range: 0 4500

- Increment: 10

- Units: cm/s/s

## PSC_VEL_FLTE: Velocity (horizontal) input filter

*Note: This parameter is for advanced users*

Velocity (horizontal) input filter.  This filter (in Hz) is applied to the input for P and I terms

- Range: 0 100

- Units: Hz

## PSC_VEL_FLTD: Velocity (horizontal) input filter

*Note: This parameter is for advanced users*

Velocity (horizontal) input filter.  This filter (in Hz) is applied to the input for D term

- Range: 0 100

- Units: Hz

## PSC_VEL_FF: Velocity (horizontal) feed forward gain

*Note: This parameter is for advanced users*

Velocity (horizontal) feed forward gain.  Converts the difference between desired velocity to a target acceleration

- Range: 0 6

- Increment: 0.01

# RALLY Parameters

## RALLY_TOTAL: Rally Total

*Note: This parameter is for advanced users*

Number of rally points currently loaded

## RALLY_LIMIT_KM: Rally Limit

*Note: This parameter is for advanced users*

Maximum distance to rally point. If the closest rally point is more than this number of kilometers from the current position and the home location is closer than any of the rally points from the current position then do RTL to home rather than to the closest rally point. This prevents a leftover rally point from a different airfield being used accidentally. If this is set to 0 then the closest rally point is always used.

- Units: km

- Increment: 0.1

## RALLY_INCL_HOME: Rally Include Home

Controls if Home is included as a Rally point (i.e. as a safe landing place) for RTL

|Value|Meaning|
|:---:|:---:|
|0|DoNotIncludeHome|
|1|IncludeHome|

# RC Parameters

## RC_OVERRIDE_TIME: RC override timeout

*Note: This parameter is for advanced users*

Timeout after which RC overrides will no longer be used, and RC input will resume, 0 will disable RC overrides, -1 will never timeout, and continue using overrides until they are disabled

- Range: 0.0 120.0

- Units: s

## RC_OPTIONS: RC options

*Note: This parameter is for advanced users*

RC input options

- Bitmask: 0:Ignore RC Receiver, 1:Ignore MAVLink Overrides, 2:Ignore Receiver Failsafe bit but allow other RC failsafes if setup, 3:FPort Pad, 4:Log RC input bytes, 5:Arming check throttle for 0 input, 6:Skip the arming check for neutral Roll/Pitch/Yaw sticks, 7:Allow Switch reverse, 8:Use passthrough for CRSF telemetry, 9:Suppress CRSF mode/rate message for ELRS systems,10:Enable multiple receiver support, 11:Use Link Quality for RSSI with CRSF, 12:Annotate CRSF flight mode with * on disarm, 13: Use 420kbaud for ELRS protocol

## RC_PROTOCOLS: RC protocols enabled

*Note: This parameter is for advanced users*

Bitmask of enabled RC protocols. Allows narrowing the protocol detection to only specific types of RC receivers which can avoid issues with incorrect detection. Set to 1 to enable all protocols.

- Bitmask: 0:All,1:PPM,2:IBUS,3:SBUS,4:SBUS_NI,5:DSM,6:SUMD,7:SRXL,8:SRXL2,9:CRSF,10:ST24,11:FPORT,12:FPORT2,13:FastSBUS,14:DroneCAN,15:Ghost,16:MAVRadio

## RC_FS_TIMEOUT: RC Failsafe timeout

RC failsafe will trigger this many seconds after loss of RC

- Range: 0.5 10.0

- Units: s

# RCn Parameters

## RCn_MIN: RC min PWM

*Note: This parameter is for advanced users*

RC minimum PWM pulse width in microseconds. Typically 1000 is lower limit, 1500 is neutral and 2000 is upper limit.

- Units: PWM

- Range: 800 2200

- Increment: 1

## RCn_TRIM: RC trim PWM

*Note: This parameter is for advanced users*

RC trim (neutral) PWM pulse width in microseconds. Typically 1000 is lower limit, 1500 is neutral and 2000 is upper limit.

- Units: PWM

- Range: 800 2200

- Increment: 1

## RCn_MAX: RC max PWM

*Note: This parameter is for advanced users*

RC maximum PWM pulse width in microseconds. Typically 1000 is lower limit, 1500 is neutral and 2000 is upper limit.

- Units: PWM

- Range: 800 2200

- Increment: 1

## RCn_REVERSED: RC reversed

*Note: This parameter is for advanced users*

Reverse channel input. Set to 0 for normal operation. Set to 1 to reverse this input channel.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Reversed|

## RCn_DZ: RC dead-zone

*Note: This parameter is for advanced users*

PWM dead zone in microseconds around trim or bottom

- Units: PWM

- Range: 0 200

## RCn_OPTION: RC input option

Function assigned to this RC channel

|Value|Meaning|
|:---:|:---:|
|0|Do Nothing|
|4|RTL|
|5|Save Trim (4.1 and lower)|
|7|Save WP|
|9|Camera Trigger|
|11|Fence Enable|
|16|AUTO Mode|
|19|Gripper Release|
|24|Auto Mission Reset|
|27|Retract Mount1|
|28|Relay1 On/Off|
|30|Lost Rover Sound|
|31|Motor Emergency Stop|
|34|Relay2 On/Off|
|35|Relay3 On/Off|
|36|Relay4 On/Off|
|40|Proximity Avoidance Enable|
|41|ArmDisarm (4.1 and lower)|
|42|SMARTRTL Mode|
|46|RC Override Enable|
|50|LearnCruise Speed|
|51|MANUAL Mode|
|52|ACRO Mode|
|53|STEERING Mode|
|54|HOLD Mode|
|55|GUIDED Mode|
|56|LOITER Mode|
|57|FOLLOW Mode|
|58|Clear Waypoints|
|59|Simple Mode|
|62|Compass Learn|
|63|Sailboat Tack|
|65|GPS Disable|
|66|Relay5 On/Off|
|67|Relay6 On/Off|
|72|CIRCLE Mode|
|74|Sailboat motoring 3pos|
|78|RunCam Control|
|79|RunCam OSD Control|
|80|VisoOdom Align|
|81|Disarm|
|90|EKF Source Set|
|94|VTX Power|
|97|Windvane home heading direction offset|
|100|KillIMU1|
|101|KillIMU2|
|102|Camera Mode Toggle|
|105|GPS Disable Yaw|
|106|Disable Airspeed Use|
|110|KillIMU3|
|112|SwitchExternalAHRS|
|113|Retract Mount2|
|153|ArmDisarm (4.2 and higher)|
|155|Set steering trim to current servo and RC|
|156|Torqeedo Clear Err|
|162|FFT Tune|
|163|Mount Lock|
|164|Pause Stream Logging|
|165|Arm/Emergency Motor Stop|
|166|Camera Record Video|
|167|Camera Zoom|
|168|Camera Manual Focus|
|169|Camera Auto Focus|
|171|Calibrate Compasses|
|172|Battery MPPT Enable|
|174|Camera Image Tracking|
|175|Camera Lens|
|177|Mount LRF enable|
|201|Roll|
|202|Pitch|
|207|MainSail|
|208|Flap|
|211|Walking Height|
|212|Mount1 Roll|
|213|Mount1 Pitch|
|214|Mount1 Yaw|
|215|Mount2 Roll|
|216|Mount2 Pitch|
|217|Mount2 Yaw|
|300|Scripting1|
|301|Scripting2|
|302|Scripting3|
|303|Scripting4|
|304|Scripting5|
|305|Scripting6|
|306|Scripting7|
|307|Scripting8|

# RCMAP Parameters

## RCMAP_ROLL: Roll channel

*Note: This parameter is for advanced users*

Roll channel number. This is useful when you have a RC transmitter that can't change the channel order easily. Roll is normally on channel 1, but you can move it to any channel with this parameter.  Reboot is required for changes to take effect.

- Range: 1 16

- Increment: 1

- RebootRequired: True

## RCMAP_PITCH: Pitch channel

*Note: This parameter is for advanced users*

Pitch channel number. This is useful when you have a RC transmitter that can't change the channel order easily. Pitch is normally on channel 2, but you can move it to any channel with this parameter.  Reboot is required for changes to take effect.

- Range: 1 16

- Increment: 1

- RebootRequired: True

## RCMAP_THROTTLE: Throttle channel

*Note: This parameter is for advanced users*

Throttle channel number. This is useful when you have a RC transmitter that can't change the channel order easily. Throttle is normally on channel 3, but you can move it to any channel with this parameter. Reboot is required for changes to take effect.

- Range: 1 16

- Increment: 1

- RebootRequired: True

## RCMAP_YAW: Yaw channel

*Note: This parameter is for advanced users*

Yaw channel number. This is useful when you have a RC transmitter that can't change the channel order easily. Yaw (also known as rudder) is normally on channel 4, but you can move it to any channel with this parameter.  Reboot is required for changes to take effect.

- Range: 1 16

- Increment: 1

- RebootRequired: True

# RELAY10 Parameters

## RELAY10_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY10_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY10_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY10_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY11 Parameters

## RELAY11_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY11_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY11_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY11_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY12 Parameters

## RELAY12_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY12_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY12_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY12_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY13 Parameters

## RELAY13_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY13_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY13_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY13_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY14 Parameters

## RELAY14_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY14_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY14_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY14_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY15 Parameters

## RELAY15_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY15_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY15_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY15_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY16 Parameters

## RELAY16_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY16_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY16_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY16_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY1 Parameters

## RELAY1_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY1_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY1_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY1_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY2 Parameters

## RELAY2_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY2_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY2_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY2_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY3 Parameters

## RELAY3_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY3_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY3_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY3_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY4 Parameters

## RELAY4_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY4_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY4_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY4_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY5 Parameters

## RELAY5_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY5_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY5_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY5_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY6 Parameters

## RELAY6_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY6_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY6_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY6_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY7 Parameters

## RELAY7_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY7_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY7_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY7_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY8 Parameters

## RELAY8_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY8_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY8_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY8_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RELAY9 Parameters

## RELAY9_FUNCTION: Relay function

The function the relay channel is mapped to.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Relay|
|4|Camera|
|5|Bushed motor reverse 1 throttle or throttle-left or omni motor 1|
|6|Bushed motor reverse 2 throttle-right or omni motor 2|
|7|Bushed motor reverse 3 omni motor 3|
|8|Bushed motor reverse 4 omni motor 4|

## RELAY9_PIN: Relay pin

Digital pin number for relay control. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|49|BB Blue GP0 pin 4|
|50|AUXOUT1|
|51|AUXOUT2|
|52|AUXOUT3|
|53|AUXOUT4|
|54|AUXOUT5|
|55|AUXOUT6|
|57|BB Blue GP0 pin 3|
|113|BB Blue GP0 pin 6|
|116|BB Blue GP0 pin 5|
|62|BBBMini Pin P8.13|
|101|MainOut1|
|102|MainOut2|
|103|MainOut3|
|104|MainOut4|
|105|MainOut5|
|106|MainOut6|
|107|MainOut7|
|108|MainOut8|
|1000|DroneCAN Hardpoint ID 0|
|1001|DroneCAN Hardpoint ID 1|
|1002|DroneCAN Hardpoint ID 2|
|1003|DroneCAN Hardpoint ID 3|
|1004|DroneCAN Hardpoint ID 4|
|1005|DroneCAN Hardpoint ID 5|
|1006|DroneCAN Hardpoint ID 6|
|1007|DroneCAN Hardpoint ID 7|
|1008|DroneCAN Hardpoint ID 8|
|1009|DroneCAN Hardpoint ID 9|
|1010|DroneCAN Hardpoint ID 10|
|1011|DroneCAN Hardpoint ID 11|
|1012|DroneCAN Hardpoint ID 12|
|1013|DroneCAN Hardpoint ID 13|
|1014|DroneCAN Hardpoint ID 14|
|1015|DroneCAN Hardpoint ID 15|

## RELAY9_DEFAULT: Relay default state

Should the relay default to on or off, this only applies to RELAYx_FUNC "Relay" (1). All other uses will pick the appropriate default output state from within the controlling function's parameters. Note that if INVERTED is set then the default is inverted.

|Value|Meaning|
|:---:|:---:|
|0|Off|
|1|On|
|2|NoChange|

## RELAY9_INVERTED: Relay invert output signal

Should the relay output signal be inverted. If enabled, relay on would be pin low and relay off would be pin high. NOTE: this impact's DEFAULT.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Inverted|

# RNGFND1 Parameters

## RNGFND1_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND1_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND1_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND1_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND1_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND1_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND1_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND1_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND1_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND1_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND1_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND1_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND1_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND1_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND1_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND1_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND1_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND1_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND1_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND1_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND1_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND1_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND1_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND1_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND2 Parameters

## RNGFND2_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND2_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND2_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND2_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND2_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND2_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND2_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND2_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND2_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND2_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND2_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND2_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND2_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND2_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND2_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND2_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND2_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND2_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND2_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND2_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND2_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND2_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND2_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND2_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND3 Parameters

## RNGFND3_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND3_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND3_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND3_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND3_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND3_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND3_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND3_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND3_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND3_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND3_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND3_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND3_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND3_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND3_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND3_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND3_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND3_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND3_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND3_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND3_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND3_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND3_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND3_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND4 Parameters

## RNGFND4_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND4_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND4_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND4_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND4_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND4_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND4_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND4_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND4_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND4_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND4_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND4_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND4_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND4_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND4_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND4_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND4_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND4_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND4_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND4_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND4_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND4_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND4_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND4_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND5 Parameters

## RNGFND5_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND5_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND5_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND5_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND5_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND5_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND5_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND5_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND5_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND5_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND5_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND5_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND5_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND5_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND5_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND5_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND5_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND5_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND5_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND5_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND5_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND5_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND5_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND5_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND6 Parameters

## RNGFND6_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND6_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND6_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND6_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND6_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND6_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND6_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND6_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND6_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND6_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND6_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND6_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND6_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND6_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND6_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND6_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND6_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND6_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND6_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND6_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND6_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND6_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND6_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND6_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND7 Parameters

## RNGFND7_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND7_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND7_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND7_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND7_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND7_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND7_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND7_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND7_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND7_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND7_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND7_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND7_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND7_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND7_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND7_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND7_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND7_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND7_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND7_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND7_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND7_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND7_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND7_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND8 Parameters

## RNGFND8_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND8_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND8_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND8_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND8_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND8_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND8_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND8_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND8_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND8_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND8_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND8_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND8_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND8_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND8_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND8_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND8_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND8_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND8_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND8_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND8_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND8_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND8_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND8_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFND9 Parameters

## RNGFND9_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFND9_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFND9_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFND9_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFND9_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFND9_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND9_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFND9_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFND9_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFND9_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFND9_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFND9_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFND9_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND9_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND9_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFND9_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFND9_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFND9_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFND9_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFND9_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFND9_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFND9_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFND9_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFND9_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RNGFNDA Parameters

## RNGFNDA_TYPE: Rangefinder type

Type of connected rangefinder

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Analog|
|2|MaxbotixI2C|
|3|LidarLite-I2C|
|5|PWM|
|6|BBB-PRU|
|7|LightWareI2C|
|8|LightWareSerial|
|9|Bebop|
|10|MAVLink|
|11|USD1_Serial|
|12|LeddarOne|
|13|MaxbotixSerial|
|14|TeraRangerI2C|
|15|LidarLiteV3-I2C|
|16|VL53L0X or VL53L1X|
|17|NMEA|
|18|WASP-LRF|
|19|BenewakeTF02|
|20|Benewake-Serial|
|21|LidarLightV3HP|
|22|PWM|
|23|BlueRoboticsPing|
|24|DroneCAN|
|25|BenewakeTFminiPlus-I2C|
|26|LanbaoPSK-CM8JL65-CC5|
|27|BenewakeTF03|
|28|VL53L1X-ShortRange|
|29|LeddarVu8-Serial|
|30|HC-SR04|
|31|GYUS42v2|
|32|MSP|
|33|USD1_CAN|
|34|Benewake_CAN|
|35|TeraRangerSerial|
|36|Lua_Scripting|
|37|NoopLoop_TOFSense|
|38|NoopLoop_TOFSense_CAN|
|39|NRA24_CAN|
|40|NoopLoop_TOFSenseF_I2C|
|41|JRE_Serial|
|42|Ainstein_LR_D1|
|43|RDS02UF|
|44|HexsoonRadar|
|100|SITL|

## RNGFNDA_PIN: Rangefinder pin

Analog or PWM input pin that rangefinder is connected to. Analog RSSI or Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RNGFNDA_SCALING: Rangefinder scaling

Scaling factor between rangefinder reading and distance. For the linear and inverted functions this is in meters per volt. For the hyperbolic function the units are meterVolts. For Maxbotix serial sonar this is unit conversion to meters.

- Units: m/V

- Increment: 0.001

## RNGFNDA_OFFSET: rangefinder offset

Offset in volts for zero distance for analog rangefinders. Offset added to distance in centimeters for PWM lidars

- Units: V

- Increment: 0.001

## RNGFNDA_FUNCTION: Rangefinder function

Control over what function is used to calculate distance. For a linear function, the distance is (voltage-offset)*scaling. For a inverted function the distance is (offset-voltage)*scaling. For a hyperbolic function the distance is scaling/(voltage-offset). The functions return the distance in meters.

|Value|Meaning|
|:---:|:---:|
|0|Linear|
|1|Inverted|
|2|Hyperbolic|

## RNGFNDA_MIN_CM: Rangefinder minimum distance

Minimum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFNDA_MAX_CM: Rangefinder maximum distance

Maximum distance in centimeters that rangefinder can reliably read

- Units: cm

- Increment: 1

## RNGFNDA_STOP_PIN: Rangefinder stop pin

Digital pin that enables/disables rangefinder measurement for the pwm rangefinder. A value of -1 means no pin. If this is set, then the pin is set to 1 to enable the rangefinder and set to 0 to disable it. This is used to enable powersaving when out of range. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Not Used|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|111|PX4 FMU Relay1|
|112|PX4 FMU Relay2|
|113|PX4IO Relay1|
|114|PX4IO Relay2|
|115|PX4IO ACC1|
|116|PX4IO ACC2|

## RNGFNDA_RMETRIC: Ratiometric

This parameter sets whether an analog rangefinder is ratiometric. Most analog rangefinders are ratiometric, meaning that their output voltage is influenced by the supply voltage. Some analog rangefinders (such as the SF/02) have their own internal voltage regulators so they are not ratiometric.

|Value|Meaning|
|:---:|:---:|
|0|No|
|1|Yes|

## RNGFNDA_PWRRNG: Powersave range

This parameter sets the estimated terrain distance in meters above which the sensor will be put into a power saving mode (if available). A value of zero means power saving is not enabled

- Units: m

- Range: 0 32767

## RNGFNDA_GNDCLEAR: Distance (in cm) from the range finder to the ground

This parameter sets the expected range measurement(in cm) that the range finder should return when the vehicle is on the ground.

- Units: cm

- Range: 5 127

- Increment: 1

## RNGFNDA_ADDR: Bus address of sensor

This sets the bus address of the sensor, where applicable. Used for the I2C and DroneCAN sensors to allow for multiple sensors on different addresses.

- Range: 0 127

- Increment: 1

## RNGFNDA_POS_X:  X position offset

*Note: This parameter is for advanced users*

X position of the rangefinder in body frame. Positive X is forward of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFNDA_POS_Y: Y position offset

*Note: This parameter is for advanced users*

Y position of the rangefinder in body frame. Positive Y is to the right of the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFNDA_POS_Z: Z position offset

*Note: This parameter is for advanced users*

Z position of the rangefinder in body frame. Positive Z is down from the origin. Use the zero range datum point if supplied.

- Units: m

- Range: -5 5

- Increment: 0.01

## RNGFNDA_ORIENT: Rangefinder orientation

*Note: This parameter is for advanced users*

Orientation of rangefinder

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|1|Forward-Right|
|2|Right|
|3|Back-Right|
|4|Back|
|5|Back-Left|
|6|Left|
|7|Forward-Left|
|24|Up|
|25|Down|

## RNGFNDA_WSP_MAVG: Moving Average Range

*Note: This parameter is for advanced users*

Sets the number of historic range results to use for calculating the current range result. When MAVG is greater than 1, the current range result will be the current measured value averaged with the N-1 previous results

- Range: 0 255

## RNGFNDA_WSP_MEDF: Moving Median Filter

*Note: This parameter is for advanced users*

Sets the window size for the real-time median filter. When MEDF is greater than 0 the median filter is active

- Range: 0 255

## RNGFNDA_WSP_FRQ: Frequency

*Note: This parameter is for advanced users*

Sets the repetition frequency of the ranging operation in Hertz. Upon entering the desired frequency the system will calculate the nearest frequency that it can handle according to the resolution of internal timers.

- Range: 0 10000

## RNGFNDA_WSP_AVG: Multi-pulse averages

*Note: This parameter is for advanced users*

Sets the number of pulses to be used in multi-pulse averaging mode. In this mode, a sequence of rapid fire ranges are taken and then averaged to improve the accuracy of the measurement

- Range: 0 255

## RNGFNDA_WSP_THR: Sensitivity threshold

*Note: This parameter is for advanced users*

Sets the system sensitivity. Larger values of THR represent higher sensitivity. The system may limit the maximum value of THR to prevent excessive false alarm rates based on settings made at the factory. Set to -1 for automatic threshold adjustments

- Range: -1 255

## RNGFNDA_WSP_BAUD: Baud rate

*Note: This parameter is for advanced users*

Desired baud rate

|Value|Meaning|
|:---:|:---:|
|0|Low Speed|
|1|High Speed|

## RNGFNDA_RECV_ID: RangeFinder CAN receive ID

*Note: This parameter is for advanced users*

The receive ID of the CAN frames. A value of zero means all IDs are accepted.

- Range: 0 65535

## RNGFNDA_SNR_MIN: RangeFinder Minimum signal strength

*Note: This parameter is for advanced users*

RangeFinder Minimum signal strength (SNR) to accept distance

- Range: 0 65535

# RPM1 Parameters

## RPM1_TYPE: RPM type

What type of RPM sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Not Used|
|2|GPIO|
|3|EFI|
|4|Harmonic Notch|
|5|ESC Telemetry Motors Bitmask|
|6|Generator|
|7|DroneCAN|

## RPM1_SCALING: RPM scaling

Scaling factor between sensor reading and RPM.

- Increment: 0.001

## RPM1_MAX: Maximum RPM

Maximum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM1_MIN: Minimum RPM

Minimum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM1_MIN_QUAL: Minimum Quality

*Note: This parameter is for advanced users*

Minimum data quality to be used

- Increment: 0.1

## RPM1_PIN: Input pin number

Which digital GPIO pin to use. Only used on type = GPIO. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## RPM1_ESC_MASK: Bitmask of ESC telemetry channels to average

*Note: This parameter is for advanced users*

Mask of channels which support ESC rpm telemetry. RPM telemetry of the selected channels will be averaged

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16

## RPM1_ESC_INDEX: ESC Telemetry Index to write RPM to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write RPM to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## RPM1_DC_ID: DroneCAN Sensor ID

*Note: This parameter is for advanced users*

DroneCAN sensor ID to assign to this backend

- Range: -1 10

- Increment: 1

# RPM2 Parameters

## RPM2_TYPE: RPM type

What type of RPM sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Not Used|
|2|GPIO|
|3|EFI|
|4|Harmonic Notch|
|5|ESC Telemetry Motors Bitmask|
|6|Generator|
|7|DroneCAN|

## RPM2_SCALING: RPM scaling

Scaling factor between sensor reading and RPM.

- Increment: 0.001

## RPM2_MAX: Maximum RPM

Maximum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM2_MIN: Minimum RPM

Minimum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM2_MIN_QUAL: Minimum Quality

*Note: This parameter is for advanced users*

Minimum data quality to be used

- Increment: 0.1

## RPM2_PIN: Input pin number

Which digital GPIO pin to use. Only used on type = GPIO. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## RPM2_ESC_MASK: Bitmask of ESC telemetry channels to average

*Note: This parameter is for advanced users*

Mask of channels which support ESC rpm telemetry. RPM telemetry of the selected channels will be averaged

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16

## RPM2_ESC_INDEX: ESC Telemetry Index to write RPM to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write RPM to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## RPM2_DC_ID: DroneCAN Sensor ID

*Note: This parameter is for advanced users*

DroneCAN sensor ID to assign to this backend

- Range: -1 10

- Increment: 1

# RPM3 Parameters

## RPM3_TYPE: RPM type

What type of RPM sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Not Used|
|2|GPIO|
|3|EFI|
|4|Harmonic Notch|
|5|ESC Telemetry Motors Bitmask|
|6|Generator|
|7|DroneCAN|

## RPM3_SCALING: RPM scaling

Scaling factor between sensor reading and RPM.

- Increment: 0.001

## RPM3_MAX: Maximum RPM

Maximum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM3_MIN: Minimum RPM

Minimum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM3_MIN_QUAL: Minimum Quality

*Note: This parameter is for advanced users*

Minimum data quality to be used

- Increment: 0.1

## RPM3_PIN: Input pin number

Which digital GPIO pin to use. Only used on type = GPIO. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## RPM3_ESC_MASK: Bitmask of ESC telemetry channels to average

*Note: This parameter is for advanced users*

Mask of channels which support ESC rpm telemetry. RPM telemetry of the selected channels will be averaged

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16

## RPM3_ESC_INDEX: ESC Telemetry Index to write RPM to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write RPM to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## RPM3_DC_ID: DroneCAN Sensor ID

*Note: This parameter is for advanced users*

DroneCAN sensor ID to assign to this backend

- Range: -1 10

- Increment: 1

# RPM4 Parameters

## RPM4_TYPE: RPM type

What type of RPM sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Not Used|
|2|GPIO|
|3|EFI|
|4|Harmonic Notch|
|5|ESC Telemetry Motors Bitmask|
|6|Generator|
|7|DroneCAN|

## RPM4_SCALING: RPM scaling

Scaling factor between sensor reading and RPM.

- Increment: 0.001

## RPM4_MAX: Maximum RPM

Maximum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM4_MIN: Minimum RPM

Minimum RPM to report. Only used on type = GPIO.

- Increment: 1

## RPM4_MIN_QUAL: Minimum Quality

*Note: This parameter is for advanced users*

Minimum data quality to be used

- Increment: 0.1

## RPM4_PIN: Input pin number

Which digital GPIO pin to use. Only used on type = GPIO. Some common values are given, but see the Wiki's "GPIOs" page for how to determine the pin number for a given autopilot.

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## RPM4_ESC_MASK: Bitmask of ESC telemetry channels to average

*Note: This parameter is for advanced users*

Mask of channels which support ESC rpm telemetry. RPM telemetry of the selected channels will be averaged

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16

## RPM4_ESC_INDEX: ESC Telemetry Index to write RPM to

*Note: This parameter is for advanced users*

ESC Telemetry Index to write RPM to. Use 0 to disable.

- Range: 0 10

- Increment: 1

## RPM4_DC_ID: DroneCAN Sensor ID

*Note: This parameter is for advanced users*

DroneCAN sensor ID to assign to this backend

- Range: -1 10

- Increment: 1

# RSSI Parameters

## RSSI_TYPE: RSSI Type

Radio Receiver RSSI type. If your radio receiver supports RSSI of some kind, set it here, then set its associated RSSI_XXXXX parameters, if any.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|AnalogPin|
|2|RCChannelPwmValue|
|3|ReceiverProtocol|
|4|PWMInputPin|
|5|TelemetryRadioRSSI|

## RSSI_ANA_PIN: Receiver RSSI sensing pin

Pin used to read the RSSI voltage or PWM value. Analog Airspeed ports can be used for Analog inputs (some autopilots provide others also), Non-IOMCU Servo/MotorOutputs can be used for PWM input when configured as "GPIOs". Values for some autopilots are given as examples. Search wiki for "Analog pins" for analog pin or "GPIOs", if PWM input type, to determine pin number.

|Value|Meaning|
|:---:|:---:|
|8|V5 Nano|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## RSSI_PIN_LOW: RSSI pin's lowest voltage

RSSI pin's voltage received on the RSSI_ANA_PIN when the signal strength is the weakest. Some radio receivers put out inverted values so this value may be higher than RSSI_PIN_HIGH. When using pin 103, the maximum value of the parameter is 3.3V.

- Units: V

- Increment: 0.01

- Range: 0 5.0

## RSSI_PIN_HIGH: RSSI pin's highest voltage

RSSI pin's voltage received on the RSSI_ANA_PIN when the signal strength is the strongest. Some radio receivers put out inverted values so this value may be lower than RSSI_PIN_LOW. When using pin 103, the maximum value of the parameter is 3.3V.

- Units: V

- Increment: 0.01

- Range: 0 5.0

## RSSI_CHANNEL: Receiver RSSI channel number

The channel number where RSSI will be output by the radio receiver (5 and above).

- Range: 0 16

## RSSI_CHAN_LOW: RSSI PWM low value

PWM value that the radio receiver will put on the RSSI_CHANNEL or RSSI_ANA_PIN when the signal strength is the weakest. Some radio receivers output inverted values so this value may be lower than RSSI_CHAN_HIGH

- Units: PWM

- Range: 0 2000

## RSSI_CHAN_HIGH: Receiver RSSI PWM high value

PWM value that the radio receiver will put on the RSSI_CHANNEL or RSSI_ANA_PIN when the signal strength is the strongest. Some radio receivers output inverted values so this value may be higher than RSSI_CHAN_LOW

- Units: PWM

- Range: 0 2000

# SAIL Parameters

## SAIL_ENABLE: Enable Sailboat

This enables Sailboat functionality

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

- RebootRequired: True

## SAIL_ANGLE_MIN: Sail min angle

Mainsheet tight, angle between centerline and boom

- Units: deg

- Range: 0 90

- Increment: 1

## SAIL_ANGLE_MAX: Sail max angle

Mainsheet loose, angle between centerline and boom. For direct-control rotating masts, the rotation angle at SERVOx_MAX/_MIN; for rotating masts, this value can exceed 90 degrees if the linkages can physically rotate the mast past that angle.

- Units: deg

- Range: 0 90

- Increment: 1

## SAIL_ANGLE_IDEAL: Sail ideal angle

Ideal angle between sail and apparent wind

- Units: deg

- Range: 0 90

- Increment: 1

## SAIL_HEEL_MAX: Sailing maximum heel angle

When in auto sail trim modes the heel will be limited to this value using PID control

- Units: deg

- Range: 0 90

- Increment: 1

## SAIL_NO_GO_ANGLE: Sailing no go zone angle

The typical closest angle to the wind the vehicle will sail at. the vehicle will sail at this angle when going upwind

- Units: deg

- Range: 0 90

- Increment: 1

## SAIL_WNDSPD_MIN: Sailboat minimum wind speed to sail in

Sailboat minimum wind speed to continue sail in, at lower wind speeds the sailboat will motor if one is fitted

- Units: m/s

- Range: 0 5

- Increment: 0.1

## SAIL_XTRACK_MAX: Sailing vehicle max cross track error

The sail boat will tack when it reaches this cross track error, defines a corridor of 2 times this value wide, 0 disables

- Units: m

- Range: 5 25

- Increment: 1

## SAIL_LOIT_RADIUS: Loiter radius

When in sailing modes the vehicle will keep moving within this loiter radius

- Units: m

- Range: 0 20

- Increment: 1

# SCHED Parameters

## SCHED_DEBUG: Scheduler debug level

*Note: This parameter is for advanced users*

Set to non-zero to enable scheduler debug messages. When set to show "Slips" the scheduler will display a message whenever a scheduled task is delayed due to too much CPU load. When set to ShowOverruns the scheduled will display a message whenever a task takes longer than the limit promised in the task table.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|2|ShowSlips|
|3|ShowOverruns|

## SCHED_LOOP_RATE: Scheduling main loop rate

*Note: This parameter is for advanced users*

This controls the rate of the main control loop in Hz. This should only be changed by developers. This only takes effect on restart. Values over 400 are considered highly experimental.

- Range: 50 400

- RebootRequired: True

- Units: Hz

## SCHED_OPTIONS: Scheduling options

*Note: This parameter is for advanced users*

This controls optional aspects of the scheduler.

- Bitmask: 0:Enable per-task perf info

# SCR Parameters

## SCR_ENABLE: Enable Scripting

*Note: This parameter is for advanced users*

Controls if scripting is enabled

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Lua Scripts|

- RebootRequired: True

## SCR_VM_I_COUNT: Scripting Virtual Machine Instruction Count

*Note: This parameter is for advanced users*

The number virtual machine instructions that can be run before considering a script to have taken an excessive amount of time

- Range: 1000 1000000

- Increment: 10000

## SCR_HEAP_SIZE: Scripting Heap Size

*Note: This parameter is for advanced users*

Amount of memory available for scripting

- Range: 1024 1048576

- Increment: 1024

- RebootRequired: True

## SCR_DEBUG_OPTS: Scripting Debug Level

*Note: This parameter is for advanced users*

Debugging options

- Bitmask: 0: No Scripts to run message if all scripts have stopped, 1: Runtime messages for memory usage and execution time, 2: Suppress logging scripts to dataflash, 3: log runtime memory usage and execution time, 4: Disable pre-arm check, 5: Save CRC of current scripts to loaded and running checksum parameters enabling pre-arm, 6: Disable heap expansion on allocation failure

## SCR_USER1: Scripting User Parameter1

General purpose user variable input for scripts

## SCR_USER2: Scripting User Parameter2

General purpose user variable input for scripts

## SCR_USER3: Scripting User Parameter3

General purpose user variable input for scripts

## SCR_USER4: Scripting User Parameter4

General purpose user variable input for scripts

## SCR_USER5: Scripting User Parameter5

General purpose user variable input for scripts

## SCR_USER6: Scripting User Parameter6

General purpose user variable input for scripts

## SCR_DIR_DISABLE: Directory disable

*Note: This parameter is for advanced users*

This will stop scripts being loaded from the given locations

- Bitmask: 0:ROMFS, 1:APM/scripts

- RebootRequired: True

## SCR_LD_CHECKSUM: Loaded script checksum

*Note: This parameter is for advanced users*

Required XOR of CRC32 checksum of loaded scripts, vehicle will not arm with incorrect scripts loaded, -1 disables

## SCR_RUN_CHECKSUM: Running script checksum

*Note: This parameter is for advanced users*

Required XOR of CRC32 checksum of running scripts, vehicle will not arm with incorrect scripts running, -1 disables

## SCR_THD_PRIORITY: Scripting thread priority

*Note: This parameter is for advanced users*

This sets the priority of the scripting thread. This is normally set to a low priority to prevent scripts from interfering with other parts of the system. Advanced users can change this priority if scripting needs to be prioritised for realtime applications. WARNING: changing this parameter can impact the stability of your flight controller. The scipting thread priority in this parameter is chosen based on a set of system level priorities for other subsystems. It is strongly recommended that you use the lowest priority that is sufficient for your application. Note that all scripts run at the same priority, so if you raise this priority you must carefully audit all lua scripts for behaviour that does not interfere with the operation of the system.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|IO Priority|
|2|Storage Priority|
|3|UART Priority|
|4|I2C Priority|
|5|SPI Priority|
|6|Timer Priority|
|7|Main Priority|
|8|Boost Priority|

- RebootRequired: True

## SCR_SDEV_EN: Scripting serial device enable

*Note: This parameter is for advanced users*

Enable scripting serial devices

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## SCR_SDEV1_PROTO: Serial protocol of scripting serial device

*Note: This parameter is for advanced users*

Serial protocol of scripting serial device

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SCR_SDEV2_PROTO: Serial protocol of scripting serial device

*Note: This parameter is for advanced users*

Serial protocol of scripting serial device

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SCR_SDEV3_PROTO: Serial protocol of scripting serial device

*Note: This parameter is for advanced users*

Serial protocol of scripting serial device

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

# SERIAL Parameters

## SERIAL0_BAUD: Serial0 baud rate

The baud rate used on the USB console. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL0_PROTOCOL: Console protocol selection

Control what protocol to use on the console. 

|Value|Meaning|
|:---:|:---:|
|1|MAVLink1|
|2|MAVLink2|

- RebootRequired: True

## SERIAL1_PROTOCOL: Telem1 protocol selection

Control what protocol to use on the Telem1 port. Note that the Frsky options require external converter hardware. See the wiki for details.

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

- RebootRequired: True

## SERIAL1_BAUD: Telem1 Baud Rate

The baud rate used on the Telem1 port. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL2_PROTOCOL: Telemetry 2 protocol selection

Control what protocol to use on the Telem2 port. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL2_BAUD: Telemetry 2 Baud Rate

The baud rate of the Telem2 port. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL3_PROTOCOL: Serial 3 (GPS) protocol selection

Control what protocol Serial 3 (GPS) should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL3_BAUD: Serial 3 (GPS) Baud Rate

The baud rate used for the Serial 3 (GPS). Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL4_PROTOCOL: Serial4 protocol selection

Control what protocol Serial4 port should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL4_BAUD: Serial 4 Baud Rate

The baud rate used for Serial4. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL5_PROTOCOL: Serial5 protocol selection

Control what protocol Serial5 port should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL5_BAUD: Serial 5 Baud Rate

The baud rate used for Serial5. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL6_PROTOCOL: Serial6 protocol selection

Control what protocol Serial6 port should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL6_BAUD: Serial 6 Baud Rate

The baud rate used for Serial6. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL1_OPTIONS: Telem1 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL2_OPTIONS: Telem2 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL3_OPTIONS: Serial3 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL4_OPTIONS: Serial4 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL5_OPTIONS: Serial5 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL6_OPTIONS: Serial6 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL_PASS1: Serial passthru first port

*Note: This parameter is for advanced users*

This sets one side of pass-through between two serial ports. Once both sides are set then all data received on either port will be passed to the other port

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## SERIAL_PASS2: Serial passthru second port

*Note: This parameter is for advanced users*

This sets one side of pass-through between two serial ports. Once both sides are set then all data received on either port will be passed to the other port

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|0|Serial0|
|1|Serial1|
|2|Serial2|
|3|Serial3|
|4|Serial4|
|5|Serial5|
|6|Serial6|

## SERIAL_PASSTIMO: Serial passthru timeout

*Note: This parameter is for advanced users*

This sets a timeout for serial pass-through in seconds. When the pass-through is enabled by setting the SERIAL_PASS1 and SERIAL_PASS2 parameters then it remains in effect until no data comes from the first port for SERIAL_PASSTIMO seconds. This allows the port to revent to its normal usage (such as MAVLink connection to a GCS) when it is no longer needed. A value of 0 means no timeout.

- Range: 0 120

- Units: s

## SERIAL7_PROTOCOL: Serial7 protocol selection

Control what protocol Serial7 port should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL7_BAUD: Serial 7 Baud Rate

The baud rate used for Serial7. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL7_OPTIONS: Serial7 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL8_PROTOCOL: Serial8 protocol selection

Control what protocol Serial8 port should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL8_BAUD: Serial 8 Baud Rate

The baud rate used for Serial8. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL8_OPTIONS: Serial8 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

## SERIAL9_PROTOCOL: Serial9 protocol selection

Control what protocol Serial9 port should be used for. Note that the Frsky options require external converter hardware. See the wiki for details.

- RebootRequired: True

|Value|Meaning|
|:---:|:---:|
|-1|None|
|1|MAVLink1|
|2|MAVLink2|
|3|Frsky D|
|4|Frsky SPort|
|5|GPS|
|7|Alexmos Gimbal Serial|
|8|Gimbal|
|9|Rangefinder|
|10|FrSky SPort Passthrough (OpenTX)|
|11|Lidar360|
|13|Beacon|
|14|Volz servo out|
|15|SBus servo out|
|16|ESC Telemetry|
|17|Devo Telemetry|
|18|OpticalFlow|
|19|RobotisServo|
|20|NMEA Output|
|21|WindVane|
|22|SLCAN|
|23|RCIN|
|24|EFI Serial|
|25|LTM|
|26|RunCam|
|27|HottTelem|
|28|Scripting|
|29|Crossfire VTX|
|30|Generator|
|31|Winch|
|32|MSP|
|33|DJI FPV|
|34|AirSpeed|
|35|ADSB|
|36|AHRS|
|37|SmartAudio|
|38|FETtecOneWire|
|39|Torqeedo|
|40|AIS|
|41|CoDevESC|
|42|DisplayPort|
|43|MAVLink High Latency|
|44|IRC Tramp|
|45|DDS XRCE|
|46|IMUDATA|
|48|PPP|
|49|i-BUS Telemetry|

## SERIAL9_BAUD: Serial 9 Baud Rate

The baud rate used for Serial8. Most stm32-based boards can support rates of up to 1500. If you setup a rate you cannot support and then can't connect to your board you should load a firmware from a different vehicle type. That will reset all your parameters to defaults.

|Value|Meaning|
|:---:|:---:|
|1|1200|
|2|2400|
|4|4800|
|9|9600|
|19|19200|
|38|38400|
|57|57600|
|111|111100|
|115|115200|
|230|230400|
|256|256000|
|460|460800|
|500|500000|
|921|921600|
|1500|1.5MBaud|
|2000|2MBaud|
|12500000|12.5MBaud|

## SERIAL9_OPTIONS: Serial9 options

*Note: This parameter is for advanced users*

Control over UART options. The InvertRX option controls invert of the receive pin. The InvertTX option controls invert of the transmit pin. The HalfDuplex option controls half-duplex (onewire) mode, where both transmit and receive is done on the transmit wire. The Swap option allows the RX and TX pins to be swapped on STM32F7 based boards.

- Bitmask: 0:InvertRX, 1:InvertTX, 2:HalfDuplex, 3:SwapTXRX, 4: RX_PullDown, 5: RX_PullUp, 6: TX_PullDown, 7: TX_PullUp, 8: RX_NoDMA, 9: TX_NoDMA, 10: Don't forward mavlink to/from, 11: DisableFIFO, 12: Ignore Streamrate

- RebootRequired: True

# SERVO Parameters

## SERVO_RATE: Servo default output rate

*Note: This parameter is for advanced users*

Default output rate in Hz for all PWM outputs.

- Range: 25 400

- Units: Hz

## SERVO_DSHOT_RATE: Servo DShot output rate

*Note: This parameter is for advanced users*

DShot output rate for all outputs as a multiple of the loop rate. 0 sets the output rate to be fixed at 1Khz for low loop rates. This value should never be set below 500Hz.

|Value|Meaning|
|:---:|:---:|
|0|1Khz|
|1|loop-rate|
|2|double loop-rate|
|3|triple loop-rate|
|4|quadruple loop rate|

## SERVO_DSHOT_ESC: Servo DShot ESC type

*Note: This parameter is for advanced users*

DShot ESC type for all outputs. The ESC type affects the range of DShot commands available and the bit widths used. None means that no dshot commands will be executed. Some ESC types support Extended DShot Telemetry (EDT) which allows telemetry other than RPM data to be returned when using bi-directional dshot. If you enable EDT you must install EDT capable firmware for correct operation.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|BLHeli32/Kiss/AM32|
|2|BLHeli_S/BlueJay|
|3|BLHeli32/AM32/Kiss+EDT|
|4|BLHeli_S/BlueJay+EDT|

## SERVO_GPIO_MASK: Servo GPIO mask

*Note: This parameter is for advanced users*

Bitmask of outputs which will be available as GPIOs. Any output with either the function set to -1 or with the corresponding bit set in this mask will be available for use as a GPIO pin

- Bitmask: 0:Servo 1, 1:Servo 2, 2:Servo 3, 3:Servo 4, 4:Servo 5, 5:Servo 6, 6:Servo 7, 7:Servo 8, 8:Servo 9, 9:Servo 10, 10:Servo 11, 11:Servo 12, 12:Servo 13, 13:Servo 14, 14:Servo 15, 15:Servo 16, 16:Servo 17, 17:Servo 18, 18:Servo 19, 19:Servo 20, 20:Servo 21, 21:Servo 22, 22:Servo 23, 23:Servo 24, 24:Servo 25, 25:Servo 26, 26:Servo 27, 27:Servo 28, 28:Servo 29, 29:Servo 30, 30:Servo 31, 31:Servo 32

- RebootRequired: True

## SERVO_RC_FS_MSK: Servo RC Failsafe Mask

*Note: This parameter is for advanced users*

Bitmask of scaled passthru output channels which will be set to their trim value during rc failsafe instead of holding their last position before failsafe.

- Bitmask: 0:RCIN1Scaled, 1:RCIN2Scaled, 2:RCIN3Scaled, 3:RCIN4Scaled, 4:RCIN5Scaled, 5:RCIN6Scaled, 6:RCIN7Scaled, 7:RCIN8Scaled, 8:RCIN9Scaled, 9:RCIN10Scaled, 10:RCIN11Scaled, 11:SRCIN12Scaled, 12:RCIN13Scaled, 13:RCIN14Scaled, 14:RCIN15Scaled, 15:RCIN16Scaled

## SERVO_32_ENABLE: Enable outputs 17 to 31

*Note: This parameter is for advanced users*

This allows for up to 32 outputs, enabling parameters for outputs above 16

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

# SERVOn Parameters

## SERVOn_MIN: Minimum PWM

minimum PWM pulse width in microseconds. Typically 1000 is lower limit, 1500 is neutral and 2000 is upper limit.

- Units: PWM

- Range: 800 2200

- Increment: 1

## SERVOn_MAX: Maximum PWM

maximum PWM pulse width in microseconds. Typically 1000 is lower limit, 1500 is neutral and 2000 is upper limit.

- Units: PWM

- Range: 800 2200

- Increment: 1

## SERVOn_TRIM: Trim PWM

Trim PWM pulse width in microseconds. Typically 1000 is lower limit, 1500 is neutral and 2000 is upper limit.

- Units: PWM

- Range: 800 2200

- Increment: 1

## SERVOn_REVERSED: Servo reverse

Reverse servo operation. Set to 0 for normal operation. Set to 1 to reverse this output channel.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Reversed|

## SERVOn_FUNCTION: Servo output function

Function assigned to this servo. Setting this to Disabled(0) will setup this output for control by auto missions or MAVLink servo set commands. any other value will enable the corresponding function

|Value|Meaning|
|:---:|:---:|
|-1|GPIO|
|0|Disabled|
|1|RCPassThru|
|6|Mount1Yaw|
|7|Mount1Pitch|
|8|Mount1Roll|
|9|Mount1Retract|
|10|CameraTrigger|
|12|Mount2Yaw|
|13|Mount2Pitch|
|14|Mount2Roll|
|15|Mount2Retract|
|22|SprayerPump|
|23|SprayerSpinner|
|26|GroundSteering|
|28|Gripper|
|33|Motor1|
|34|Motor2|
|35|Motor3|
|36|Motor4|
|51|RCIN1|
|52|RCIN2|
|53|RCIN3|
|54|RCIN4|
|55|RCIN5|
|56|RCIN6|
|57|RCIN7|
|58|RCIN8|
|59|RCIN9|
|60|RCIN10|
|61|RCIN11|
|62|RCIN12|
|63|RCIN13|
|64|RCIN14|
|65|RCIN15|
|66|RCIN16|
|70|Throttle|
|73|ThrottleLeft|
|74|ThrottleRight|
|88|Winch|
|89|Main Sail|
|90|CameraISO|
|91|CameraAperture|
|92|CameraFocus|
|93|CameraShutterSpeed|
|94|Script1|
|95|Script2|
|96|Script3|
|97|Script4|
|98|Script5|
|99|Script6|
|100|Script7|
|101|Script8|
|102|Script9|
|103|Script10|
|104|Script11|
|105|Script12|
|106|Script13|
|107|Script14|
|108|Script15|
|109|Script16|
|120|NeoPixel1|
|121|NeoPixel2|
|122|NeoPixel3|
|123|NeoPixel4|
|128|WingSailElevator|
|129|ProfiLED1|
|130|ProfiLED2|
|131|ProfiLED3|
|132|ProfiLEDClock|
|133|Winch Clutch|
|134|SERVOn_MIN|
|135|SERVOn_TRIM|
|136|SERVOn_MAX|
|137|SailMastRotation|
|138|Alarm|
|139|Alarm Inverted|
|140|RCIN1Scaled|
|141|RCIN2Scaled|
|142|RCIN3Scaled|
|143|RCIN4Scaled|
|144|RCIN5Scaled|
|145|RCIN6Scaled|
|146|RCIN7Scaled|
|147|RCIN8Scaled|
|148|RCIN9Scaled|
|149|RCIN10Scaled|
|150|RCIN11Scaled|
|151|RCIN12Scaled|
|152|RCIN13Scaled|
|153|RCIN14Scaled|
|154|RCIN15Scaled|
|155|RCIN16Scaled|

- RebootRequired: True

# SERVOBLH Parameters

## SERVO_BLH_MASK: BLHeli Channel Bitmask

*Note: This parameter is for advanced users*

Enable of BLHeli pass-thru servo protocol support to specific channels. This mask is in addition to motors enabled using SERVO_BLH_AUTO (if any)

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16, 16:Channel 17, 17: Channel 18, 18: Channel 19, 19: Channel 20, 20: Channel 21, 21: Channel 22, 22: Channel 23, 23: Channel 24, 24: Channel 25, 25: Channel 26, 26: Channel 27, 27: Channel 28, 28: Channel 29, 29: Channel 30, 30: Channel 31, 31: Channel 32

- RebootRequired: True

## SERVO_BLH_AUTO: BLHeli pass-thru auto-enable for multicopter motors

If set to 1 this auto-enables BLHeli pass-thru support for all multicopter motors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

- RebootRequired: True

## SERVO_BLH_TEST: BLHeli internal interface test

*Note: This parameter is for advanced users*

Setting SERVO_BLH_TEST to a motor number enables an internal test of the BLHeli ESC protocol to the corresponding ESC. The debug output is displayed on the USB console.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TestMotor1|
|2|TestMotor2|
|3|TestMotor3|
|4|TestMotor4|
|5|TestMotor5|
|6|TestMotor6|
|7|TestMotor7|
|8|TestMotor8|

## SERVO_BLH_TMOUT: BLHeli protocol timeout

This sets the inactivity timeout for the BLHeli protocol in seconds. If no packets are received in this time normal MAVLink operations are resumed. A value of 0 means no timeout

- Units: s

- Range: 0 300

## SERVO_BLH_TRATE: BLHeli telemetry rate

This sets the rate in Hz for requesting telemetry from ESCs. It is the rate per ESC. Setting to zero disables telemetry requests

- Units: Hz

- Range: 0 500

## SERVO_BLH_DEBUG: BLHeli debug level

When set to 1 this enabled verbose debugging output over MAVLink when the blheli protocol is active. This can be used to diagnose failures.

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SERVO_BLH_OTYPE: BLHeli output type override

*Note: This parameter is for advanced users*

When set to a non-zero value this overrides the output type for the output channels given by SERVO_BLH_MASK. This can be used to enable DShot on outputs that are not part of the multicopter motors group.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|OneShot|
|2|OneShot125|
|3|Brushed|
|4|DShot150|
|5|DShot300|
|6|DShot600|
|7|DShot1200|

- RebootRequired: True

## SERVO_BLH_PORT: Control port

*Note: This parameter is for advanced users*

This sets the mavlink channel to use for blheli pass-thru. The channel number is determined by the number of serial ports configured to use mavlink. So 0 is always the console, 1 is the next serial port using mavlink, 2 the next after that and so on.

|Value|Meaning|
|:---:|:---:|
|0|Console|
|1|Mavlink Serial Channel1|
|2|Mavlink Serial Channel2|
|3|Mavlink Serial Channel3|
|4|Mavlink Serial Channel4|
|5|Mavlink Serial Channel5|

## SERVO_BLH_POLES: BLHeli Motor Poles

*Note: This parameter is for advanced users*

This allows calculation of true RPM from ESC's eRPM. The default is 14.

- Range: 1 127

- RebootRequired: True

## SERVO_BLH_3DMASK: BLHeli bitmask of 3D channels

*Note: This parameter is for advanced users*

Mask of channels which are dynamically reversible. This is used to configure ESCs in '3D' mode, allowing for the motor to spin in either direction. Do not use for channels selected with SERVO_BLH_RVMASK.

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16, 16:Channel 17, 17: Channel 18, 18: Channel 19, 19: Channel 20, 20: Channel 21, 21: Channel 22, 22: Channel 23, 23: Channel 24, 24: Channel 25, 25: Channel 26, 26: Channel 27, 27: Channel 28, 28: Channel 29, 29: Channel 30, 30: Channel 31, 31: Channel 32

- RebootRequired: True

## SERVO_BLH_BDMASK: BLHeli bitmask of bi-directional dshot channels

*Note: This parameter is for advanced users*

Mask of channels which support bi-directional dshot telemetry. This is used for ESCs which have firmware that supports bi-directional dshot allowing fast rpm telemetry values to be returned for the harmonic notch.

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16, 16:Channel 17, 17: Channel 18, 18: Channel 19, 19: Channel 20, 20: Channel 21, 21: Channel 22, 22: Channel 23, 23: Channel 24, 24: Channel 25, 25: Channel 26, 26: Channel 27, 27: Channel 28, 28: Channel 29, 29: Channel 30, 30: Channel 31, 31: Channel 32

- RebootRequired: True

## SERVO_BLH_RVMASK: BLHeli bitmask of reversed channels

*Note: This parameter is for advanced users*

Mask of channels which are reversed. This is used to configure ESCs to reverse motor direction for unidirectional rotation. Do not use for channels selected with SERVO_BLH_3DMASK.

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16, 16:Channel 17, 17: Channel 18, 18: Channel 19, 19: Channel 20, 20: Channel 21, 21: Channel 22, 22: Channel 23, 23: Channel 24, 24: Channel 25, 25: Channel 26, 26: Channel 27, 27: Channel 28, 28: Channel 29, 29: Channel 30, 30: Channel 31, 31: Channel 32

- RebootRequired: True

# SERVOFTW Parameters

## SERVO_FTW_MASK: Servo channel output bitmask

Servo channel mask specifying FETtec ESC output.

- Bitmask: 0:SERVO1,1:SERVO2,2:SERVO3,3:SERVO4,4:SERVO5,5:SERVO6,6:SERVO7,7:SERVO8,8:SERVO9,9:SERVO10,10:SERVO11,11:SERVO12

- RebootRequired: True

## SERVO_FTW_RVMASK: Servo channel reverse rotation bitmask

Servo channel mask to reverse rotation of FETtec ESC outputs.

- Bitmask: 0:SERVO1,1:SERVO2,2:SERVO3,3:SERVO4,4:SERVO5,5:SERVO6,6:SERVO7,7:SERVO8,8:SERVO9,9:SERVO10,10:SERVO11,11:SERVO12

## SERVO_FTW_POLES: Nr. electrical poles

Number of motor electrical poles

- Range: 2 50

# SERVOROB Parameters

## SERVO_ROB_POSMIN: Robotis servo position min

Position minimum at servo min value. This should be within the position control range of the servos, normally 0 to 4095

- Range: 0 4095

## SERVO_ROB_POSMAX: Robotis servo position max

Position maximum at servo max value. This should be within the position control range of the servos, normally 0 to 4095

- Range: 0 4095

# SERVOSBUS Parameters

## SERVO_SBUS_RATE: SBUS default output rate

*Note: This parameter is for advanced users*

This sets the SBUS output frame rate in Hz.

- Range: 25 250

- Units: Hz

# SERVOVOLZ Parameters

## SERVO_VOLZ_MASK: Channel Bitmask

Enable of volz servo protocol to specific channels

- Bitmask: 0:Channel1,1:Channel2,2:Channel3,3:Channel4,4:Channel5,5:Channel6,6:Channel7,7:Channel8,8:Channel9,9:Channel10,10:Channel11,11:Channel12,12:Channel13,13:Channel14,14:Channel15,15:Channel16,16:Channel17,17:Channel18,18:Channel19,19:Channel20,20:Channel21,21:Channel22,22:Channel23,23:Channel24,24:Channel25,25:Channel26,26:Channel27,28:Channel29,29:Channel30,30:Channel31,31:Channel32

## SERVO_VOLZ_RANGE: Range of travel

Range to map between 1000 and 2000 PWM. Default value of 200 gives full +-100 deg range of extended position command. This results in 0.2 deg movement per US change in PWM. If the full range is not needed it can be reduced to increase resolution. 40 deg range gives 0.04 deg movement per US change in PWM, this is higher resolution than possible with the VOLZ protocol so further reduction in range will not improve resolution. Reduced range does allow PWMs outside the 1000 to 2000 range, with 40 deg range 750 PWM results in a angle of -30 deg, 2250 would be +30 deg. This is still limited by the 200 deg maximum range of the actuator.

- Units: deg

# SIM Parameters

## SIM_DRIFT_SPEED: Gyro drift speed

Gyro drift rate of change in degrees/second/minute

## SIM_DRIFT_TIME: Gyro drift time

Gyro drift duration of one full drift cycle (period in minutes)

## SIM_ENGINE_MUL: Engine failure thrust scaler

Thrust from Motors in SIM_ENGINE_FAIL will be multiplied by this factor

- Units: ms

## SIM_WIND_SPD: Simulated Wind speed

*Note: This parameter is for advanced users*

Allows you to emulate wind in sim

- Units: m/s

## SIM_WIND_DIR: Direction simulated wind is coming from

*Note: This parameter is for advanced users*

Allows you to set wind direction (true deg) in sim

- Units: deg

## SIM_WIND_TURB: Simulated Wind variation

*Note: This parameter is for advanced users*

Allows you to emulate random wind variations in sim

- Units: m/s

## SIM_WIND_TC: Wind variation time constant

*Note: This parameter is for advanced users*

this controls the time over which wind changes take effect

- Units: s

## SIM_SONAR_ROT: Sonar rotation

Sonar rotation from rotations enumeration

## SIM_BATT_VOLTAGE: Simulated battery voltage

*Note: This parameter is for advanced users*

Simulated battery (constant) voltage

- Units: V

## SIM_BATT_CAP_AH: Simulated battery capacity

*Note: This parameter is for advanced users*

Simulated battery capacity

- Units: Ah

## SIM_SONAR_GLITCH: Sonar glitch probablility

*Note: This parameter is for advanced users*

Probablility a sonar glitch would happen

- Range: 0 1

## SIM_SONAR_RND: Sonar noise factor

*Note: This parameter is for advanced users*

Scaling factor for simulated sonar noise

## SIM_RC_FAIL: Simulated RC signal failure

*Note: This parameter is for advanced users*

Allows you to emulate rc failures in sim

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|No RC pusles|
|2|All Channels neutral except Throttle is 950us|

## SIM_FLOAT_EXCEPT: Generate floating point exceptions

*Note: This parameter is for advanced users*

If set, if a numerical error occurs SITL will die with a floating point exception.

## SIM_CAN_SRV_MSK: Mask of CAN servos/ESCs

*Note: This parameter is for advanced users*

The set of actuators controlled externally by CAN SITL AP_Periph

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8, 8: Servo 9, 9: Servo 10, 10: Servo 11, 11: Servo 12, 12: Servo 13, 13: Servo 14, 14: Servo 15, 15: Servo 16, 16: Servo 17, 17: Servo 18, 18: Servo 19, 19: Servo 20, 20: Servo 21, 21: Servo 22, 22: Servo 23, 23: Servo 24, 24: Servo 25, 25: Servo 26, 26: Servo 27, 27: Servo 28, 28: Servo 29, 29: Servo 30, 30: Servo 31, 31: Servo 32

## SIM_CAN_TYPE1: transport type for first CAN interface

*Note: This parameter is for advanced users*

transport type for first CAN interface

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MulticastUDP|
|2|SocketCAN|

## SIM_CAN_TYPE2: transport type for second CAN interface

*Note: This parameter is for advanced users*

transport type for second CAN interface

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MulticastUDP|
|2|SocketCAN|

## SIM_SONAR_SCALE: Sonar conversion scale

Sonar conversion scale from distance to voltage

- Units: m/V

## SIM_FLOW_ENABLE: Opflow Enable

Enable simulated Optical Flow sensor

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enabled|

## SIM_TERRAIN: Terrain Enable

Enable using terrain for height

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enabled|

## SIM_FLOW_RATE: Opflow Rate

Opflow Data Rate

- Units: Hz

## SIM_FLOW_DELAY: Opflow Delay

Opflow data delay

- Units: ms

## SIM_ADSB_COUNT: Number of ADSB aircrafts

Total number of ADSB simulated aircraft

## SIM_ADSB_RADIUS: ADSB radius stddev of another aircraft

Simulated standard deviation of radius in ADSB of another aircraft

- Units: m

## SIM_ADSB_ALT: ADSB altitude of another aircraft

Simulated ADSB altitude of another aircraft

- Units: m

## SIM_PIN_MASK: GPIO emulation

SITL GPIO emulation

## SIM_ADSB_TX: ADSB transmit enable

ADSB transceiever enable and disable

|Value|Meaning|
|:---:|:---:|
|0|Transceiever disable|
|1|Transceiever enable|

## SIM_SPEEDUP: Sim Speedup

Runs the simulation at multiples of normal speed. Do not use if realtime physics, like RealFlight, is being used

- Range: 1 10

## SIM_IMU_POS_X: IMU Offsets

XYZ position of the IMU accelerometer relative to the body frame origin (X-axis)

- Units: m

## SIM_IMU_POS_Y: IMU Offsets

XYZ position of the IMU accelerometer relative to the body frame origin (Y-axis)

- Units: m

## SIM_IMU_POS_Z: IMU Offsets

XYZ position of the IMU accelerometer relative to the body frame origin (Z-axis)

- Units: m

## SIM_FLOW_POS_X: Opflow Pos

XYZ position of the optical flow sensor focal point relative to the body frame origin (X-axis)

- Units: m

## SIM_FLOW_POS_Y: Opflow Pos

XYZ position of the optical flow sensor focal point relative to the body frame origin (Y-axis)

- Units: m

## SIM_FLOW_POS_Z: Opflow Pos

XYZ position of the optical flow sensor focal point relative to the body frame origin (Z-axis)

- Units: m

## SIM_ENGINE_FAIL: Engine Fail Mask

mask of motors which SIM_ENGINE_MUL will be applied to

- Bitmask: 0: Servo 1, 1: Servo 2, 2: Servo 3, 3: Servo 4, 4: Servo 5, 5: Servo 6, 6: Servo 7, 7: Servo 8

## SIM_TEMP_START: Start temperature

*Note: This parameter is for advanced users*

Baro start temperature

- Units: degC

## SIM_TEMP_BRD_OFF: Baro temperature offset

*Note: This parameter is for advanced users*

Barometer board temperature offset from atmospheric temperature

- Units: degC

## SIM_TEMP_TCONST: Warmup time constant

*Note: This parameter is for advanced users*

Barometer warmup temperature time constant

- Units: degC

## SIM_TEMP_BFACTOR: Baro temperature factor

*Note: This parameter is for advanced users*

A pressure change with temperature that closely matches what has been observed with a ICM-20789

## SIM_WIND_DIR_Z: Simulated wind vertical direction

*Note: This parameter is for advanced users*

Allows you to set vertical wind direction (true deg) in sim. 0 means pure horizontal wind. 90 means pure updraft.

- Units: deg

## SIM_WIND_T: Wind Profile Type

Selects how wind varies from surface to WIND_T_ALT

|Value|Meaning|
|:---:|:---:|
|0|square law|
|1|none|
|2|linear-see WIND_T_COEF|

## SIM_WIND_T_ALT: Full Wind Altitude

*Note: This parameter is for advanced users*

Altitude at which wind reaches full strength, decaying from full strength as altitude lowers to ground level

- Units: m

## SIM_WIND_T_COEF: Linear Wind Curve Coeff

*Note: This parameter is for advanced users*

For linear wind profile,wind is reduced by (Altitude-WIND_T_ALT) x this value

## SIM_RC_CHANCOUNT: RC channel count

SITL RC channel count

## SIM_WOW_PIN: Weight on Wheels Pin

*Note: This parameter is for advanced users*

SITL set this simulated pin to true if vehicle is on ground

## SIM_BAUDLIMIT_EN: Telemetry bandwidth limitting

SITL enable bandwidth limitting on telemetry ports with non-zero values

## SIM_SHOVE_X: Acceleration of shove x

Acceleration of shove to vehicle in x axis

- Units: m/s/s

## SIM_SHOVE_Y: Acceleration of shove y

Acceleration of shove to vehicle in y axis

- Units: m/s/s

## SIM_SHOVE_Z: Acceleration of shove z

Acceleration of shove to vehicle in z axis

- Units: m/s/s

## SIM_SHOVE_TIME: Time length for shove

Force to the vehicle over a period of time

- Units: ms

## SIM_FLOW_RND: Opflow noise

Optical Flow sensor measurement noise

- Units: rad/s

## SIM_TWIST_X: Twist x

Rotational acceleration of twist x axis

- Units: rad/s/s

## SIM_TWIST_Y: Twist y

Rotational acceleration of twist y axis

- Units: rad/s/s

## SIM_TWIST_Z: Twist z

Rotational acceleration of twist z axis

- Units: rad/s/s

## SIM_TWIST_TIME: Twist time

Time that twist is applied on the vehicle

- Units: ms

## SIM_GND_BEHAV: Ground behavior

Ground behavior of aircraft (tailsitter, no movement, forward only)

## SIM_IMU_ORIENT: IMU orientation

*Note: This parameter is for advanced users*

Simulated orientation of the IMUs

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Yaw45|
|2|Yaw90|
|3|Yaw135|
|4|Yaw180|
|5|Yaw225|
|6|Yaw270|
|7|Yaw315|
|8|Roll180|
|9|Yaw45Roll180|
|10|Yaw90Roll180|
|11|Yaw135Roll180|
|12|Pitch180|
|13|Yaw225Roll180|
|14|Yaw270Roll180|
|15|Yaw315Roll180|
|16|Roll90|
|17|Yaw45Roll90|
|18|Yaw90Roll90|
|19|Yaw135Roll90|
|20|Roll270|
|21|Yaw45Roll270|
|22|Yaw90Roll270|
|23|Yaw135Roll270|
|24|Pitch90|
|25|Pitch270|
|26|Yaw90Pitch180|
|27|Yaw270Pitch180|
|28|Pitch90Roll90|
|29|Pitch90Roll180|
|30|Pitch90Roll270|
|31|Pitch180Roll90|
|32|Pitch180Roll270|
|33|Pitch270Roll90|
|34|Pitch270Roll180|
|35|Pitch270Roll270|
|36|Yaw90Pitch180Roll90|
|37|Yaw270Roll90|
|38|Yaw293Pitch68Roll180|
|39|Pitch315|
|40|Pitch315Roll90|
|42|Roll45|
|43|Roll315|
|100|Custom 4.1 and older|
|101|Custom 1|
|102|Custom 2|

## SIM_WAVE_ENABLE: Wave enable

Wave enable and modes

|Value|Meaning|
|:---:|:---:|
|0|disabled|
|1|roll and pitch|
|2|roll and pitch and heave|

## SIM_WAVE_LENGTH: Wave length

Wave length in SITL

- Units: m

## SIM_WAVE_AMP: Wave amplitude

Wave amplitude in SITL

- Units: m

## SIM_WAVE_DIR: Wave direction

Direction wave is coming from

- Units: deg

## SIM_WAVE_SPEED: Wave speed

Wave speed in SITL

- Units: m/s

## SIM_TIDE_DIR: Tide direction

Tide direction wave is coming from

- Units: deg

## SIM_TIDE_SPEED: Tide speed

Tide speed in simulation

- Units: m/s

## SIM_OPOS_LAT: Original Position (Latitude)

*Note: This parameter is for advanced users*

Specifies vehicle's startup latitude

## SIM_OPOS_LNG: Original Position (Longitude)

*Note: This parameter is for advanced users*

Specifies vehicle's startup longitude

## SIM_OPOS_ALT: Original Position (Altitude)

*Note: This parameter is for advanced users*

Specifies vehicle's startup altitude (AMSL)

## SIM_OPOS_HDG: Original Position (Heading)

*Note: This parameter is for advanced users*

Specifies vehicle's startup heading (0-360)

## SIM_LOOP_DELAY: Extra delay per main loop

Extra time delay per main loop

- Units: us

## SIM_EFI_TYPE: Type of Electronic Fuel Injection

Different types of Electronic Fuel Injection (EFI) systems

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MegaSquirt EFI system|
|2|Löweheiser EFI system|
|8|Hirth engines|

## SIM_VIB_MOT_HMNC: Motor harmonics

Motor harmonics generated in SITL

## SIM_VIB_MOT_MASK: Motor mask

Motor mask, allowing external simulators to mark motors

## SIM_VIB_MOT_MAX: Max motor vibration frequency

Max frequency to use as baseline for adding motor noise for the gyros and accels

- Units: Hz

## SIM_INS_THR_MIN: Minimum throttle INS noise

Minimum throttle for simulated ins noise

## SIM_VIB_MOT_MULT: Vibration motor scale

Amplitude scaling of motor noise relative to gyro/accel noise

## SIM_ODOM_ENABLE: Odometry enable

SITL odometry enabl

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## SIM_LED_LAYOUT: LED layout

LED layout config value

## SIM_THML_SCENARI: Thermal scenarios

Scenario for thermalling simulation, for soaring

## SIM_VICON_POS_X: SITL vicon position on vehicle in Forward direction

*Note: This parameter is for advanced users*

SITL vicon position on vehicle in Forward direction

- Units: m

- Range: 0 10

## SIM_VICON_POS_Y: SITL vicon position on vehicle in Right direction

*Note: This parameter is for advanced users*

SITL vicon position on vehicle in Right direction

- Units: m

- Range: 0 10

## SIM_VICON_POS_Z: SITL vicon position on vehicle in Down direction

SITL vicon position on vehicle in Down direction

- Units: m

- Range: 0 10

## SIM_VICON_GLIT_X: SITL vicon position glitch North

*Note: This parameter is for advanced users*

SITL vicon position glitch North

- Units: m

## SIM_VICON_GLIT_Y: SITL vicon position glitch East

*Note: This parameter is for advanced users*

SITL vicon position glitch East

- Units: m

## SIM_VICON_GLIT_Z: SITL vicon position glitch Down

*Note: This parameter is for advanced users*

SITL vicon position glitch Down

- Units: m

## SIM_VICON_FAIL: SITL vicon failure

*Note: This parameter is for advanced users*

SITL vicon failure

|Value|Meaning|
|:---:|:---:|
|0|Vicon Healthy|
|1|Vicon Failed|

## SIM_VICON_YAW: SITL vicon yaw angle in earth frame

*Note: This parameter is for advanced users*

SITL vicon yaw angle in earth frame

- Units: deg

- Range: 0 360

## SIM_VICON_YAWERR: SITL vicon yaw error

*Note: This parameter is for advanced users*

SITL vicon yaw added to reported yaw sent to vehicle

- Units: deg

- Range: -180 180

## SIM_VICON_TMASK: SITL vicon type mask

*Note: This parameter is for advanced users*

SITL vicon messages sent

- Bitmask: 0:VISION_POSITION_ESTIMATE, 1:VISION_SPEED_ESTIMATE, 2:VICON_POSITION_ESTIMATE, 3:VISION_POSITION_DELTA, 4:ODOMETRY

## SIM_VICON_VGLI_X: SITL vicon velocity glitch North

*Note: This parameter is for advanced users*

SITL vicon velocity glitch North

- Units: m/s

## SIM_VICON_VGLI_Y: SITL vicon velocity glitch East

*Note: This parameter is for advanced users*

SITL vicon velocity glitch East

- Units: m/s

## SIM_VICON_VGLI_Z: SITL vicon velocity glitch Down

*Note: This parameter is for advanced users*

SITL vicon velocity glitch Down

- Units: m/s

## SIM_RATE_HZ: Loop rate

SITL Loop rate

- Units: Hz

## SIM_IMU_COUNT: IMU count

Number of simulated IMUs to create

## SIM_BARO_COUNT: Baro count

Number of simulated baros to create in SITL

- Range: 0 3

## SIM_TIME_JITTER: Loop time jitter

*Note: This parameter is for advanced users*

Upper limit of random jitter in loop time

- Units: us

## SIM_ESC_TELEM: Simulated ESC Telemetry

*Note: This parameter is for advanced users*

enable perfect simulated ESC telemetry

## SIM_ESC_ARM_RPM: ESC RPM when armed

*Note: This parameter is for advanced users*

Simulated RPM when motors are armed

## SIM_UART_LOSS: UART byte loss percentage

*Note: This parameter is for advanced users*

Sets percentage of outgoing byte loss on UARTs

- Units: %

## SIM_ADSB_TYPES: Simulated ADSB Type mask

*Note: This parameter is for advanced users*

specifies which simulated ADSB types are active

- Bitmask: 0:MAVLink,3:SageTechMXS

## SIM_OSD_COLUMNS: Simulated OSD number of text columns

Simulated OSD number of text columns

- Range: 10 100

## SIM_OSD_ROWS: Simulated OSD number of text rows

Simulated OSD number of text rows

- Range: 10 100

## SIM_GPS_DISABLE: GPS 1 disable

*Note: This parameter is for advanced users*

Disables GPS 1

|Value|Meaning|
|:---:|:---:|
|0|Enable|
|1|GPS Disabled|

## SIM_GPS_LAG_MS: GPS 1 Lag

*Note: This parameter is for advanced users*

GPS 1 lag

- Units: ms

## SIM_GPS_TYPE: GPS 1 type

*Note: This parameter is for advanced users*

Sets the type of simulation used for GPS 1

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|UBlox|
|5|NMEA|
|6|SBP|
|7|File|
|8|Nova|
|9|SBP2|
|11|Trimble|
|19|MSP|

## SIM_GPS_BYTELOSS: GPS Byteloss

*Note: This parameter is for advanced users*

Percent of bytes lost from GPS 1

- Units: %

## SIM_GPS_NUMSATS: GPS 1 Num Satellites

Number of satellites GPS 1 has in view

## SIM_GPS_GLITCH_X: GPS 1 Glitch

*Note: This parameter is for advanced users*

Glitch offsets of simulated GPS 1 sensor (X-axis)

## SIM_GPS_GLITCH_Y: GPS 1 Glitch

*Note: This parameter is for advanced users*

Glitch offsets of simulated GPS 1 sensor (Y-axis)

## SIM_GPS_GLITCH_Z: GPS 1 Glitch

*Note: This parameter is for advanced users*

Glitch offsets of simulated GPS 1 sensor (Z-axis)

## SIM_GPS_HZ: GPS 1 Hz

GPS 1 Update rate

- Units: Hz

## SIM_GPS_DRIFTALT: GPS 1 Altitude Drift

*Note: This parameter is for advanced users*

GPS 1 altitude drift error

- Units: m

## SIM_GPS_POS_X: GPS 1 Position

GPS 1 antenna phase center position relative to the body frame origin (X-axis)

- Units: m

## SIM_GPS_POS_Y: GPS 1 Position

GPS 1 antenna phase center position relative to the body frame origin (Y-axis)

- Units: m

## SIM_GPS_POS_Z: GPS 1 Position

GPS 1 antenna phase center position relative to the body frame origin (Z-axis)

- Units: m

## SIM_GPS_NOISE: GPS 1 Noise

*Note: This parameter is for advanced users*

Amplitude of the GPS1 altitude error

- Units: m

## SIM_GPS_LOCKTIME: GPS 1 Lock Time

*Note: This parameter is for advanced users*

Delay in seconds before GPS1 acquires lock

- Units: s

## SIM_GPS_ALT_OFS: GPS 1 Altitude Offset

GPS 1 Altitude Error

- Units: m

## SIM_GPS_HDG: GPS 1 Heading

*Note: This parameter is for advanced users*

Enable GPS1 output of NMEA heading HDT sentence or UBLOX_RELPOSNED

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_GPS_ACC: GPS 1 Accuracy

*Note: This parameter is for advanced users*

GPS 1 Accuracy

## SIM_GPS_VERR_X: GPS 1 Velocity Error

*Note: This parameter is for advanced users*

GPS 1 Velocity Error Offsets in NED (X-axis)

## SIM_GPS_VERR_Y: GPS 1 Velocity Error

*Note: This parameter is for advanced users*

GPS 1 Velocity Error Offsets in NED (Y-axis)

## SIM_GPS_VERR_Z: GPS 1 Velocity Error

*Note: This parameter is for advanced users*

GPS 1 Velocity Error Offsets in NED (Z-axis)

## SIM_GPS_JAM: GPS jamming enable

*Note: This parameter is for advanced users*

Enable simulated GPS jamming

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_GPS2_DISABLE: GPS 2 disable

*Note: This parameter is for advanced users*

Disables GPS 2

|Value|Meaning|
|:---:|:---:|
|0|Enable|
|1|GPS Disabled|

## SIM_GPS2_LAG_MS: GPS 2 Lag

*Note: This parameter is for advanced users*

GPS 2 lag in ms

- Units: ms

## SIM_GPS2_TYPE: GPS 2 type

*Note: This parameter is for advanced users*

Sets the type of simulation used for GPS 2

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|UBlox|
|5|NMEA|
|6|SBP|
|7|File|
|8|Nova|
|9|SBP2|
|11|Trimble|
|19|MSP|

## SIM_GPS2_BYTELOS: GPS 2 Byteloss

*Note: This parameter is for advanced users*

Percent of bytes lost from GPS 2

- Units: %

## SIM_GPS2_NUMSATS: GPS 2 Num Satellites

Number of satellites GPS 2 has in view

## SIM_GPS2_GLTCH_X: GPS 2 Glitch

*Note: This parameter is for advanced users*

Glitch offsets of simulated GPS 2 sensor (X-axis)

## SIM_GPS2_GLTCH_Y: GPS 2 Glitch

*Note: This parameter is for advanced users*

Glitch offsets of simulated GPS 2 sensor (Y-axis)

## SIM_GPS2_GLTCH_Z: GPS 2 Glitch

*Note: This parameter is for advanced users*

Glitch offsets of simulated GPS 2 sensor (Z-axis)

## SIM_GPS2_HZ: GPS 2 Hz

GPS 2 Update rate

- Units: Hz

## SIM_GPS2_DRFTALT: GPS 2 Altitude Drift

*Note: This parameter is for advanced users*

GPS 2 altitude drift error

- Units: m

## SIM_GPS2_POS_X: GPS 2 Position

GPS 2 antenna phase center position relative to the body frame origin (X-axis)

- Units: m

## SIM_GPS2_POS_Y: GPS 2 Position

GPS 2 antenna phase center position relative to the body frame origin (Y-axis)

- Units: m

## SIM_GPS2_POS_Z: GPS 2 Position

GPS 2 antenna phase center position relative to the body frame origin (Z-axis)

- Units: m

## SIM_GPS2_NOISE: GPS 2 Noise

*Note: This parameter is for advanced users*

Amplitude of the GPS2 altitude error

- Units: m

## SIM_GPS2_LCKTIME: GPS 2 Lock Time

*Note: This parameter is for advanced users*

Delay in seconds before GPS2 acquires lock

- Units: s

## SIM_GPS2_ALT_OFS: GPS 2 Altitude Offset

GPS 2 Altitude Error

- Units: m

## SIM_GPS2_HDG: GPS 2 Heading

*Note: This parameter is for advanced users*

Enable GPS2 output of NMEA heading HDT sentence or UBLOX_RELPOSNED

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_GPS2_ACC: GPS 2 Accuracy

*Note: This parameter is for advanced users*

GPS 2 Accuracy

## SIM_GPS2_VERR_X: GPS 2 Velocity Error

*Note: This parameter is for advanced users*

GPS 2 Velocity Error Offsets in NED (X-axis)

## SIM_GPS2_VERR_Y: GPS 2 Velocity Error

*Note: This parameter is for advanced users*

GPS 2 Velocity Error Offsets in NED (Y-axis)

## SIM_GPS2_VERR_Z: GPS 2 Velocity Error

*Note: This parameter is for advanced users*

GPS 2 Velocity Error Offsets in NED (Z-axis)

## SIM_INIT_LAT_OFS: Initial Latitude Offset

GPS initial lat offset from origin

## SIM_INIT_LON_OFS: Initial Longitude Offset

GPS initial lon offset from origin

## SIM_INIT_ALT_OFS: Initial Altitude Offset

GPS initial alt offset from origin

## SIM_GPS_LOG_NUM: GPS Log Number

Log number for GPS:update_file()

## SIM_GPS2_JAM: GPS jamming enable

*Note: This parameter is for advanced users*

Enable simulated GPS jamming

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_MAG_RND: Mag motor noise factor

*Note: This parameter is for advanced users*

Scaling factor for simulated vibration from motors

## SIM_MAG_DELAY: Mag measurement delay

*Note: This parameter is for advanced users*

Magnetometer measurement delay

- Units: ms

## SIM_MAG_ALY_HGT: Magnetic anomaly height

*Note: This parameter is for advanced users*

Height above ground where anomally strength has decayed to 1/8 of the ground level value

- Units: m

## SIM_MAG1_ORIENT: MAG1 Orientation

*Note: This parameter is for advanced users*

MAG1 external compass orientation

## SIM_MAG1_SCALING: MAG1 Scaling factor

*Note: This parameter is for advanced users*

Scale the compass 1 to simulate sensor scale factor errors

## SIM_MAG1_DEVID: MAG1 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 1

## SIM_MAG2_DEVID: MAG2 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 2

## SIM_MAG3_DEVID: MAG3 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 3

## SIM_MAG4_DEVID: MAG2 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 4

## SIM_MAG5_DEVID: MAG5 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 5

## SIM_MAG6_DEVID: MAG6 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 6

## SIM_MAG7_DEVID: MAG7 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 7

## SIM_MAG8_DEVID: MAG8 Device ID

*Note: This parameter is for advanced users*

Device ID of simulated compass 8

## SIM_MAG1_FAIL: MAG1 Failure

*Note: This parameter is for advanced users*

Simulated failure of MAG1

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|MAG1 Failure|

## SIM_MAG2_ORIENT: MAG2 Orientation

*Note: This parameter is for advanced users*

MAG2 external compass orientation

## SIM_MAG2_FAIL: MAG2 Failure

*Note: This parameter is for advanced users*

Simulated failure of MAG2

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|MAG2 Failure|

## SIM_MAG2_SCALING: MAG2 Scaling factor

*Note: This parameter is for advanced users*

Scale the compass 2 to simulate sensor scale factor errors

## SIM_MAG3_FAIL: MAG3 Failure

*Note: This parameter is for advanced users*

Simulated failure of MAG3

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|MAG3 Failure|

## SIM_MAG3_SCALING: MAG3 Scaling factor

*Note: This parameter is for advanced users*

Scale the compass 3 to simulate sensor scale factor errors

## SIM_MAG3_ORIENT: MAG3 Orientation

*Note: This parameter is for advanced users*

MAG3 external compass orientation

## SIM_MAG_SAVE_IDS: Save MAG devids on startup

*Note: This parameter is for advanced users*

This forces saving of compass devids on startup so that simulated compasses start as calibrated

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_IMUT_START: IMU temperature start

Starting IMU temperature of a curve

## SIM_IMUT_END: IMU temperature end

Ending IMU temperature of a curve

## SIM_IMUT_TCONST: IMU temperature time constant

IMU temperature time constant of the curve

## SIM_IMUT_FIXED: IMU fixed temperature

IMU fixed temperature by user

## SIM_ACC1_BIAS_X: Accel 1 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (X-axis)

## SIM_ACC1_BIAS_Y: Accel 1 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Y-axis)

## SIM_ACC1_BIAS_Z: Accel 1 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Z-axis)

## SIM_ACC2_BIAS_X: Accel 2 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (X-axis)

## SIM_ACC2_BIAS_Y: Accel 2 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Y-axis)

## SIM_ACC2_BIAS_Z: Accel 2 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Z-axis)

## SIM_ACC3_BIAS_X: Accel 3 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (X-axis)

## SIM_ACC3_BIAS_Y: Accel 3 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Y-axis)

## SIM_ACC3_BIAS_Z: Accel 3 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Z-axis)

## SIM_GYR1_RND: Gyro 1 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_GYR2_RND: Gyro 2 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_GYR3_RND: Gyro 3 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_ACC1_RND: Accel 1 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_ACC2_RND: Accel 2 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_ACC3_RND: Accel 3 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_GYR1_SCALE_X: Gyro 1 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (X-axis)

## SIM_GYR1_SCALE_Y: Gyro 1 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Y-axis)

## SIM_GYR1_SCALE_Z: Gyro 1 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Z-axis)

## SIM_GYR2_SCALE_X: Gyro 2 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (X-axis)

## SIM_GYR2_SCALE_Y: Gyro 2 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Y-axis)

## SIM_GYR2_SCALE_Z: Gyro 2 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Z-axis)

## SIM_GYR3_SCALE_X: Gyro 3 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (X-axis)

## SIM_GYR3_SCALE_Y: Gyro 3 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Y-axis)

## SIM_GYR3_SCALE_Z: Gyro 3 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Z-axis)

## SIM_ACCEL1_FAIL: ACCEL1 Failure

*Note: This parameter is for advanced users*

Simulated failure of ACCEL1

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|ACCEL1 Failure|

## SIM_ACCEL2_FAIL: ACCEL2 Failure

*Note: This parameter is for advanced users*

Simulated failure of ACCEL2

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|ACCEL2 Failure|

## SIM_ACCEL3_FAIL: ACCEL3 Failure

*Note: This parameter is for advanced users*

Simulated failure of ACCEL3

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|ACCEL3 Failure|

## SIM_GYR_FAIL_MSK: Gyro Failure Mask

*Note: This parameter is for advanced users*

Determines if the gyro reading updates are stopped when for an IMU simulated failure by ACCELx_FAIL params

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Readings stopped|

## SIM_ACC_FAIL_MSK: Accelerometer Failure Mask

*Note: This parameter is for advanced users*

Determines if the acclerometer reading updates are stopped when for an IMU simulated failure by ACCELx_FAIL params

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Readings stopped|

## SIM_ACC1_SCAL_X: Accel 1 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (X-axis)

## SIM_ACC1_SCAL_Y: Accel 1 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Y-axis)

## SIM_ACC1_SCAL_Z: Accel 1 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Z-axis)

## SIM_ACC2_SCAL_X: Accel 2 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (X-axis)

## SIM_ACC2_SCAL_Y: Accel 2 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Y-axis)

## SIM_ACC2_SCAL_Z: Accel 2 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Z-axis)

## SIM_ACC3_SCAL_X: Accel 3 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (X-axis)

## SIM_ACC3_SCAL_Y: Accel 3 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Y-axis)

## SIM_ACC3_SCAL_Z: Accel 3 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Z-axis)

## SIM_SAIL_TYPE: Sailboat simulation sail type

0: mainsail with sheet, 1: directly actuated wing

## SIM_JSON_MASTER: JSON master instance

the instance number to  take servos from

## SIM_OH_MASK: SIM-on_hardware Output Enable Mask

channels which are passed through to actual hardware when running sim on actual hardware

## SIM_GYR_FILE_RW: Gyro data to/from files

Read and write gyro data to/from files

|Value|Meaning|
|:---:|:---:|
|0|Stop writing data|
|1|Read data from file|
|2|Write data to a file|
|3|Read data from file and stop on EOF|

## SIM_ACC_FILE_RW: Accelerometer data to/from files

Read and write accelerometer data to/from files

|Value|Meaning|
|:---:|:---:|
|0|Stop writing data|
|1|Read data from file|
|2|Write data to a file|
|3|Read data from file and stop on EOF|

## SIM_GYR1_BIAS_X: First Gyro bias on X axis

*Note: This parameter is for advanced users*

First Gyro bias on X axis

- Units: rad/s

## SIM_GYR1_BIAS_Y: First Gyro bias on Y axis

*Note: This parameter is for advanced users*

First Gyro bias on Y axis

- Units: rad/s

## SIM_GYR1_BIAS_Z: First Gyro bias on Z axis

*Note: This parameter is for advanced users*

First Gyro bias on Z axis

- Units: rad/s

## SIM_GYR2_BIAS_X: Second Gyro bias on X axis

*Note: This parameter is for advanced users*

Second Gyro bias on X axis

- Units: rad/s

## SIM_GYR2_BIAS_Y: Second Gyro bias on Y axis

*Note: This parameter is for advanced users*

Second Gyro bias on Y axis

- Units: rad/s

## SIM_GYR2_BIAS_Z: Second Gyro bias on Z axis

*Note: This parameter is for advanced users*

Second Gyro bias on Z axis

- Units: rad/s

## SIM_GYR3_BIAS_X: Third Gyro bias on X axis

*Note: This parameter is for advanced users*

Third Gyro bias on X axis

- Units: rad/s

## SIM_GYR3_BIAS_Y: Third Gyro bias on Y axis

*Note: This parameter is for advanced users*

Third Gyro bias on Y axis

- Units: rad/s

## SIM_GYR3_BIAS_Z: Third Gyro bias on Z axis

*Note: This parameter is for advanced users*

Third Gyro bias on Z axis

- Units: rad/s

## SIM_ACC4_SCAL_X: Accel 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (X-axis)

## SIM_ACC4_SCAL_Y: Accel 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Y-axis)

## SIM_ACC4_SCAL_Z: Accel 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Z-axis)

## SIM_ACCEL4_FAIL: ACCEL4 Failure

*Note: This parameter is for advanced users*

Simulated failure of ACCEL4

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|ACCEL4 Failure|

## SIM_GYR4_SCALE_X: Gyro 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (X-axis)

## SIM_GYR4_SCALE_Y: Gyro 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Y-axis)

## SIM_GYR4_SCALE_Z: Gyro 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Z-axis)

## SIM_ACC4_RND: Accel 4 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_GYR4_RND: Gyro 4 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_ACC4_BIAS_X: Accel 4 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (X-axis)

## SIM_ACC4_BIAS_Y: Accel 4 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Y-axis)

## SIM_ACC4_BIAS_Z: Accel 4 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Z-axis)

## SIM_GYR4_BIAS_X: Fourth Gyro bias on X axis

*Note: This parameter is for advanced users*

Fourth Gyro bias on X axis

- Units: rad/s

## SIM_GYR4_BIAS_Y: Fourth Gyro bias on Y axis

*Note: This parameter is for advanced users*

Fourth Gyro bias on Y axis

- Units: rad/s

## SIM_GYR4_BIAS_Z: Fourth Gyro bias on Z axis

*Note: This parameter is for advanced users*

Fourth Gyro bias on Z axis

- Units: rad/s

## SIM_ACC5_SCAL_X: Accel 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (X-axis)

## SIM_ACC5_SCAL_Y: Accel 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Y-axis)

## SIM_ACC5_SCAL_Z: Accel 4 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated accelerometer (Z-axis)

## SIM_ACCEL5_FAIL: ACCEL5 Failure

*Note: This parameter is for advanced users*

Simulated failure of ACCEL5

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|ACCEL5 Failure|

## SIM_GYR5_SCALE_X: Gyro 5 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (X-axis)

## SIM_GYR5_SCALE_Y: Gyro 5 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Y-axis)

## SIM_GYR5_SCALE_Z: Gyro 5 scaling factor

*Note: This parameter is for advanced users*

scaling factors applied to simulated gyroscope (Z-axis)

## SIM_ACC5_RND: Accel 5 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_GYR5_RND: Gyro 5 motor noise factor

*Note: This parameter is for advanced users*

scaling factor for simulated vibration from motors

## SIM_ACC5_BIAS_X: Accel 5 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (X-axis)

## SIM_ACC5_BIAS_Y: Accel 5 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Y-axis)

## SIM_ACC5_BIAS_Z: Accel 5 bias

*Note: This parameter is for advanced users*

bias of simulated accelerometer sensor (Z-axis)

## SIM_GYR5_BIAS_X: Fifth Gyro bias on X axis

*Note: This parameter is for advanced users*

Fifth Gyro bias on X axis

- Units: rad/s

## SIM_GYR5_BIAS_Y: Fifth Gyro bias on Y axis

*Note: This parameter is for advanced users*

Fifth Gyro bias on Y axis

- Units: rad/s

## SIM_GYR5_BIAS_Z: Fifth Gyro bias on Z axis

*Note: This parameter is for advanced users*

Fifth Gyro bias on Z axis

- Units: rad/s

## SIM_OH_RELAY_MSK: SIM-on_hardware Relay Enable Mask

Allow relay output operation when running SIM-on-hardware

## SIM_CLAMP_CH: Simulated Clamp Channel

If non-zero the vehicle will be clamped in position until the value on this servo channel passes 1800PWM

# SIMARSPD2 Parameters

## SIM_ARSPD2_FAIL: Airspeed sensor failure

*Note: This parameter is for advanced users*

Simulates Airspeed sensor 1 failure

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_ARSPD2_FAILP: Airspeed sensor failure pressure

*Note: This parameter is for advanced users*

Simulated airspeed sensor failure pressure

- Units: Pa

## SIM_ARSPD2_PITOT: Airspeed pitot tube failure pressure

*Note: This parameter is for advanced users*

Simulated airspeed sensor pitot tube failure pressure

- Units: Pa

## SIM_ARSPD2_SIGN: Airspeed signflip

*Note: This parameter is for advanced users*

Simulated airspeed sensor with reversed pitot/static connections

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_ARSPD2_RATIO: Airspeed ratios

*Note: This parameter is for advanced users*

Simulated airspeed sensor ratio

# SIMARSPD Parameters

## SIM_ARSPD_FAIL: Airspeed sensor failure

*Note: This parameter is for advanced users*

Simulates Airspeed sensor 1 failure

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_ARSPD_FAILP: Airspeed sensor failure pressure

*Note: This parameter is for advanced users*

Simulated airspeed sensor failure pressure

- Units: Pa

## SIM_ARSPD_PITOT: Airspeed pitot tube failure pressure

*Note: This parameter is for advanced users*

Simulated airspeed sensor pitot tube failure pressure

- Units: Pa

## SIM_ARSPD_SIGN: Airspeed signflip

*Note: This parameter is for advanced users*

Simulated airspeed sensor with reversed pitot/static connections

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_ARSPD_RATIO: Airspeed ratios

*Note: This parameter is for advanced users*

Simulated airspeed sensor ratio

# SIMBAR2 Parameters

## SIM_BAR2_RND: Barometer noise

*Note: This parameter is for advanced users*

Barometer noise in height

- Units: m

## SIM_BAR2_DRIFT: Barometer altitude drift

*Note: This parameter is for advanced users*

Barometer altitude drifts at this rate

- Units: m/s

## SIM_BAR2_DISABLE: Barometer disable

*Note: This parameter is for advanced users*

Disable barometer in SITL

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## SIM_BAR2_GLITCH: Barometer glitch

*Note: This parameter is for advanced users*

Barometer glitch height in SITL

- Units: m

## SIM_BAR2_FREEZE: Barometer freeze

*Note: This parameter is for advanced users*

Freeze barometer to last recorded altitude

## SIM_BAR2_DELAY: Barometer delay

*Note: This parameter is for advanced users*

Barometer data time delay

- Units: ms

## SIM_BAR2_WCF_FWD: Wind coefficient forward

*Note: This parameter is for advanced users*

Barometer wind coefficient direction forward in SITL

## SIM_BAR2_WCF_BAK: Wind coefficient backward

*Note: This parameter is for advanced users*

Barometer wind coefficient direction backward in SITL

## SIM_BAR2_WCF_RGT: Wind coefficient right

*Note: This parameter is for advanced users*

Barometer wind coefficient direction right in SITL

## SIM_BAR2_WCF_LFT: Wind coefficient left

*Note: This parameter is for advanced users*

Barometer wind coefficient direction left in SITL

## SIM_BAR2_WCF_UP: Wind coefficient up

*Note: This parameter is for advanced users*

Barometer wind coefficient direction up in SITL

## SIM_BAR2_WCF_DN: Wind coefficient down

*Note: This parameter is for advanced users*

Barometer wind coefficient direction down in SITL

# SIMBAR3 Parameters

## SIM_BAR3_RND: Barometer noise

*Note: This parameter is for advanced users*

Barometer noise in height

- Units: m

## SIM_BAR3_DRIFT: Barometer altitude drift

*Note: This parameter is for advanced users*

Barometer altitude drifts at this rate

- Units: m/s

## SIM_BAR3_DISABLE: Barometer disable

*Note: This parameter is for advanced users*

Disable barometer in SITL

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## SIM_BAR3_GLITCH: Barometer glitch

*Note: This parameter is for advanced users*

Barometer glitch height in SITL

- Units: m

## SIM_BAR3_FREEZE: Barometer freeze

*Note: This parameter is for advanced users*

Freeze barometer to last recorded altitude

## SIM_BAR3_DELAY: Barometer delay

*Note: This parameter is for advanced users*

Barometer data time delay

- Units: ms

## SIM_BAR3_WCF_FWD: Wind coefficient forward

*Note: This parameter is for advanced users*

Barometer wind coefficient direction forward in SITL

## SIM_BAR3_WCF_BAK: Wind coefficient backward

*Note: This parameter is for advanced users*

Barometer wind coefficient direction backward in SITL

## SIM_BAR3_WCF_RGT: Wind coefficient right

*Note: This parameter is for advanced users*

Barometer wind coefficient direction right in SITL

## SIM_BAR3_WCF_LFT: Wind coefficient left

*Note: This parameter is for advanced users*

Barometer wind coefficient direction left in SITL

## SIM_BAR3_WCF_UP: Wind coefficient up

*Note: This parameter is for advanced users*

Barometer wind coefficient direction up in SITL

## SIM_BAR3_WCF_DN: Wind coefficient down

*Note: This parameter is for advanced users*

Barometer wind coefficient direction down in SITL

# SIMBARO Parameters

## SIM_BARO_RND: Barometer noise

*Note: This parameter is for advanced users*

Barometer noise in height

- Units: m

## SIM_BARO_DRIFT: Barometer altitude drift

*Note: This parameter is for advanced users*

Barometer altitude drifts at this rate

- Units: m/s

## SIM_BARO_DISABLE: Barometer disable

*Note: This parameter is for advanced users*

Disable barometer in SITL

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## SIM_BARO_GLITCH: Barometer glitch

*Note: This parameter is for advanced users*

Barometer glitch height in SITL

- Units: m

## SIM_BARO_FREEZE: Barometer freeze

*Note: This parameter is for advanced users*

Freeze barometer to last recorded altitude

## SIM_BARO_DELAY: Barometer delay

*Note: This parameter is for advanced users*

Barometer data time delay

- Units: ms

## SIM_BARO_WCF_FWD: Wind coefficient forward

*Note: This parameter is for advanced users*

Barometer wind coefficient direction forward in SITL

## SIM_BARO_WCF_BAK: Wind coefficient backward

*Note: This parameter is for advanced users*

Barometer wind coefficient direction backward in SITL

## SIM_BARO_WCF_RGT: Wind coefficient right

*Note: This parameter is for advanced users*

Barometer wind coefficient direction right in SITL

## SIM_BARO_WCF_LFT: Wind coefficient left

*Note: This parameter is for advanced users*

Barometer wind coefficient direction left in SITL

## SIM_BARO_WCF_UP: Wind coefficient up

*Note: This parameter is for advanced users*

Barometer wind coefficient direction up in SITL

## SIM_BARO_WCF_DN: Wind coefficient down

*Note: This parameter is for advanced users*

Barometer wind coefficient direction down in SITL

# SIMGLD Parameters

## SIM_GLD_BLN_BRST: balloon burst height

balloon burst height

- Units: m

## SIM_GLD_BLN_RATE: balloon climb rate

balloon climb rate

- Units: m/s

# SIMGRPE Parameters

## SIM_GRPE_ENABLE: Gripper servo Sim enable/disable

*Note: This parameter is for advanced users*

Allows you to enable (1) or disable (0) the gripper servo simulation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_GRPE_PIN: Gripper emp pin

*Note: This parameter is for advanced users*

The pin number that the gripper emp is connected to. (start at 1)

- Range: 0 15

# SIMGRPS Parameters

## SIM_GRPS_ENABLE: Gripper servo Sim enable/disable

*Note: This parameter is for advanced users*

Allows you to enable (1) or disable (0) the gripper servo simulation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_GRPS_PIN: Gripper servo pin

*Note: This parameter is for advanced users*

The pin number that the gripper servo is connected to. (start at 1)

- Range: 0 15

## SIM_GRPS_GRAB: Gripper Grab PWM

*Note: This parameter is for advanced users*

PWM value in microseconds sent to Gripper to initiate grabbing the cargo

- Range: 1000 2000

- Units: PWM

## SIM_GRPS_RELEASE: Gripper Release PWM

*Note: This parameter is for advanced users*

PWM value in microseconds sent to Gripper to release the cargo

- Range: 1000 2000

- Units: PWM

## SIM_GRPS_REVERSE: Gripper close direction

*Note: This parameter is for advanced users*

Reverse the closing direction.

|Value|Meaning|
|:---:|:---:|
|0|Normal|
|1|Reverse|

# SIMPLD Parameters

## SIM_PLD_ENABLE: Preland device Sim enable/disable

*Note: This parameter is for advanced users*

Allows you to enable (1) or disable (0) the Preland simulation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_PLD_LAT: Precland device center's latitude

*Note: This parameter is for advanced users*

Precland device center's latitude

- Units: deg

- Increment: 0.000001

- Range: -90 90

## SIM_PLD_LON: Precland device center's longitude

*Note: This parameter is for advanced users*

Precland device center's longitude

- Units: deg

- Increment: 0.000001

- Range: -180 180

## SIM_PLD_HEIGHT: Precland device center's height SITL origin

*Note: This parameter is for advanced users*

Precland device center's height above SITL origin. Assumes a 2x2m square as station base

- Units: m

- Increment: 1

- Range: 0 10000

## SIM_PLD_YAW: Precland device systems rotation from north

*Note: This parameter is for advanced users*

Precland device systems rotation from north

- Units: deg

- Increment: 1

- Range: -180 +180

## SIM_PLD_RATE: Precland device update rate

*Note: This parameter is for advanced users*

Precland device rate. e.g led patter refresh rate, RF message rate, etc.

- Units: Hz

- Range: 0 200

## SIM_PLD_TYPE: Precland device radiance type

*Note: This parameter is for advanced users*

Precland device radiance type: it can be a cylinder, a cone, or a sphere.

|Value|Meaning|
|:---:|:---:|
|0|cylinder|
|1|cone|
|2|sphere|

## SIM_PLD_ALT_LIMIT: Precland device alt range

*Note: This parameter is for advanced users*

Precland device maximum range altitude

- Units: m

- Range: 0 100

## SIM_PLD_DIST_LIMIT: Precland device lateral range

*Note: This parameter is for advanced users*

Precland device maximum lateral range

- Units: m

- Range: 5 100

## SIM_PLD_ORIENT: Precland device orientation

*Note: This parameter is for advanced users*

Precland device orientation vector

|Value|Meaning|
|:---:|:---:|
|0|Front|
|4|Back|
|24|Up|

## SIM_PLD_OPTIONS: SIM_Precland extra options

*Note: This parameter is for advanced users*

SIM_Precland extra options

- Bitmask: 0: Enable target distance

## SIM_PLD_SHIP: SIM_Precland follow ship

*Note: This parameter is for advanced users*

This makes the position of the landing beacon follow the simulated ship from SIM_SHIP. The ship movement is controlled with the SIM_SHIP parameters

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

# SIMRFL Parameters

## SIM_RFL_OPTS: FlightAxis options

*Note: This parameter is for advanced users*

Bitmask of FlightAxis options

- Bitmask: 0: Reset position on startup, 1: Swap first 4 and last 4 servos (for quadplane testing), 2: Demix heli servos and send roll/pitch/collective/yaw, 3: Don't print frame rate stats

# SIMSB Parameters

## SIM_SB_MASS: mass

mass of blimp not including lifting gas

- Units: kg

## SIM_SB_HMASS: helium mass

mass of lifting gas

- Units: kg

## SIM_SB_ARM_LEN: arm length

distance from center of mass to one motor

- Units: m

## SIM_SB_MOT_THST: motor thrust

thrust at max throttle for one motor

- Units: N

## SIM_SB_DRAG_FWD: drag in forward direction

drag on X axis

## SIM_SB_DRAG_SIDE: drag in sidewards direction

drag on Y axis

## SIM_SB_DRAG_UP: drag in upward direction

drag on Z axis

## SIM_SB_MOI_YAW: moment of inertia in yaw

moment of inertia in yaw

## SIM_SB_MOI_ROLL: moment of inertia in roll

moment of inertia in roll

## SIM_SB_MOI_PITCH: moment of inertia in pitch

moment of inertia in pitch

## SIM_SB_ALT_TARG: altitude target

altitude target

- Units: m

## SIM_SB_CLMB_RT: target climb rate

target climb rate

- Units: m/s

## SIM_SB_YAW_RT: yaw rate

maximum yaw rate with full left throttle at target altitude

- Units: deg/s

## SIM_SB_MOT_ANG: motor angle

maximum motor tilt angle

- Units: deg

## SIM_SB_COL: center of lift

center of lift position above CoG

- Units: m

## SIM_SB_WVANE: weathervaning offset

center of drag for weathervaning

- Units: m

## SIM_SB_FLR: free lift rate

amount of additional lift generated by the helper balloon (for the purpose of ascent), as a proportion of the 'neutral buoyancy' lift

# SIMSERVO Parameters

## SIM_SERVO_SPEED: servo speed

servo speed (time for 60 degree deflection). If DELAY and FILTER are not set then this is converted to a 1p lowpass filter. If DELAY or FILTER are set then this is treated as a rate of change limit

- Units: s

## SIM_SERVO_DELAY: servo delay

servo delay

- Units: s

## SIM_SERVO_FILTER: servo filter

servo filter

- Units: Hz

# SIMSLUP Parameters

## SIM_SLUP_ENABLE: Slung Payload Sim enable/disable

*Note: This parameter is for advanced users*

Slung Payload Sim enable/disable

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_SLUP_WEIGHT: Slung Payload weight

*Note: This parameter is for advanced users*

Slung Payload weight in kg

- Units: kg

- Range: 0 15

## SIM_SLUP_LINELEN: Slung Payload line length

*Note: This parameter is for advanced users*

Slung Payload line length in meters

- Units: m

- Range: 0 100

## SIM_SLUP_DRAG: Slung Payload drag coefficient

*Note: This parameter is for advanced users*

Slung Payload drag coefficient.  Higher values increase drag and slow the payload more quickly

- Units: m

- Range: 0 10

## SIM_SLUP_SYSID: Slung Payload MAVLink system ID

*Note: This parameter is for advanced users*

Slung Payload MAVLink system id to distinguish it from others on the same network

- Range: 0 255

# SIMSPR Parameters

## SIM_SPR_ENABLE: Sprayer Sim enable/disable

*Note: This parameter is for advanced users*

Allows you to enable (1) or disable (0) the Sprayer simulation

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SIM_SPR_PUMP: Sprayer pump pin

*Note: This parameter is for advanced users*

The pin number that the Sprayer pump is connected to. (start at 1)

- Range: 0 15

## SIM_SPR_SPIN: Sprayer spinner servo pin

*Note: This parameter is for advanced users*

The pin number that the Sprayer spinner servo is connected to. (start at 1)

- Range: 0 15

# SPRAY Parameters

## SPRAY_ENABLE: Sprayer enable/disable

Allows you to enable (1) or disable (0) the sprayer

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## SPRAY_PUMP_RATE: Pump speed

Desired pump speed when travelling 1m/s expressed as a percentage

- Units: %

- Range: 0 100

## SPRAY_SPINNER: Spinner rotation speed

Spinner's rotation speed in PWM (a higher rate will disperse the spray over a wider area horizontally)

- Units: ms

- Range: 1000 2000

## SPRAY_SPEED_MIN: Speed minimum

Speed minimum at which we will begin spraying

- Units: cm/s

- Range: 0 1000

## SPRAY_PUMP_MIN: Pump speed minimum

Minimum pump speed expressed as a percentage

- Units: %

- Range: 0 100

# SRn Parameters

## SRn_RAW_SENS: Raw sensor stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of RAW_IMU, SCALED_IMU2, SCALED_IMU3, SCALED_PRESSURE, SCALED_PRESSURE2, SCALED_PRESSURE3 and AIRSPEED

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_EXT_STAT: Extended status stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of SYS_STATUS, POWER_STATUS, MCU_STATUS, MEMINFO, CURRENT_WAYPOINT, GPS_RAW_INT, GPS_RTK (if available), GPS2_RAW_INT (if available), GPS2_RTK (if available), NAV_CONTROLLER_OUTPUT, FENCE_STATUS, and GLOBAL_TARGET_POS_INT

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_RC_CHAN: RC Channel stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of SERVO_OUTPUT_RAW and RC_CHANNELS

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_RAW_CTRL: Raw Control stream rate

*Note: This parameter is for advanced users*

MAVLink Raw Control stream rate of SERVO_OUT

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_POSITION: Position stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of GLOBAL_POSITION_INT and LOCAL_POSITION_NED

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_EXTRA1: Extra data type 1 stream rate to ground station

*Note: This parameter is for advanced users*

MAVLink Stream rate of ATTITUDE, SIMSTATE (SIM only), AHRS2 and PID_TUNING

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_EXTRA2: Extra data type 2 stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of VFR_HUD

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_EXTRA3: Extra data type 3 stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of AHRS, SYSTEM_TIME, WIND, RANGEFINDER, DISTANCE_SENSOR, BATTERY2, BATTERY_STATUS, GIMBAL_DEVICE_ATTITUDE_STATUS, OPTICAL_FLOW, MAG_CAL_REPORT, MAG_CAL_PROGRESS, EKF_STATUS_REPORT, VIBRATION, RPM, ESC TELEMETRY, and WHEEL_DISTANCE

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_PARAMS: Parameter stream rate

*Note: This parameter is for advanced users*

MAVLink Stream rate of PARAM_VALUE

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

## SRn_ADSB: ADSB stream rate

*Note: This parameter is for advanced users*

MAVLink ADSB (AIS) stream rate

- Units: Hz

- Range: 0 50

- Increment: 1

- RebootRequired: True

# SRTL Parameters

## SRTL_ACCURACY: SmartRTL accuracy

*Note: This parameter is for advanced users*

SmartRTL accuracy. The minimum distance between points.

- Units: m

- Range: 0 10

## SRTL_POINTS: SmartRTL maximum number of points on path

*Note: This parameter is for advanced users*

SmartRTL maximum number of points on path. Set to 0 to disable SmartRTL.  100 points consumes about 3k of memory.

- Range: 0 500

- RebootRequired: True

## SRTL_OPTIONS: SmartRTL options

Bitmask of SmartRTL options.

- Bitmask: 2:Ignore pilot yaw

# STAT Parameters

## STAT_BOOTCNT: Boot Count

Number of times board has been booted

- ReadOnly: True

## STAT_FLTTIME: Total FlightTime

Total FlightTime (seconds)

- Units: s

- ReadOnly: True

## STAT_RUNTIME: Total RunTime

Total time autopilot has run

- Units: s

- ReadOnly: True

## STAT_RESET: Statistics Reset Time

Seconds since January 1st 2016 (Unix epoch+1451606400) since statistics reset (set to 0 to reset statistics, other set values will be ignored)

- Units: s

- ReadOnly: True

# TEMP Parameters

## TEMP_LOG: Logging

Enables temperature sensor logging

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Log all instances|
|2|Log only instances with sensor source set to None|

# TEMP1 Parameters

## TEMP1_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP1_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP1_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP1_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP1_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP1_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP1_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP1_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP1_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP1_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP1_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP1_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP2 Parameters

## TEMP2_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP2_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP2_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP2_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP2_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP2_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP2_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP2_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP2_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP2_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP2_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP2_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP3 Parameters

## TEMP3_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP3_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP3_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP3_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP3_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP3_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP3_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP3_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP3_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP3_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP3_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP3_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP4 Parameters

## TEMP4_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP4_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP4_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP4_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP4_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP4_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP4_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP4_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP4_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP4_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP4_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP4_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP5 Parameters

## TEMP5_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP5_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP5_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP5_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP5_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP5_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP5_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP5_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP5_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP5_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP5_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP5_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP6 Parameters

## TEMP6_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP6_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP6_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP6_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP6_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP6_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP6_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP6_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP6_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP6_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP6_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP6_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP7 Parameters

## TEMP7_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP7_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP7_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP7_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP7_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP7_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP7_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP7_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP7_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP7_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP7_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP7_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP8 Parameters

## TEMP8_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP8_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP8_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP8_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP8_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP8_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP8_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP8_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP8_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP8_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP8_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP8_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TEMP9 Parameters

## TEMP9_TYPE: Temperature Sensor Type

Enables temperature sensors

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|TSYS01|
|2|MCP9600|
|3|MAX31865|
|4|TSYS03|
|5|Analog|
|6|DroneCAN|
|7|MLX90614|

- RebootRequired: True

## TEMP9_BUS: Temperature sensor bus

*Note: This parameter is for advanced users*

Temperature sensor bus number, typically used to select from multiple I2C buses

- Range: 0 3

- RebootRequired: True

## TEMP9_ADDR: Temperature sensor address

*Note: This parameter is for advanced users*

Temperature sensor address, typically used for I2C address

- Range: 0 127

- RebootRequired: True

## TEMP9_SRC: Sensor Source

Sensor Source is used to designate which device's temperature report will be replaced by this temperature sensor's data. If 0 (None) then the data is only available via log. In the future a new Motor temperature report will be created for returning data directly.

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|ESC|
|2|Motor|
|3|Battery Index|
|4|Battery ID/SerialNumber|
|5|CAN based Pitot tube|
|6|DroneCAN-out on AP_Periph|

## TEMP9_SRC_ID: Sensor Source Identification

Sensor Source Identification is used to replace a specific instance of a system component's temperature report with the temp sensor's. Examples: TEMP_SRC = 1 (ESC), TEMP_SRC_ID = 1 will set the temp of ESC1. TEMP_SRC = 3 (BatteryIndex),TEMP_SRC_ID = 2 will set the temp of BATT2. TEMP_SRC = 4 (BatteryId/SerialNum),TEMP_SRC_ID=42 will set the temp of all batteries that have param BATTn_SERIAL = 42.

## TEMP9_PIN: Temperature sensor analog voltage sensing pin

Sets the analog input pin that should be used for temprature monitoring. Values for some autopilots are given as examples. Search wiki for "Analog pins".

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|2|Pixhawk/Pixracer/Navio2/Pixhawk2_PM1|
|5|Navigator|
|13|Pixhawk2_PM2/CubeOrange_PM2|
|14|CubeOrange|
|16|Durandal|
|100|PX4-v1|

## TEMP9_A0: Temperature sensor analog 0th polynomial coefficient

a0 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP9_A1: Temperature sensor analog 1st polynomial coefficient

a1 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP9_A2: Temperature sensor analog 2nd polynomial coefficient

a2 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP9_A3: Temperature sensor analog 3rd polynomial coefficient

a3 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP9_A4: Temperature sensor analog 4th polynomial coefficient

a4 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

## TEMP9_A5: Temperature sensor analog 5th polynomial coefficient

a5 in polynomial of form temperature in deg = a0 + a1*voltage + a2*voltage^2 + a3*voltage^3 + a4*voltage^4 + a5*voltage^5

# TRQ1 Parameters

## TRQ1_TYPE: Torqeedo connection type

Torqeedo connection type

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Tiller|
|2|Motor|

- RebootRequired: True

## TRQ1_ONOFF_PIN: Torqeedo ON/Off pin

Pin number connected to Torqeedo's on/off pin. -1 to use serial port's RTS pin if available

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

- RebootRequired: True

## TRQ1_DE_PIN: Torqeedo DE pin

Pin number connected to RS485 to Serial converter's DE pin. -1 to use serial port's CTS pin if available

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

- RebootRequired: True

## TRQ1_OPTIONS: Torqeedo Options

*Note: This parameter is for advanced users*

Torqeedo Options Bitmask

- Bitmask: 0:Log,1:Send debug to GCS

## TRQ1_POWER: Torqeedo Motor Power

*Note: This parameter is for advanced users*

Torqeedo motor power.  Only applied when using motor connection type (e.g. TRQD_TYPE=2)

- Units: %

- Range: 0 100

- Increment: 1

## TRQ1_SLEW_TIME: Torqeedo Throttle Slew Time

*Note: This parameter is for advanced users*

Torqeedo slew rate specified as the minimum number of seconds required to increase the throttle from 0 to 100%.  Higher values cause a slower response, lower values cause a faster response.  A value of zero disables the limit

- Units: s

- Range: 0 5

- Increment: 0.1

## TRQ1_DIR_DELAY: Torqeedo Direction Change Delay

*Note: This parameter is for advanced users*

Torqeedo direction change delay.  Output will remain at zero for this many seconds when transitioning between forward and backwards rotation

- Units: s

- Range: 0 5

- Increment: 0.1

## TRQ1_SERVO_FN: Torqeedo Servo Output Function

*Note: This parameter is for advanced users*

Torqeedo Servo Output Function

|Value|Meaning|
|:---:|:---:|
|70|Throttle|
|73|ThrottleLeft|
|74|ThrottleRight|

- Increment: 0.1

# TRQ2 Parameters

## TRQ2_TYPE: Torqeedo connection type

Torqeedo connection type

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Tiller|
|2|Motor|

- RebootRequired: True

## TRQ2_ONOFF_PIN: Torqeedo ON/Off pin

Pin number connected to Torqeedo's on/off pin. -1 to use serial port's RTS pin if available

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

- RebootRequired: True

## TRQ2_DE_PIN: Torqeedo DE pin

Pin number connected to RS485 to Serial converter's DE pin. -1 to use serial port's CTS pin if available

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

- RebootRequired: True

## TRQ2_OPTIONS: Torqeedo Options

*Note: This parameter is for advanced users*

Torqeedo Options Bitmask

- Bitmask: 0:Log,1:Send debug to GCS

## TRQ2_POWER: Torqeedo Motor Power

*Note: This parameter is for advanced users*

Torqeedo motor power.  Only applied when using motor connection type (e.g. TRQD_TYPE=2)

- Units: %

- Range: 0 100

- Increment: 1

## TRQ2_SLEW_TIME: Torqeedo Throttle Slew Time

*Note: This parameter is for advanced users*

Torqeedo slew rate specified as the minimum number of seconds required to increase the throttle from 0 to 100%.  Higher values cause a slower response, lower values cause a faster response.  A value of zero disables the limit

- Units: s

- Range: 0 5

- Increment: 0.1

## TRQ2_DIR_DELAY: Torqeedo Direction Change Delay

*Note: This parameter is for advanced users*

Torqeedo direction change delay.  Output will remain at zero for this many seconds when transitioning between forward and backwards rotation

- Units: s

- Range: 0 5

- Increment: 0.1

## TRQ2_SERVO_FN: Torqeedo Servo Output Function

*Note: This parameter is for advanced users*

Torqeedo Servo Output Function

|Value|Meaning|
|:---:|:---:|
|70|Throttle|
|73|ThrottleLeft|
|74|ThrottleRight|

- Increment: 0.1

# VISO Parameters

## VISO_TYPE: Visual odometry camera connection type

*Note: This parameter is for advanced users*

Visual odometry camera connection type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|MAVLink|
|2|IntelT265|
|3|VOXL(ModalAI)|

- RebootRequired: True

## VISO_POS_X: Visual odometry camera X position offset

*Note: This parameter is for advanced users*

X position of the camera in body frame. Positive X is forward of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## VISO_POS_Y: Visual odometry camera Y position offset

*Note: This parameter is for advanced users*

Y position of the camera in body frame. Positive Y is to the right of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## VISO_POS_Z: Visual odometry camera Z position offset

*Note: This parameter is for advanced users*

Z position of the camera in body frame. Positive Z is down from the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## VISO_ORIENT: Visual odometery camera orientation

*Note: This parameter is for advanced users*

Visual odometery camera orientation

|Value|Meaning|
|:---:|:---:|
|0|Forward|
|2|Right|
|4|Back|
|6|Left|
|24|Up|
|25|Down|

## VISO_SCALE: Visual odometry scaling factor

*Note: This parameter is for advanced users*

Visual odometry scaling factor applied to position estimates from sensor

## VISO_DELAY_MS: Visual odometry sensor delay

*Note: This parameter is for advanced users*

Visual odometry sensor delay relative to inertial measurements

- Units: ms

- Range: 0 250

## VISO_VEL_M_NSE: Visual odometry velocity measurement noise

*Note: This parameter is for advanced users*

Visual odometry velocity measurement noise in m/s

- Units: m/s

- Range: 0.05 5.0

## VISO_POS_M_NSE: Visual odometry position measurement noise 

*Note: This parameter is for advanced users*

Visual odometry position measurement noise minimum (meters). This value will be used if the sensor provides a lower noise value (or no noise value)

- Units: m

- Range: 0.1 10.0

## VISO_YAW_M_NSE: Visual odometry yaw measurement noise

*Note: This parameter is for advanced users*

Visual odometry yaw measurement noise minimum (radians), This value will be used if the sensor provides a lower noise value (or no noise value)

- Units: rad

- Range: 0.05 1.0

## VISO_QUAL_MIN: Visual odometry minimum quality

*Note: This parameter is for advanced users*

Visual odometry will only be sent to EKF if over this value. -1 to always send (even bad values), 0 to send if good or unknown

- Units: %

- Range: -1 100

# VTX Parameters

## VTX_ENABLE: Is the Video Transmitter enabled or not

Toggles the Video Transmitter on and off

|Value|Meaning|
|:---:|:---:|
|0|Disable|
|1|Enable|

## VTX_POWER: Video Transmitter Power Level

Video Transmitter Power Level. Different VTXs support different power levels, the power level chosen will be rounded down to the nearest supported power level

- Range: 1 1000

## VTX_CHANNEL: Video Transmitter Channel

Video Transmitter Channel

- Range: 0 7

## VTX_BAND: Video Transmitter Band

Video Transmitter Band

|Value|Meaning|
|:---:|:---:|
|0|Band A|
|1|Band B|
|2|Band E|
|3|Airwave|
|4|RaceBand|
|5|Low RaceBand|
|6|1G3 Band A|
|7|1G3 Band B|
|8|Band X|
|9|3G3 Band A|
|10|3G3 Band B|

## VTX_FREQ: Video Transmitter Frequency

Video Transmitter Frequency. The frequency is derived from the setting of BAND and CHANNEL

- ReadOnly: True

- Range: 1000 6000

## VTX_OPTIONS: Video Transmitter Options

*Note: This parameter is for advanced users*

Video Transmitter Options. Pitmode puts the VTX in a low power state. Unlocked enables certain restricted frequencies and power levels. Do not enable the Unlocked option unless you have appropriate permissions in your jurisdiction to transmit at high power levels. One stop-bit may be required for VTXs that erroneously mimic iNav behaviour.

- Bitmask: 0:Pitmode,1:Pitmode until armed,2:Pitmode when disarmed,3:Unlocked,4:Add leading zero byte to requests,5:Use 1 stop-bit in SmartAudio,6:Ignore CRC in SmartAudio,7:Ignore status updates in CRSF and blindly set VTX options

## VTX_MAX_POWER: Video Transmitter Max Power Level

Video Transmitter Maximum Power Level. Different VTXs support different power levels, this prevents the power aux switch from requesting too high a power level. The switch supports 6 power levels and the selected power will be a subdivision between 0 and this setting.

- Range: 25 1000

# WENC Parameters

## WENC_TYPE: WheelEncoder type

What type of WheelEncoder is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Quadrature|
|10|SITL Quadrature|

## WENC_CPR: WheelEncoder counts per revolution

WheelEncoder counts per full revolution of the wheel

- Increment: 1

## WENC_RADIUS: Wheel radius

Wheel radius

- Units: m

- Increment: 0.001

## WENC_POS_X: Wheel's X position offset

X position of the center of the wheel in body frame. Positive X is forward of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## WENC_POS_Y: Wheel's Y position offset

Y position of the center of the wheel in body frame. Positive Y is to the right of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## WENC_POS_Z: Wheel's Z position offset

Z position of the center of the wheel in body frame. Positive Z is down from the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## WENC_PINA: Input Pin A

Input Pin A

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## WENC_PINB: Input Pin B

Input Pin B

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## WENC2_TYPE: Second WheelEncoder type

What type of WheelEncoder sensor is connected

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Quadrature|
|10|SITL Quadrature|

## WENC2_CPR: WheelEncoder 2 counts per revolution

WheelEncoder 2 counts per full revolution of the wheel

- Increment: 1

## WENC2_RADIUS: Wheel2's radius

Wheel2's radius

- Units: m

- Increment: 0.001

## WENC2_POS_X: Wheel2's X position offset

X position of the center of the second wheel in body frame. Positive X is forward of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## WENC2_POS_Y: Wheel2's Y position offset

Y position of the center of the second wheel in body frame. Positive Y is to the right of the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## WENC2_POS_Z: Wheel2's Z position offset

Z position of the center of the second wheel in body frame. Positive Z is down from the origin.

- Units: m

- Range: -5 5

- Increment: 0.01

## WENC2_PINA: Second Encoder Input Pin A

Second Encoder Input Pin A

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

## WENC2_PINB: Second Encoder Input Pin B

Second Encoder Input Pin B

|Value|Meaning|
|:---:|:---:|
|-1|Disabled|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|

# WNDVN Parameters

## WNDVN_TYPE: Wind Vane Type

Wind Vane type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Heading when armed|
|2|RC input offset heading when armed|
|3|Analog|
|4|NMEA|
|10|SITL true|
|11|SITL apparent|

- RebootRequired: True

## WNDVN_DIR_PIN: Wind vane analog voltage pin for direction

Analog input pin to read as wind vane direction

|Value|Meaning|
|:---:|:---:|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## WNDVN_DIR_V_MIN: Wind vane voltage minimum

Minimum voltage supplied by analog wind vane. When using pin 103, the maximum value of the parameter is 3.3V.

- Units: V

- Increment: 0.01

- Range: 0 5.0

## WNDVN_DIR_V_MAX: Wind vane voltage maximum

Maximum voltage supplied by analog wind vane. When using pin 103, the maximum value of the parameter is 3.3V.

- Units: V

- Increment: 0.01

- Range: 0 5.0

## WNDVN_DIR_OFS: Wind vane headwind offset

Angle offset when analog windvane is indicating a headwind, ie 0 degress relative to vehicle

- Units: deg

- Increment: 1

- Range: 0 360

## WNDVN_DIR_FILT: apparent Wind vane direction low pass filter frequency

apparent Wind vane direction low pass filter frequency, a value of -1 disables filter

- Units: Hz

## WNDVN_CAL: Wind vane calibration start

Start wind vane calibration by setting this to 1 or 2

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Calibrate direction|
|2|Calibrate speed|

## WNDVN_DIR_DZ: Wind vane deadzone when using analog sensor

Wind vane deadzone when using analog sensor

- Units: deg

- Increment: 1

- Range: 0 360

## WNDVN_SPEED_MIN: Wind vane cut off wind speed

Wind vane direction will be ignored when apparent wind speeds are below this value (if wind speed sensor is present).  If the apparent wind is consistently below this value the vane will not work

- Units: m/s

- Increment: 0.1

- Range: 0 5

## WNDVN_SPEED_TYPE: Wind speed sensor Type

Wind speed sensor type

|Value|Meaning|
|:---:|:---:|
|0|None|
|1|Airspeed library|
|2|Modern Devices Wind Sensor|
|3|RPM library|
|4|NMEA|
|10|SITL true|
|11|SITL apparent|

- RebootRequired: True

## WNDVN_SPEED_PIN: Wind vane speed sensor analog pin

Wind speed analog speed input pin for Modern Devices Wind Sensor rev. p

|Value|Meaning|
|:---:|:---:|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## WNDVN_TEMP_PIN: Wind vane speed sensor analog temp pin

Wind speed sensor analog temp input pin for Modern Devices Wind Sensor rev. p, set to -1 to diasble temp readings

|Value|Meaning|
|:---:|:---:|
|11|Pixracer|
|13|Pixhawk ADC4|
|14|Pixhawk ADC3|
|15|Pixhawk ADC6/Pixhawk2 ADC|
|50|AUX1|
|51|AUX2|
|52|AUX3|
|53|AUX4|
|54|AUX5|
|55|AUX6|
|103|Pixhawk SBUS|

## WNDVN_SPEED_OFS: Wind speed sensor analog voltage offset

Wind sensor analog voltage offset at zero wind speed

- Units: V

- Increment: 0.01

- Range: 0 3.3

## WNDVN_SPEED_FILT: apparent wind speed low pass filter frequency

apparent Wind speed low pass filter frequency, a value of -1 disables filter

- Units: Hz

## WNDVN_TRUE_FILT: True speed and direction low pass filter frequency

True speed and direction low pass filter frequency, a value of -1 disables filter

- Units: Hz

# WP Parameters

## WP_SPEED: Waypoint speed default

Waypoint speed default

- Units: m/s

- Range: 0 100

- Increment: 0.1

## WP_RADIUS: Waypoint radius

The distance in meters from a waypoint when we consider the waypoint has been reached. This determines when the vehicle will turn toward the next waypoint.

- Units: m

- Range: 0 100

- Increment: 0.1

## WP_ACCEL: Waypoint acceleration

Waypoint acceleration.  If zero then ATC_ACCEL_MAX is used

- Units: m/s/s

- Range: 0 100

- Increment: 0.1

## WP_JERK: Waypoint jerk

Waypoint jerk (change in acceleration).  If zero then jerk is same as acceleration

- Units: m/s/s/s

- Range: 0 100

- Increment: 0.1

# WPPIVOT Parameters

## WP_PIVOT_ANGLE: Pivot Angle

Pivot when the difference between the vehicle's heading and its target heading is more than this many degrees. Set to zero to disable pivot turns.  This parameter should be greater than 5 degrees for pivot turns to work.

- Units: deg

- Range: 0 360

- Increment: 1

## WP_PIVOT_RATE: Pivot Turn Rate

Turn rate during pivot turns

- Units: deg/s

- Range: 0 360

- Increment: 1

## WP_PIVOT_DELAY: Pivot Delay

Vehicle waits this many seconds after completing a pivot turn before proceeding

- Units: s

- Range: 0 60

- Increment: 0.1

# WRC Parameters

## WRC_ENABLE: Wheel rate control enable/disable

Enable or disable wheel rate control

|Value|Meaning|
|:---:|:---:|
|0|Disabled|
|1|Enabled|

## WRC_RATE_MAX: Wheel max rotation rate

Wheel max rotation rate

- Units: rad/s

- Range: 0 200

## WRC_RATE_FF: Wheel rate control feed forward gain

Wheel rate control feed forward gain.  Desired rate (in radians/sec) is multiplied by this constant and output to output (in the range -1 to +1)

- Range: 0.100 2.000

## WRC_RATE_P: Wheel rate control P gain

Wheel rate control P gain.  Converts rate error (in radians/sec) to output (in the range -1 to +1)

- Range: 0.100 2.000

## WRC_RATE_I: Wheel rate control I gain

Wheel rate control I gain.  Corrects long term error between the desired rate (in rad/s) and actual

- Range: 0.000 2.000

## WRC_RATE_IMAX: Wheel rate control I gain maximum

Wheel rate control I gain maximum.  Constrains the output (range -1 to +1) that the I term will generate

- Range: 0.000 1.000

## WRC_RATE_D: Wheel rate control D gain

Wheel rate control D gain.  Compensates for short-term change in desired rate vs actual

- Range: 0.000 0.400

## WRC_RATE_FILT: Wheel rate control filter frequency

Wheel rate control input filter.  Lower values reduce noise but add delay.

- Range: 1.000 100.000

- Units: Hz

## WRC_RATE_FLTT: Wheel rate control target frequency in Hz

Wheel rate control target frequency in Hz

- Range: 1 50

- Increment: 1

- Units: Hz

## WRC_RATE_FLTE: Wheel rate control error frequency in Hz

Wheel rate control error frequency in Hz

- Range: 1 50

- Increment: 1

- Units: Hz

## WRC_RATE_FLTD: Wheel rate control derivative frequency in Hz

Wheel rate control derivative frequency in Hz

- Range: 1 50

- Increment: 1

- Units: Hz

## WRC_RATE_SMAX: Wheel rate slew rate limit

*Note: This parameter is for advanced users*

Sets an upper limit on the slew rate produced by the combined P and D gains. If the amplitude of the control action produced by the rate feedback exceeds this value, then the D+P gain is reduced to respect the limit. This limits the amplitude of high frequency oscillations caused by an excessive gain. The limit should be set to no more than 25% of the actuators maximum slew rate to allow for load effects. Note: The gain will not be reduced to less than 10% of the nominal value. A value of zero will disable this feature.

- Range: 0 200

- Increment: 0.5

## WRC_RATE_PDMX: Wheel rate control PD sum maximum

Wheel rate control PD sum maximum.  The maximum/minimum value that the sum of the P and D term can output

- Range: 0.000 1.000

## WRC_RATE_D_FF: Wheel rate Derivative FeedForward Gain

*Note: This parameter is for advanced users*

FF D Gain which produces an output that is proportional to the rate of change of the error

- Range: 0.000 0.400

- Increment: 0.001

## WRC_RATE_NTF: Wheel rate Target notch filter index

*Note: This parameter is for advanced users*

Wheel rate Target notch filter index

- Range: 1 8

## WRC_RATE_NEF: Wheel rate Error notch filter index

*Note: This parameter is for advanced users*

Wheel rate Error notch filter index

- Range: 1 8

## WRC2_RATE_FF: Wheel rate control feed forward gain

Wheel rate control feed forward gain.  Desired rate (in radians/sec) is multiplied by this constant and output to output (in the range -1 to +1)

- Range: 0.100 2.000

## WRC2_RATE_P: Wheel rate control P gain

Wheel rate control P gain.  Converts rate error (in radians/sec) to output (in the range -1 to +1)

- Range: 0.100 2.000

## WRC2_RATE_I: Wheel rate control I gain

Wheel rate control I gain.  Corrects long term error between the desired rate (in rad/s) and actual

- Range: 0.000 2.000

## WRC2_RATE_IMAX: Wheel rate control I gain maximum

Wheel rate control I gain maximum.  Constrains the output (range -1 to +1) that the I term will generate

- Range: 0.000 1.000

## WRC2_RATE_D: Wheel rate control D gain

Wheel rate control D gain.  Compensates for short-term change in desired rate vs actual

- Range: 0.000 0.400

## WRC2_RATE_FILT: Wheel rate control filter frequency

Wheel rate control input filter.  Lower values reduce noise but add delay.

- Range: 1.000 100.000

- Units: Hz

## WRC2_RATE_FLTT: Wheel rate control target frequency in Hz

Wheel rate control target frequency in Hz

- Range: 1 50

- Increment: 1

- Units: Hz

## WRC2_RATE_FLTE: Wheel rate control error frequency in Hz

Wheel rate control error frequency in Hz

- Range: 1 50

- Increment: 1

- Units: Hz

## WRC2_RATE_FLTD: Wheel rate control derivative frequency in Hz

Wheel rate control derivative frequency in Hz

- Range: 1 50

- Increment: 1

- Units: Hz

## WRC2_RATE_SMAX: Wheel rate slew rate limit

*Note: This parameter is for advanced users*

Sets an upper limit on the slew rate produced by the combined P and D gains. If the amplitude of the control action produced by the rate feedback exceeds this value, then the D+P gain is reduced to respect the limit. This limits the amplitude of high frequency oscillations caused by an excessive gain. The limit should be set to no more than 25% of the actuators maximum slew rate to allow for load effects. Note: The gain will not be reduced to less than 10% of the nominal value. A value of zero will disable this feature.

- Range: 0 200

- Increment: 0.5

## WRC2_RATE_PDMX: Wheel rate control PD sum maximum

Wheel rate control PD sum maximum.  The maximum/minimum value that the sum of the P and D term can output

- Range: 0.000 1.000

## WRC2_RATE_D_FF: Wheel rate Derivative FeedForward Gain

*Note: This parameter is for advanced users*

FF D Gain which produces an output that is proportional to the rate of change of the target

- Range: 0.000 0.400

- Increment: 0.001

## WRC2_RATE_NTF: Wheel rate Target notch filter index

*Note: This parameter is for advanced users*

Wheel rate Target notch filter index

- Range: 1 8

## WRC2_RATE_NEF: Wheel rate Error notch filter index

*Note: This parameter is for advanced users*

Wheel rate Error notch filter index

- Range: 1 8