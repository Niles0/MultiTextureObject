/*
 * Author: Selin Nur Özsert
 * Description: Generates multi-texture haptic objects from MATLAB CSV data for WEART integration.
 */

Unity WEART Haptic Data Visualizer

This project translates exported volumetric CSV data into an interactive, 3D haptic object in Unity.

Features

UI-Driven Data Loading: Dynamically reads available CSV files from the StreamingAssets folder via a dropdown menu.

Dynamic Grid Generation: Parses spatial coordinates (x_unity, y_unity, z_unity) and groups them into a customizable 3D grid of touchable objects.

Haptic Mapping:

Stiffness: Mapped based on the depth/physical Y-axis (y_unity).

Temperature: Mapped based on inclusion type (0.7 for 3mm inclusions, 0.3 for 1mm inclusions and baseline volume).

Texture: Mapped dynamically to distinct characters/letters extracted from the data (source_type).

Mouse Haptic Testing: Includes a testing probe to feel haptic responses using standard mouse input (click & drag or hover), bypassing the immediate need for a VR headset/hand tracking.

Prerequisites

Unity (Tested with WEART SDK compatible versions).

WEART SDK imported into your Unity project.

TextMeshPro (for UI components).

Folder Setup

For the UI to successfully detect your data, you must place your exported CSV files into the following directory:
Assets/StreamingAssets/Data

(Note: If the StreamingAssets or Data folders do not exist, create them exactly as spelled).

Core Scripts Overview

1. GenerateMultiTextureObject.cs

The main engine of the project. It handles:

Scanning the StreamingAssets/Data folder and populating the UI dropdown.

Parsing the selected CSV file for coordinates, source names, and source types.

Calculating the physical bounds and sorting the points into an averaged 3D grid.

Instantiating the physical cube and applying the computed temperature, stiffness, and texture values to each grid chunk.

2. TextureObject.cs

A lightweight component attached to the instantiated grid prefabs. It acts as a bridge, receiving the computed float values from the generator and passing them directly to the WEART hardware via the WeArtTouchableObject component.

3. MouseTouchProbe.cs

A developer testing tool. Attach this to an empty GameObject along with a WeArtHapticObject. It casts a ray from the camera to your mouse cursor. When you click and hold over the generated haptic grid, it simulates physical contact, sending the specific texture, temperature, and stiffness data of that grid cell to your WEART device.

How to Use

Place your CSV data files into Assets/StreamingAssets/Data.

Enter Play Mode in Unity.

Use the Dropdown UI to select the data file you want to visualize.

Click the Generate button. The script will clear any old generation and build a new 3D grid.

Use the Mouse Touch Probe to touch the generated cube. Haptic feedback is generated on the WEART thibmle based on the interaction in the Unity scene.

## Developers
**Selin Nur Özsert** 
contact: selinnozsert@gmail.com
**Ahmed Davud Duran** 
contact: adavudduran@gmail.com
