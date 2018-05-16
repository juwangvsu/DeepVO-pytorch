# Readme
## Usage
- Run 'KITTI/downloader.sh' to download the KITTI visual odometry dataset and only keep the left camera color images (image_03 folder.)
- Run 'preprocess.py' to 
    - remove unused images based on the readme file in KITTI devkit.
    - transform ground truth poses in KITTI (12 floats [R|t]) into 6 floats (euler angle + translation)
    - and save the transformed ground truth pose into .npz