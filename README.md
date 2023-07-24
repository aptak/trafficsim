# trafficsim
Simulate traffic

Initial approach:
Model roads and intersections/circles/ramps as a grid fine enough to model
curves.  Set a "plate scale" = feet per grid pixel.
Vehicle is the base class for all vehicles.  Subclass as needed for different
types of vehicles.  Include lenth, direction and current speed of each vehicle.
Most vehicles will be rigid, maybe later allow for trucks and trailers where
this assumption breaks.

Also model traffic flow with stop lights, stop signs and speed limits.  Allow
speed limits to be broken as in real life.  Maybe later include speed cameras.

Simulation proceeds with time steps.  At each time step advance each vehicle
based on its speed and traffic/traffic control up ahead.  I.e., only enter
intersection if light is yellow or green, reduce speed if light is yellow (later
allow for more aggressive driving).  Stop at stop signs, read lights, and
stopped traffic in front.  Allow for a response time for the first car at
intersection to notice that light is green or traffic is clear at a stop sign.

Vehicle class parameters:
 len_ft = length (in feet)
 len = length in grid "pixels"
 x_ft,y_ft position of front of vehicle (in ft)
 x, y x,y position on traffic grid (integer indices)
 direction relative to north in degrees, i.e., 90 degrees = east.
    - For simplicity, quantize this is 45 deg. intervals intially.
 speed_ft speed in ft/time inveral
 speed = speed in "pixels" / time interval
 id - unique id for this vehicle
 vtype - what type of vehicle is this (redundant if vehicles types are
       subclassed but also can be useful to have this stored in baseclass)

Vehicle_car, van, truck, etc subclass of Vehicle parameters:
static default_len_ft = used to simply track default length of each type of vehicle, later may have subclass fns.
 
TrafficGrid class parameters:
- x,y "image" of car positions, intersections, traffic lights and stop signs
TrafficGrid functions
- visualize: draw grid on screen probably using curses

FlowControl = base class for what is controling flow of traffic through a position (typically intersection)
- posn = x,y position on grid of traffic light
- direction = always one of 0, 90, 180, 270


TrafficLight public subclass of FlowControl  parameters:
- current state = red, yellow or green
- time_s = time in secs since last change: elapsed time for current state
- time = time in time intervals since last change
- state_durations_s[] = total duration in seconds for each state
- state_durations[] = total duration in time intervals for each state

StopSign public subclass of FlowControl parameters:
- inherits x,y, direction
- NumStopSigns = 1 (or could be, e.g., 4 for a four-way stop)

Lane parameters:
- posn = starting x,y position of lane
- direction = 0,90,180,270
- length = length in pixels of lane
- speed_limit_mph = speed limit is miles per hour
- speed_limit_fts = speed limit in feet per second
- speed_limit = speed limits in pixels/time interval = speed_limit_fts * time_step_s / plate_scale

Intersection parameters:
- posn = x,y position on grid of center of intersection
- lanes = vector of lanes that cross intersection

TrafficSim parameters:
- time_step_s =  seconds per time interval
- elapsed time / no. of iterations
- grid = TrafficGrid
- vehicles = vector<Vehicles>
- Traffic_lights: vector<TrafficLight>
- plate_scale = ft/pixel

TrafficSim functions
- Step: move every vehicle to next position when possible, updating speeds, etc.
- StepVehicle: for given vehicle, move to next grid position if possible
- Update
- FtToPixels:convert feet to pixels
- SecToTimeStep: convert seconds to time steps
- ReadConfig: read in configuration file giving grid layout with lanes, intersections, stop lights and signs, no. and types of vehicles
- 

