# Setting up ISA Stuff #

## Editing the model ##
The __best__ thing to do to edit the model would be with Blender.

# __IMPORTANT!!!__ #
When seperating the glass and the gazebo model, seperate the glass, copy the new object in a new file and export that.
Then go back to the building model before the glass has been seperated and delete the glass faces.
This will cause there to be an "invisible" floor which __will cause CHAOS__

If floating robot/invisible wall showing on Lider, send a message as it is a complete nightmare!

# Glass and Gazebo # 
Glass from Blender __won't__ be transfered to Gazebo.
Steps to overcome this: 
1. Open up blender
2. Select the model and go into Edit mode (Tab)
3. Select all the faces where there is glass in the model
4. Seperate them by pressing __P__ and seperate them by ....
5. Copy the glass object into a new file where you can [export](# Exporting-model) the model



## Exporting model ##

1. Go to file -> export -> collada
2. Choose where you want the file (in the same folder as your textures)
