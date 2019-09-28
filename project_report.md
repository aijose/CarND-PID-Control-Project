# **PID Controller**

---

## Objectives

The goals / steps of this project are the following:
* Design a PID controller to steer a vehicle along a track
* The PID controller takes the cross track error (CTE) at each time-step as input and computes the steering angle
* Write a report summarizing the approach used to tune the hyper-parameters

## Rubric Points
### This section will describe how the each of the [rubric points](https://review.udacity.com/#!/rubrics/1971/view) were addressed in this project.  

---

### Compilation: Your code should compile

The code compiles successfully. No additional code files were created.

### Implementation - the PID procedure follows what was taught in the lessons

The PID object is initialized with the optimized values of coefficients (Kp,
Ki, Kd).  At each time-step the cross track error (CTE) provided by the
simulator is used to update the the proportional, integral and differential
errors. The control function (steering value) is computed by multiplying the
PID coefficients with the corresponding errors. The steering angle is then bounded
by the limits of the steering angle (i.e., [-1,1]) and provided to the
simulator. At each time-step the total error is computed as the cumulative mean
square error for debugging and performance evaluation.

### Reflection

#### Describe the effect each of the P, I, D components had in your implementation.

The P parameter enabled the car to quickly correct its trajectory when it
deviated away from the center of the track. At low values of P, the car does not
correct itself quickly enough, especially at sharp turns. However, higher values
of P can lead to higher amplitude of oscillations in the car's trajectory.

The I parameter was critical in reducing the oscillations. If the value of I is
too small, the car had more pronounced oscillations in its path. If the value
of I is too high, the car was observed to have very rapid positive-negative (zig-zag)
steering values which slowed down the vehicle and would lead to poor driving
experience. Sudden overshoots in the vehicle trajectory were also observed for
high values of the I parameter.

The effect of the D parameter was relatively less obvious. High values of the D
parameter lead to oscillations followed by divergence of the car's path.
However, even setting the lowest value of zero for the D parameter did not cause
failure as long as the values of the P and I parameters were reasonable. This
seems to indicate that for this problem, the D parameter is not as critical as
the P and I parameters.

#### Describe how the final hyperparameters were chosen.

Initial iterations with the P, I, D parameters lead to divergence in the path
of the car. It was found that reducing the throttle from the default 0.3 to 0.1,
reduced the likelihood of divergence and provided a better environment for
playing around with the PID parameters. In the reduced throttle setting, the
PID parameters were adjusted manually using an approach similar to the twiddle
approach. In order to evaluate the quality of a trajectory, the CTE error was
noted at four key points in the track with distinct landmarks. A better
trajectory may be expected to have a lower cumulative error at the landmarks
and particularly at the final landmark which contains all the accumulated
errors.

Only one parameter was changed at a time and multiple values were
explored until no noticeable improvement was observed. Then another
parameter was chosen and multiple values were explored until no significant
performance improvement was observed. The process was repeated until the car
completed the track in a reasonable fashion.

Once good parameters were found for a throttle setting of 0.1, the throttle was
increased to the original (higher) value of 0.3. The parameters were further refined at
the higher throttle setting using the manual iterative approach outlined above.
One way to minimize large deviations in the trajectory was to reduce the
throttle when the steering values were high. This led to a better behavior of
the car.  The final values for each of the PID parameters was P=0.25, I=1.5, D=0.0001.

### Simulation - the vehicle must successfully drive a lap around the track.

The car successfully completed the track at a good speed (throttle was
approximately in the range 0.2-0.3 depending on steering angle). The video
below shows the car completing one lap around the track.

[![IMAGE ALT TEXT HERE](youtube.png)](https://youtu.be/xDrND-zHOIw)
