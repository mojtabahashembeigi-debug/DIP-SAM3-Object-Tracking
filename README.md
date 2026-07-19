Video Object Tracking with SAM 3 and Spatial Moments Analysis

This repository contains the implementation of the final project for the Digital Image Processing (DIP) course. In this project, Meta's state-of-the-art SAM 3 (Segment Anything Model 3) foundation model is utilized for zero-shot, intelligent video object segmentation. Following the AI segmentation, classical image processing techniques—specifically the calculation of Spatial Image Moments—are applied to extract, analyze, and visualize the object's flight trajectory.
Key Features
•	Text-Prompt Tracking: Automatic object detection and segmentation in a video using only a text prompt ("eagle").
•	Monkey Patching (Gated Repo Bypass): Utilizing request redirection techniques to download model weights from public mirrors, eliminating the need for a HuggingFace authentication token.
•	Geometric Analysis with OpenCV: Calculating the area (M00) and the centroid coordinates (CX, CY) using zero and first-order spatial image moments.
•	Visual Rendering (Alpha Blending): Seamlessly blending the AI-generated binary masks with the original video frames, drawing dynamic Bounding Boxes, and rendering a continuous flight path line.
•	Data Visualization: Generating a scientific 2D scatter plot of the eagle's flight trajectory, featuring a time-based colormap to indicate progression.
Prerequisites and Setup
This code is highly optimized to run in the Google Colab environment. To execute the project successfully, please follow these exact steps:
1.	Log into your Google account (Google Drive).
2.	Create a folder named exactly DIP_FinalProject in the root directory of your Google Drive (My Drive).
3.	Upload your input video and name it Eagle.mp4 inside this folder.
4.	Open the provided Notebook (.ipynb) in Google Colab.
5.	From the top menu, go to Runtime > Change runtime type, and set the Hardware accelerator to T4 GPU.
Execution Guide
The codebase is divided into 4 main sections that should be executed sequentially in Colab cells:
Part 1: Environment Setup & Drive Mount
Executing this section connects Google Colab to your Google Drive (drive.mount) and verifies the existence of the required folder and the Eagle.mp4 input video.
Part 2: Installation & Downloading SAM 3 Weights
In this step, the official SAM 3 repository is cloned, and necessary libraries (opencv-python, torch, matplotlib) are installed. Furthermore, the heavy model checkpoint (sam3.pt) is rapidly downloaded using the aria2 download utility.
Part 3: Video Tracking & Output Generation
This is the core engine of the project:
•	Using the smart_hf_download monkey-patching trick, the script bypasses HuggingFace's gated repository restrictions for config files.
•	The SAM 3 model is initialized. By passing the "eagle" text prompt, the model extracts the object's mask across all video frames.
•	The extract_binary_mask function converts the raw nested tensor outputs into standard binary images (uint8).
•	Using cv2.moments, the script calculates the centroid for each frame, draws bounding boxes and trajectories, and writes the final processed frames into a new video file.
Part 4: Trajectory Plotting
In the final step, the extracted centroid coordinates are plotted as a 2D Scatter Plot. Theoretical Note: In this plot, the Y-axis is intentionally inverted using plt.gca().invert_yaxis(). This is done to perfectly match the standard digital image coordinate system, where the origin $(0,0)$ is located at the top-left corner.
Project Outputs
After fully executing the notebook, the following output files will be generated and saved directly into your DIP_FinalProject folder in Google Drive:
1.	Eagle_tracked.mp4: The final rendered video featuring a semi-transparent colored mask, a dynamic bounding box, and the yellow trajectory line.
2.	Eagle_Trajectory_Plot.png: A scientific 2D plot of the flight path, with color-coded points representing the frame number (time elapsed).
This repository was created as the final project for the Digital Image Processing course.

