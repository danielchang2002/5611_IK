# CSCI 5611 Project 3: Optimization-Based Animation with Inverse Kinematics
Author: Daniel Chang (chan1975)

## Inverse Kinematics Scenario

Click [here](https://github.com/danielchang2002/5611_projects/tree/main/project3/IK_2D) for the code!

### Demo video

![img](https://raw.githubusercontent.com/danielchang2002/5611_IK/main/mike.png)
Click [here](https://youtu.be/gtZkAkhACsc) to watch the demo video!

### Features
- 2D multi-arm inverse kinematic scenario. 
  - Two arm end effectors reach to touch an object
  - Implemented with cyclic coordinate descent
- Natural joint limits
  - Angle and rotational speed limits
- 2D Re-rooting inverse kinematics 
  - Mikey Wazowski is able to walk by rooting one foot, swinging the other foot in the direction of movement via IK, and repeating with the other foot
  - The rooted foot is colored pink to clearly demonstrate the re-rooting implementation
- User interaction
  - Users can control the location that the arm end effectors reach by using their mouse
  - Users can control the lateral direction of movement (re-rooting IK) of mikey wazowski via A/D on the keyboard
  - Users can left click the mouse to pick up sully when in range in order to make him go to work scaring kids
- Alternative IK Solver
  - I used basic random search as a second inverse kinematics solving technique
  - i.e., for each solve call, I tested random sets of angles for the joint set and kept the angle set that minimizd the distance between the end effector and the goal.
  - IK was a lot simpler to implement.
The only downside is that it is quite time intensive.
The smoothness of the animation heavily depends on the number of random joint set iterations that you test (shown near the end of the video)
I had to play around with the smoothing parameters (like joint angle acceleration cap) 
  - Random search is flexible, as it has no limitations in the spaces in the angle set search space it can explore. Obviously, how comprehensive the search is depends on the iteration count again.
  - Both methods support constraints well, as you can easily clamp angle values to predetermined limits.


### Technologies used:
- Processing (Java)
- Used google images to find textures

### Difficulties encountered
- It was difficult to use CCD in 3D.
Quaternions or rotation matrices were required.
I tried to use the trick of rotating only in the plane created by the node-to-goal and node-to-end-effector vectors, but it was a lot of book keeping code.
Due to time constraints, I resorted to creating a 2D simulation

- It was difficult to get re-rooting IK to work. 
I implemented this by treating the left and right leg, along with the hip, of mike wazowski as one single limb. 
To get lateral motion, I rooted one foot, assigned the other foot as the end effector, and gave the other foot a goal that was a few pixels above the ground and to the right/left.
Once the end effector foot reached that goal, it was then assigned another goal that was a few pixels to the right again, but this time on the ground.
Then, the end effectors and root feet were swapped
  - It was difficult to swap the root/end effectors.
  This required swapping the values in the length/points arrays.
  Moreover, the angles had to be recomputed, as they were angles that were relative to the last limb.
- Another issue regarding the re-rooting was that I had to manually adjust the joint angles of the legs. Even though the solver was following the joint angle constraints, mikey would eventually go into a weird sumo squat every time he would get a few steps into his walk. 
I solved this by setting an "angle decay" on the leg that had the root foot, so that it would straighten out while the next leg made its step.

- There were no real issues related to getting basic random search working, as the implementation is simple.
However, it is a bit trickier to get the animation to be smooth. 
I had to play around with the smoothing parameters (like joint angle acceleration cap) 
In the end, it still looked jittery