# Deadlift Form Performance Tracker
Sports Performance Tracking: project for Spring 2022 CSE 598 Perception in Robotics

[Demo video](https://youtu.be/UMo1DXSu5yI)

Two Cameras are calibrated by taking several pictures of black and white checkerboard boxes. These calibrated cameras are then used to capture video of a person performing the deadlift from both a front and a side view. In real-time, the cameras provide a live feed to the program, which is formatted and handled by OpenCV.

MediaPipe, a 3D pose estimator, is used to extract two corresponding sets of landmarks for each instant in time. The landmarks are normalized for the position and orientation of the cameras, allowing for a weighted average of the two sets to increase accuracy and account for possible occlusions. Afterward, a set of heuristics are calculated with the corrected set of landmarks. These heuristics measure the performance of the deadlift and is then used to provide feedback.

Four heuristics are tracked, and they are as follows.
1. Width of the feet, to ensure they’re shoulder-width apart
2. Distance between the barbell and the user’s center of mass
3. Angle between the neck and spine
4. How parallel is the bar to the floor

The video streams, extracted landmarks, and heuristic values are then incorporated to create a visual feedback video stream for analysis. The feedback implements color-coded cues on whether the user is performing well or not. The aim is for the user to understand these metrics at a glance, without distracting them from their exercise. We tested the effectiveness of our approach by collecting two sets of deadlift demonstrations and having our application critique them. The first set contained approximately six deadlifts performed with ”good form,” while the second set consisted of a similar number of deadlifts performed with intentionally ”bad form.” In the second set, violations of form were both subtle and greatly exaggerated so as to assess our approach for robustness. These two sets can be viewed in the [Demo video here](https://youtu.be/UMo1DXSu5yI).

We achieved our original goal of providing feedback visually on each frame. Furthermore, the project proved to be versatile, as it can provide annotations regardless of camera positioning or the lifter's physical appearance. However, there are some shortcomings with our approach, chief of which, is landmark noise returned by MediaPipe. Some of the heuristics that we used are quite sensitive to even the mildest of perturbations and this became evident during evaluation. We noticed instances of our framework unjustly criticizing good techniques and failing to criticize intentionally poor techniques. The issue of noise in the data presents itself most obviously during sequences of frames where the heuristic indicators oscillate rapidly between "good" and "bad". This indicates the underlying heuristic value is close to the threshold, and despite little movement from the user, the noise prevents a definitive classification of their form.  
