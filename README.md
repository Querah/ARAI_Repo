# ARAI_Repo
My advanced robotic AI project is highly affected by https://github.com/OpenDriveLab/TCP.
So if you want to get more information, you can go to link above. 
## 0. Setup
git clone TCP and download CARLA
```
git clone https://github.com/OpenDriveLab/TCP.git
cd TCP
mkdir carla
cd carla
wget https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/CARLA_0.9.10.1.tar.gz
wget https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/AdditionalMaps_0.9.10.1.tar.gz
tar -xf CARLA_0.9.10.1.tar.gz
tar -xf AdditionalMaps_0.9.10.1.tar.gz
rm CARLA_0.9.10.1.tar.gz
rm AdditionalMaps_0.9.10.1.tar.gz
```
build the conda environment
```
cd TCP
conda env create -f environment.yml --name TCP
conda activate TCP
```
## 1. Dataset
You can get dataset(115G) at here.
https://drive.google.com/file/d/1HZxlSZ_wUVWkNTWMXXcSQxtYdT7GogSm/view
If there any problem, download via TCP repo. 

## 2. Train
set the dataset path in TCP/config.py file and
```
python TCP/train.py --gpus NUM_OF_GPUS

## 3. Data generation
launch the carla sever
```
cd CARLA_ROOT
./CarlaUE4.sh --world-port=2000 -opengl
```
and collect data
```
sh leaderboard/scripts/data_collection.sh
```
Before run this code, you have to modify leaderboard/leaderboard/leaderbaord_evaluator.py according to your environment.
Also, you should change "PATH_TO_CARLA", the first line of leaderboard/scripts/data_collection.sh file, into "carla".

## 4. Evaluate
