# Flame Tracker
The Flame Tracker is a video processing application designed for the combustion research community. With its Graphical User Interface (GUI), it is possible to edit a video and track a flame or a bright object on a frame by frame basis. Flame characteristics such as position, spread rate, length and area can be obtained by isolating a flame from its background with different methods.

The Flame Tracker is open source and cross platform; however, the MacOS and Windows versions are different. The 'script' folder contains both versions. Windows user have the additional option to donwload the latest release of the Flame Tracker and run the executable without the need to download the scripts (see...).

Author: Luca Carmignani, PhD

Contact: flameTrackerContact@gmail.com

Copyright (C) 2020,2021  Luca Carmignani

# Before you start:
Based on your operating system, download the appropriate script folder (flameTracker_Win or flameTracker_Mac). Each folder contains five python files, and flameTracker.py is the main one containing the GUI structure.
The Flame Tracker was written in Python 3.6+ (https://www.python.org), and the packages required to run the code are (they can be installed with pip):
- Pyqt5 (https://pypi.org/project/PyQt5/)
- openCV (https://opencv.org)
- numPy (https://numpy.org)
- PyQtgraph (http://www.pyqtgraph.org)

One of the source codes related to the legend visualization in the last package (PyQtgraph) has been modified. The version used by the Flame Tracker is in combustionTools/flameTracker/scripts/other. You should replace the original LegendItem.py file in the package folder pyqtgraph/graphicsItems/legendItems.py.

# Run the code:
At this point, you should be able to run flameTracker.py using terminal (Mac users), console (Windows users).

# Code overview
As mentioned before, the Flame Tracker folder contains five python files: flameTracker.py, manualTracking.py, lumaTracking.py, colorTracking.py, and templateAddition.py. The Flame Tracker is conceptually divided in two categories: video editing and video analysis; the scripts and the GUI follow this conceptual scheme.
The file flameTracker.py (the only one launched by the user), creates the GUI and controls the video editing, while manualTracking.py, lumaTracking.py, and colorTracking.py represent alternative methods to be used for the video analysis.

- flameTracker.py
This is the main code to run Flame Tracker and/or modify the GUI. Only the main functions related to the "preview Box" in the GUI are written in
this file. This code should be modified only if necessary.

- manualTracking.py
This script is used to track an object "manually" based on mouse clicks from the user. The number of clicks per frame is specified by the user; after clicking on 'Start tracking' the frames in the selected range will show in a new window and the click positions on each frame are recorded by the Flame Tracker.

- lumaTracking.py
This script is used to track a flame based on the luma intensity value of each pixel. Once the video parameters are set, the tracking does not require any further user input. Each frame is transformed from the RGB to the YCC color space; only the Y component is considered, and by choosing an appropriate threshold the flame can be isolated from the background. It is possible to filter out undesired particles and small objects according to their size (value specified by the user with
'filterParticleSldr_LT'), and then the flame edges are calculated. The value of average pixels is used to adjust the edge locations (1 pixel will
give the maximum or minimum location of the flame). The flame characteristics (length, area, ...) are calculated from the binary image obtained from the Y channel and the filtering. For the spread rate calculations, the moving average value is specified by the user.

- colorTracking.py
This script is used to track a flame based on color regions specified by the user. This method is automatic in the sense that once the video parameters are set, the tracking does not require any further user input. Minimum and maximum values for each RGB channels are chosen by the user; noisy particles or small objects are filtered out by the user with the slider 'filterParticleSldr_CT'. The left label of the GUI in the "Analysis box" shows the regions identified by the color filtering, while the binary image in the right label shows the regions considered according to the user input. From the binary flames, all the information (position, length, area, ...) can be calculated. Regarding the spread rate calculations, the moving average value is specified by the user.

- templateAddition.py
This script is a template to add a new analysis method to the Flame Tracker. There are comments step by step, but feel free to contact me for any questions. There are some functions, such as the perspective corrections, that should be recalled in each file (i.e. see 'perspectiveCorrectionCT' in colorTracking.py). A help button (and relative explanation) should be included in any new method.

# Add methods to the Flame Tracker:
To add an analysis (I recommend to start from templateAddition.py):
1) create a new selection in self.analysisSelectionBox in flameTracker.py and add the import line at the beginning of the file
2) in the self.analysisSelectionBox function, add the connection to your new file and create the new analysis box (check size with other recent files such as colorTracking.py)
3) the buttons in the new file will need their methods declared in flameTracker.py. There is an assigned method block for each analysis at the end of the class "Window".
4) The perspective correction function needs to be copied in each file (changing name accordingly)

# Additional information
A publication with a detailed explanation of objectives and capabilities of the Flame Tracker is under preparation for the SoftwareX journal.

For issues with the code and/or the analysis, please attach screenshots or other useful information related to you problem with your question at: flameTrackerContact@gmail.com.

# License:
Flame Tracker is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

Flame Tracker is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
