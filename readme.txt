repo:
	hptitan Documents/DeepVO-python
	juwangvsu github

-----------4/12/22 main.py gt label-------------------------

dataloader return item format:
	t_x: b,seq,c,w,h (8,7,3,608, 184)
	t_y: b,seq, labelsize (8,7,6)
model.py DeepVO:
	input shape (8,7,3,608, 184)
	t_x image is stacked to become (8,6,6,608,184)
	further change view to (8*6,6,608,184)
	this is passed to CNN, result feature tensor ([48, 1024, 10, 3])
	change view to ((8,6, 30720)
	send to RNN
	final result (batch_size 8, seq_len 8, 6)

the model actually predict the relative pose between the two stacked frame. so
this definetly will cause drift as trajectory of a long video will accumulate.
without loop closure, no way to get a good result.
	
	
-----------4/5/22 test.py gt label-------------------------
output: results/*.txt
	each line pose estimate for the video seq?
		euler angle y,x,z, pos x, y, z

label:  04.txt: each line 12 numbers, is the pose, representing 3x4 matrix.
	the position is the last column (3x1). corresponding to the 3th, 7th,
		11th number iin the txt file, the rest are 3x3 rot matrix.
	
	npy format: converted from .txt file
		[0:15] for each pose
		euler angle y,x,z, pos x, y, z, 3x3 rot matrix
	gt[0:3] angle, [3:6] translation

seq_len = 6,  overlap = 5
Folder 04 finish in 0.0029706954956054688 sec
len(answer):  271
expect len:  271
Predict use 31.668784141540527 sec
Loss =  243.41754709869468


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



	
