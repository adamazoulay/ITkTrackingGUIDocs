Modules and Code
================

main.py
-------
This is the main python file, it initiates the PyQt application, builds the main window and edit window forms, sets the
correct coordinates, and then executes the app. Most of the meat of the code is stored in the other files, this one is
mostly for organization.

lib\\issue_tracking_gui.py
--------------------------
All the code for the GUI is contained within the IssueTrackingGUI class. The class inherits from the PyQt class
``QMainWindow`` which is the central widget for our program.

\__init__
``````````
First the .ui file for the GUI is loaded, and then we initialize all global variables to fill in later as needed. This
prevents errors for undefined variables.

Next the action of the File and Help menu items is defined. They are all given a shortcut and linked with a function
inside of the class which executes the action. We also connect the ``load_img`` function to a change in the tree
so that the image is refreshed when we select a new component.

We install an eventFilter on the selectionView (where we display the images) so we can capture clicks and
button presses.

Finally, we load up the selection_edit window to be displayed beside the main window.

open_help
`````````
Opens a web page to the documentation.

close_all
`````````
Closes the edit_widget, config_widget, and then shuts down the main window.

closeEvent
``````````
A function to override the PyQt closeEvent function, calls the close_all function and then passes back the event to PyQt.

colour_selection_tree
`````````````````````
This function is used when we load and image. It checks all saved markings and if the item in the tree is selected,
it will colour the item red so the user can easily identify which components are marked.

flatten_tree
````````````
A recursive helper fuction for colour_selection_tree_. Takes all elements of the tree view and puts them into one array.

save
````
Checks to make sure a location has been defined to save to, and then pickles all config and selection data into an array
and saves it to the save file.

save_as
```````
Define a save location and then run save_.

new
```
This will wipe all stored data by reinitializing the global variables, allowing the user to start selecting on a
new file.

eventFilter
```````````
This function controls all actions inside of the viewing window.

In the first case, we check for mouse wheel scrolling. We set this action to zoom in and out fon the current image.

The second case is for custom selection. If custom selection mode is active, then add all click positions to the
current item and then overwrite it in the cur_selected dictionary.

For the third case, if we right click which in custom selection mode, we end selection mode and
reload the list in the edit_widget.

Next we have the case for a normal left click. We get the click coordinates and then check if it is inside any predefined
areas in the cur_dict dictionary. If it is, we add it to the selected list if it is not already selected. Otherwise we
remove it from the selected list.

keyPressEvent
`````````````
Another overridden function from PyQt, this checks if we are holding the Ctrl key. If we are, we enable click and drag mode.
We also check if the R key was pressed, and if it was we reset the image to fit in the selection view.

keyReleaseEvent
```````````````
Similar to the previous function, once we release the Ctrl key we disable click and drag mode.

resizeEvent
```````````
Checks if the window is resized. If it is, we reload the image. This allows us to track the image zoom along with the
window size.

open
````
Opens an existing save file in the program. Loads both arrays from the save file into the correct variables in the program.

load_img
````````
This function takes the current image name and attempts to load an image with the corresponding name from the img folder.
There are cases where we use the same image for multiple locations, and we check for those cases here as well. The image
is then loaded to the scene and the boxes are drawn on top if we have the edit window open.

draw_boxes
``````````
This function is used in the load_img function. It checks the list of predefined areas and draws them if we are in a
matching location. It then checks the selected areas and draws boxes on top of the old one if it is selected.

build_window_coords
```````````````````
This function gets the total screen geometry and sets the program to be 9/14 of the width and 8/10 of the height.

selection_edit
``````````````
Here we open up the selection_edit widget and make sure to position it correctly. Then we refresh the image (for boxes).

config_edit
```````````
Open up the configuration window. Nothing special.

about
`````
Build and display the About window. Takes a message and image to disply, and then ususes the PyQt function QMessageBox
to display the result.



lib\\config_edit_widget
-----------------------

lib\\selection_edit_widget
--------------------------

lib\\selection_areas
--------------------

