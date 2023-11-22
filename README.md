# ARAI_Repo
My advanced robotic AI project is highly affected by https://github.com/OpenDriveLab/TCP.
So if you want to get more information, you can go to link above. 
## 0. Installation
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
