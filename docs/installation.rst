============
Installation
============

There are three steps for the installation of the ITG:

1. Copy the source code to your computer
2. Install Python 3.6 and pip
3. Install the dependencies required for the code to run


1. Downloading the source code
------------------------------
You can `Download and extract`_ the source code manually or you can `Clone the repo`_ from GitLab. Downloading
and extracting will allow you to quickly get up and running but will force you to repeat the process for future updates.
Cloning the repo will allow you to download future updates directly to your computer by running a single command in git.

Download and extract
~~~~~~~~~~~~~~~~~~~~
To download an archive of the latest stable version, navigate to the GitLab page for the `ITk Tracking GUI`__
and click on the |download| button, and select the archive type you wish to download (.zip is usually fine for
most systems).

Once you have the archive downloaded to your computer, extract it to the location you would like to store the program.


Clone the repo
~~~~~~~~~~~~~~
To clone the repo from gitlab, you must have git installed on your computer. You can clone the repo using the URL of the
project which is located on the readme page.


2. Install Python 3.6 and pip
-----------------------------
**For windows and MacOS**, navigate to the `Python 3.6 download page`_ and scroll to the bottom. There will be a list of installers. Click
the one for your operating system, and install it once the download is complete.

*During installation, make sure the* ``Add Python 3.6 to PATH`` *option is selected.*

**For linux**, Python 3 should already be installed on your system. If it is not, you can install it by running the
package installer with the option ``python3``. For example, ``sudo apt-get install python3``.

3. Install the dependencies
---------------------------
Once the Python installation is finished, we need to install the dependencies required for the program to run.
Open up a command window in the root directory where you extracted the code (there should be a file called
``requirements.txt`` located there).

Once the window is open, run the following command:

.. code-block:: python

    pip3 install -r requirements.txt

The updates should download without error. Once this is complete the setup is finished.





.. _ITkTrackingGUI: https://gitlab.cern.ch/aazoulay/ITkTrackingGUI

.. |download| image:: img/download.png
    :align: middle

__ ITkTrackingGUI_

.. _`Python 3.6 download page`: https://www.python.org/downloads/release/python-365/


