# CSCI 5611 Project 3: Optimization-Based Animation with Inverse Kinematics
Author: Daniel Chang (chan1975)

## Inverse Kinematics Scenario

Click [here](https://github.com/danielchang2002/5611_projects/tree/main/project3/IK_2D) for the code!

### Demo video

![img](https://raw.githubusercontent.com/danielchang2002/5611_PDE/main/cloth.png)
Click [here](https://www.youtube.com/watch?v=FkDdmKzh4CU&ab_channel=DanielChang) to watch the demo video!

### Features
-

### Technologies used:
- Processing (Java)
- Used google images to find textures

### Difficulties encountered
- It was difficult to use CCD in 3D. Due to time constraints, I resorted to creating a 2D simulation
- It was difficult to get re-rooting IK to work. 
I implemented this by treating the left and right leg, along with the hip, of mike wazowski as one single limb. 
To get lateral motion, I iteratively swapped the root end of the leg limb.