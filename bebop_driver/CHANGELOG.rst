^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package bebop_driver
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

0.5.1 (2016-05-04)
------------------
* Add bebop_description as a build dep to bebop_driver (fixes `#45 <https://github.com/AutonomyLab/bebop_autonomy/issues/45>`_)
* Fix inline build of arsdk to use the frozen manifest (fixes `#46 <https://github.com/AutonomyLab/bebop_autonomy/issues/46>`_)
  - Prior to this release, the build script would always compile the
  development branch of ARSDK. This fix ensures that instead of
  `default.xml` manifest file - which represents the dev version of ARSDK
  package - `release.xml` is used by `repo`. This manifest file includes a
  certain hash for each ARSDK package that enforces a consistent build for
  ARSDK.
* Contributors: Mani Monajjemi

0.5.0 (2016-04-01)
------------------
* Based on Parrot ARSDK 3.8.3. Tested with Bebop 1.0 (2.0.57) and Bebop 2.0 (3.1.0)
* Update to SDK 3.8.3
  - SDK 3.8.3 from
  https://github.com/Parrot-Developers/arsdk_manifests.git
  - SDK 3.8.3 git hash: 2930cc7f7a79173d51c1fc167475fa9fa6650def
* Add support for VideoStream v2.0
* Publish TF
* Experimental implementation of odometery (pose, velocity)
* Publish the GPS fix as a ROS standard message (closes `#39 <https://github.com/AutonomyLab/bebop_autonomy/issues/39>`_)
  - Message type: sensor_msgs/NavSatFix
  - Topic: fix
* Add joint state publisher for camera's pan/tilt
  - Add a new param to enable/disable the TF publisher for odom
  - Add a new param to set the odom frame id
* Include bebop_description and robot_state_publisher in driver's launch
  files
* Add proper limitations for camera's pan/tilt joints
* Add explicit linkage to libav (fixes `#32 <https://github.com/AutonomyLab/bebop_autonomy/issues/32>`_)
* Fix libav API inconsistency issues #30 #35 #36
* Improve H264 parameter update method
  - Implement a better way to pass SPS/PPS params to H264 decoder (SDK
  3.8.x)
* Add a new CMake option "RUN_HARDWARE_TESTS" to explicitly enable hardware in the loop testing (disabled by default)
* Contributors: Mani Monajjemi, chartoin, Jake Bruce

0.4.1 (2016-02-17)
------------------
* Add ROS API for recording on-board picture/video (closes `#5 <https://github.com/AutonomyLab/bebop_autonomy/issues/5>`_)
* Add a new ROS topic for taking on-board snapshot: `snapshot`
* Add a new ROS topic for toggling on-board video recording: `record`
* Update the docs
* Add curl as a rosdep build dep (fixes `#33 <https://github.com/AutonomyLab/bebop_autonomy/issues/33>`_)
* Fix a bug in bebop_driver's nodelet destructor
* Fix a bug in ASyncSub class
* Contributors: Mani Monajjemi

0.4.0 (2016-01-17)
------------------
* Update Parrot SDK to 3.7.5 (from 3.6)
  - Remove upstream XML hash from .msg files to minmize msg type changes from now on
  - New Topic and Message type for `DefaultCameraOrientation`
* Add cmd_vel timeout for safety
  - The driver now sends stop command if no new cmd_vel is received
  within a pre-defined timeout period. This timeout is set to 0.1s by default and can be changed via `cmd_vel_timeout` parameter.
* Fix right-jand rule bug of angular.z @jacobperron (fixes `#26 <https://github.com/AutonomyLab/bebop_autonomy/issues/26>`_)
* Patch ARSDK to fix Sanselan's old URL
  - This is temporary and must be reverted when this is fixed upstream.
  Issue reported here: `Parrot-Developers/ARSDKBuildUtils#61 <https://github.com/Parrot-Developers/ARSDKBuildUtils/issues/61>`_
* Add bebop ip address as ROS parameter (fixes `#19 <https://github.com/AutonomyLab/bebop_autonomy/issues/19>`_) - (Param name: `bebop_ip`, default value: 192.168.42.1)
* Fix CameraInfo issues (closes `#10 <https://github.com/AutonomyLab/bebop_autonomy/issues/10>`_)
  - Fix bugs in loading camera calibration data and update the tests
  - Add a sample calibration file for bebop camera: bebop_camera_calib.yaml
  - Load camera calibration file by default in both node/nodelet launch
  files
* Remove redundant bebop.launch file (closes `#11 <https://github.com/AutonomyLab/bebop_autonomy/issues/11>`_)
* Fix coordinate system inconsistencies (fixes `#13 <https://github.com/AutonomyLab/bebop_autonomy/issues/13>`_)
  - Fix cmd_vel.linear.y sign error
  - Use attitude values in tests instead of velocities
* Contributors: Anup, Mani Monajjemi, Jacob Perron

0.3.0 (2015-09-17)
------------------
* Renamed package to bebop_driver
* Built against ARSDK3_version_3_6
* bebop_autonomy is now a metapackage
  - bebop_autonomy is the ROS metapackage name
  - Rename bebop_autonomy package to bebop_driver
  - Rename bebop_autonomy_msgs to bebop_msgs
* Contributors: Mani Monajjemi

0.2.0 (2015-09-10)
------------------
* Finalized documentation
* Remove bebop_autonomy's dependency to image_view
* Imrovements to code autogeneration scripts.
* CLAMP values for cmd_vels and anim_id
* Added contents to almost all doc pages
* Bebop In The Loop tests (first revision)
* Fixed more style (lint) issues
* Finalized the first revision of tests
* Add autogenerated docs for Settings, Topics and Params
* Contributors: Mani Monajjemi

0.1.2 (2015-09-05)
------------------
* Move 'state' params to their own param namespace
* Add missing unzip dep to package.xml
* Contributors: Mani Monajjemi

0.1.1 (2015-09-04)
------------------
* Add support for downloading and building ARDroneSDK3 during the build process
* Add flattrim, flip and navigatehome interfaces
* Add forward declaration to classes where it is possible
* Major bug fixes and improvements
  - Dynamic Reconfigure: Convert all two state int_t values to enum
  - Fix the private nodehandle bugs in  State and Settings handlers
  - Fix the data flow of Settings between rosparam and dynamic reconfigure
  and bebop
  - Fix SDK enum types in C (I32 instead of U8)
  - Add Start/Stop streaming to Bebop interface class
* Add bebop_nodelet launch with image_view
* Organized DynR configs into groups
  + Moved the autogeneration report to a seperated file
  + build speed improvements
* Dynamically reconfigurable Bebop settings
* Add support to enable publishing of a specific State
* Add support to propogate states from bebop to ROS
* Auto-generated .msg and .h files based on libARCommands XML files
* New threading model for data retreival and publishing
  - Nodelet now manages its own thread to receive frames from Bebop
  - GetFrame() function abstracts all sync to access the rgb frame
  - All subscribers send commands to the Bebop in their callbacks
* Integreate ARSAL logs into ROS_LOG
  - Fix sync issues between frame grabber and publisher
* Improve video decode/publish pipeline
  - Adopt frame decoding from official examples
  - Thread safe access to raw frame ptr
  - Synchronised frame decoding and publishing
* Proof of concept ROS driver for bebop drone
* Contributors: Mani Monajjemi
