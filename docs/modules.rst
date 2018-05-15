Modules and Code
================

main.py
-------
This is the main python file, it initiates the PyQt application, builds the main window and edit window forms, sets the
correct coordinates, and then executes the app. Most of the meat of the code is stored in the other files, this one is
mostly for organization.

issue_tracking_gui.py
---------------------
All the code for the GUI is contained within the IssueTrackingGUI class. The class inherits from the PyQt class
``QMainWindow`` which is the central widget for our program.

\__init__
``````````
First the .ui file for the GUI is loaded, and then we initialize all global variables to fill in later as needed. This
prevents errors for undefined variables.

Next the action of the File and Help menu items is defined. They are all given a shortcut and linked with a function
inside of the class which executes the action. We also connect the ``load_img`` function to a change in the tree
so that the image is refreshed when we select a new component.