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
 x,y position of front of vehicle
 direction relative to north in degrees, i.e., 90 degrees = east.
    - For simplicity, quantize this is 45 deg. intervals intially.
 id - unique id for this vehicle
 vtype - what type of vehicle is this (redundant if vehicles types are
       subclassed but also can be useful to have this stored in baseclass)
 

