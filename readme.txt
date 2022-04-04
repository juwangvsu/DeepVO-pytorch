repo:
	hptitan Documents/DeepVO-python
	juwangvsu github

-----------12/20/21 prepare some pc2 and odom data  ----------------
from turtlebot3 simulation bag file
turtlebot3_imuodompt2_3/
	.pcd  --- point cloud (binary)
	.ply  --- ply format for point cloud (meshlab readable)
	.yaml --- pose information corresponding to each ply

-----------10/20/21 train and test work ----------------
train:
	python main.py
test:
	python test.py
	load model params from :  models/
delete datainfo/* when train or run new data set to avoid shape mismatch

visualize:
	python visualize.py
	edit video_list in py file
	eog result/route_05_gradient.png

------------10/12/21 first test ----------------
dataset download:
	ln -sn ../KITTI (or mkdir KITTI)
	./download.sh
		this take a long time
		or download xx.zip from synology
		unzip to KITTI/images/
		to run test.py, 04.zip is enough
		
dataset gt:
mkdir KITTI/pose_GT
cd KITTI/pose_GT/
unzip ~/Documents/DeepVO-pytorch/data_odometry_poses.zip
cp dataset/poses/* .
unzip ~/Documents/DeepVO-pytorch/data_odom_npy.zip

download trained model 
	or from synology, put in models/

test.py gpu req:
	batch_size=8 work on newpcamd (use about 7gb)
	batch_size=16, work on hptitan, not on newpcamd

----- additional modification done: -----------------------
modify params.py:
	data folder

python preprocess.py:

request pretrained weight for CNN part

self.pretrained_flownet = None

trained model and python main.py
	https://drive.google.com/file/d/1l0s3rYWgN8bL0Fyofee8IhN-0knxJF22/view
	mv t000102050809_v04060710_im184x608_s5x7_b8_rnn1000_optAdagrad_lr0.0005.model.train models/
	cannot reshape array of size 0 into shape (3,3)



	
