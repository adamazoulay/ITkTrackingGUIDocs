Modules and Code
================

This sections gives a rundown of the basic functionality of all modules in the source code. More details can be found
in the comments of the code. An explanation of the algorithmic flow and the data structures can be found in the
`Structures and Flow`_ section of the documentation.

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
A recursive helper function for colour_selection_tree_. Takes all elements of the tree view and puts them into one array.

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
This is the widget for accepting the configuration information and saving it to the parent dictionary. All we do at the
start is connect the save and close buttons to save the data or close the window respectively.

save_config
```````````
Set each of the config values and close the window once save is clicked.


lib\\selection_edit_widget
--------------------------
This module contains the code for the selection of components with the edit widget. We initialize it the same way we
initialize the main GUI window, but setting the global variables and connecting the buttons on the GUI to functions
within the class.

comment_double_click
````````````````````
This function checks if the user has double clicked the comments column (column 2). If they have, it sets the column
as editable and allows the user to input a comment which is then saved in the main window cur_selected array.

save_comments
`````````````
This is a convenience function (maybe redundant, needs to be checked). It loops through all the items in the cur_selected
list and saves all the comments to the parent dictionary.

eventFilter
```````````
This event filter allows us to trigger when focus is lost from the edit window. For example, when the user fills in a
comment and then clicks the main window, we want the edit window to save all the comments so they are not lost. More
features can be added here in the future if needed.

add_custom_component
````````````````````
The user can trigger this by clicking the 'Add custom' button. It sets the name for the custom component and creates
a blank board item, adding it to the parent dictionary and setting custom mode to true.

The rest of the functionality comes from the eventFilter in `lib\\issue_tracking_gui.py`_.

add_selected_components
```````````````````````
Here we loop through all the components that are currently highlighted on the list, and add them to the selected list.
We then place the board item for all selected components into the cur_selected dictionary in the main window.

We then reload the list and the image (to have correct box colours and selection tree colours).

remove_selected_components
``````````````````````````
We loop through all the selected items and remove them from the parent cur_selected dictionary if they are already in it.
If they are not, we do nothing. We also make sure to wipe the comment field (strange behaviour if we do not do this).

We then reload the list and the image (to have correct box colours and selection tree colours).

build_edit_coords
`````````````````
Checks the coordinates of the main window and then positions itself on the right side of the window, scaled to its width
and with the same height.

load_list
`````````
This function refreshes the elementTree and the selectedTree which list the components available for selection and the
currently selected components. First we check some load cases for repeated lists (like the ASICs) and then we check to
see if there already exists a selection on this component.

We then grab the dictionary for the selected component and populate the elementTree and the selectedTree rows with
all the components available.

Finally we reset the selected items dictionary (for the next loading in case of the dictionary not existing).


lib\\selection_areas
--------------------

This module stores the class BoardItem which is used to store the information about each predefined area on the components.
A BoardItem contains:

- name (str)
- description (str)
- signal (str)
- direction (str)
- pad_type (str)
- coords [on the template image] (list)
- comments (str)

After the class definition comes all the components stored inside of dictionaries. Each item in the dictionary
corresponds to one location on the component it is named after. See `Structures and Flow`_ for more details.

.. _`Structures and Flow`: flow.html
