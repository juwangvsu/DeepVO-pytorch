repo:
	hptitan Documents/DeepVO-python
	juwangvsu github

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
cd /media/student/code12/DeepVO-pytorch/KITTI/pose_GT
unzip pose_GT/data_odometry_poses.zip
cp dataset/poses/* .

modify params.py:
	data folder

python preprocess.py:

request pretrained weight for CNN part

self.pretrained_flownet = None

download trained model and python main.py
	cannot reshape array of size 0 into shape (3,3)



	
