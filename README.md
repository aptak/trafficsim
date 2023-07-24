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
 length (in feet)
 length_grid (in "pixels")
 x,y position of front of vehicle (in ft probably)
 x_grid, y_grid x,y position on traffic grid (integer indices)
 direction relative to north in degrees, i.e., 90 degrees = east.
    - For simplicity, quantize this is 45 deg. intervals intially.
 speed speed in ft/time inveral
 speed_grid = speed in "pixels" / s
 id - unique id for this vehicle
 vtype - what type of vehicle is this (redundant if vehicles types are
       subclassed but also can be useful to have this stored in baseclass)
 
TrafficGrid class parameters:
- x,y "image" of car positions, intersections, traffic lights and stop signs
TrafficGrid functions
- visualize: draw grid on screen probably using curses


TrafficLight parameters:
- posn = x,y position on grid of traffic light
- direction = always one of 0, 90, 180, 270
- current state = red, yellow or green
- time since last change: elapsed time for current state
- state_durations[] = total elapse time for each state

StopSign parameters:
- posn = x,y position on grid of traffic light
- direction = always one of 0, 90, 180, 270

Lane parameters:
- posn = starting x,y position of lane
- direction = 0,90,180,270
- length = length in pixels of lane

TrafficSim parameters:
- time step
- elapsed time / no. of iterations
- grid of type TrafficGrid
- vehicles = vector<Vehicles>
- Traffic_lights: position and directions of traffic lights

TrafficSim functions
- Step: move every vehicle to next position when possible, updating speeds, etc.
- Step_vehicle: for given vehicle, move to next grid position if possible
- Update


