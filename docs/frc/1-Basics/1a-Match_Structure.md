# Match Structure

## Autonomous vs. Teleoperated

Competition matches are divided into two main periods: *autonomous* and *teleoperated* (teleop). In autonomous, the robot can move/score independent of driver control, running *solely* on code (there are exceptions to this in some years, e.g. 2019, where both driver control and autonomous routines were legal). Subsequently, in teleop, the robot is controlled by the drive team. 

Once the match starts, autonomous begins and it lasts for 15 seconds. Then, teleop begins and lasts for 135 seconds. The match ends when teleop ends. 

During the autonomous period, we generally want to score points and position the robot appropriately for teleop. Thus, we tend to do a lot of preparation for this period. (See the [Autonomous section](https://github.com/FRC1257/robotics-training/tree/master/frc/4.%20Autonomous) for more details.)

## Robot State & Functions

There are two types of general functions the robot executes: `init()` functions, which run at *the beginning of* specific times, and `periodic()` functions, which run *during* specific times. The `init()` functions are as follows: 

- `robotInit()` - run once, after the robot is finished powering on
- `autonomousInit()` - run once at the start of auto
- `teleopInit()` - run once at the start of teleop

and the `periodic()` ones, which run at 50 Hz, or every 20 ms:

- `robotPeriodic()` - run if the robot is on
- `autonomousPeriodic()` - run periodically during auto
- `teleopPeriodic()` - run periodically during teleop

There are two more functions we use, `testInit()` and `testPeriodic()`. While these are not directly tied to the structure of the match, they are useful when things need to be separated during robot testing. The testing period would be controlled through the [Driver Station](https://docs.wpilib.org/en/latest/docs/software/driverstation/driver-station.html). 

<hr>

Here is a brief order of the states the robot goes through:

1. Robot is turned on and the roboRIO boots.
2. The roboRIO finishes booting and user code (i.e. our robot code) is run.
3. Our robot code starts, first running `robotInit()`.
5. Our robot repeats `robotPeriodic()` for the remainder of the time the robot is powered on.
6. When the match begins, the `autonomousInit()` function is called, followed by `autonomousPeriodic()` until the end of autonomous.
7. When autonomous is over, and the field has confirmed that all robots have been disabled, we are transitioned into `teleopInit()`.
8. If `teleopInit()` has exited with no issue, we're moved into `teleopPeriodic()` for the remainder of the match.