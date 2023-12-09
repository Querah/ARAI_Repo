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
Or you can download the reduced data via https://drive.google.com/file/d/1b4sGfCyNIqzJSGJPBm3lKiRMF3eqppxS/view?usp=sharing

## 2. Train
set the dataset path in TCP/config.py file and
```
python TCP/train.py --gpus NUM_OF_GPUS
```

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
From now, you should do several things to get the result.
First change self.alpha into 0 in leaderboard/team_code/tcp_agent.py. And if you want PID controller only, make self.status==1 while multi-step controller only at status==0.
You should change the weather. Go to the line 254 of the leaderboard/leaderboard/leaderboard_evaluator.py file.
```
  if args.weather != "none":
    assert args.weather in WEATHERS
    CarlaDataProvider.set_weather(WEATHERS[args.weather])
```
And change above code into under code. Notice that you should choose either first line or second line.
```
  w = carla.WeatherParameters(precipitation=100.0, precipitation_deposits=70.0, sun_altitude_angle=50.0, fog_density = 50.0, wetness=50.0) # when hard rain situation
  w = carla.WeatherParameters(sun_altitude_angle=-30.0, fog_density = 50.0) # when night situation
  CarlaDataProvider.set_weather(w)
```
 Then launch the carla sever
```
cd CARLA_ROOT
./CarlaUE4.sh --world-port=2000 -opengl
```
and start evaluation.
```
sh leaderboard/scripts/run_evaluation.sh
```
Don't forget you should rearrange the leaderboard/scripts/run_evaulation.py file according to your environment.

