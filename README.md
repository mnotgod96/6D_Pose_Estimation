# 6D_Pose_Estimation
ECE 549/CS 543 Final Project

# Setting up your environment
If you've never used the cluster before, this part will help you get all of the packages that we are using. 

## .bashrc (Run once)
The following code will load various software that you'll likely need into your environment for every time you ssh into the cluster.
```
echo $'module load anaconda/3\nmodule load cuda/10.0\nmodule load python/3\nmodule load texlive/2019\nmodule load curl/7.61.0\nmodule load git/2.19.0' >> ~/.bashrc
```
After doing this, run the following to properly configure anaconda
```
echo ". /usr/local/anaconda/5.2.0/python3/etc/profile.d/conda.sh" >> ~/.bashrc
```
Next, I have had issues where I'd run out of memory in the home directory while using anaconda. Therefore I created a softlink to the scratch directory so that way there would be no memory issues
```
mkdir ~/scratch/conda
ln -s ~/scratch/conda .conda
```
Finally, if you'd like anaconda to run on start up, run the following
```
echo "conda activate" >> ~/.bashrc
```
If you think there are other pieces of software you'd like, try running
```
module avail
```
to see what is available. Modules can be installed for your current session by 
```
module load {Software Name}
```
and modules can be permenantly added by adding the previous line to your .bashrc file as follows
```
echo $'module load {Software Name}' >> ~/.bashrc
```
## Python
Anaconda will be used to manage python packages to ensure everyone is using the same software. Please edit the file "requirements.txt" as needed. 

To create an anaconda environment
```
conda create --name cv python=3.6
```

To activate an anaconda environment
```
conda activate cv
```

To update your anaconda environment with changes to the requirements.txt run
```
conda install --file requirements.txt
```
I had issues getting pip to work so some python packages may have to be downloaded more manually. For example torch can be installed with
```
conda install pytorch torchivsion -c pytorch
```


# Getting the Code
Clone this repo with 
```
git clone --recurse-submodules -j8 git@github.com:Jbwasse2/6D_Pose_Estimation.git
```
or 
```
git clone --recurse-submodules -j8 https://github.com/Jbwasse2/6D_Pose_Estimation.git
```
depending on whether you have ssh key set up and linked with github (Which I highly recommend doing so that way you don't have to keep entering in your username and password when you pull/push. See [this link](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) for more info.

# Data
The data for this project is kept in my scratch directory. I have created a soft link to this directory in the repository (the soft link is named data). I have changed the permissions of this directory so anyone can change it. To access this data simply do 'cd data'. I will write a script to back up the data every night, just in case something happens. This backup will only be available to me.

Trained models should not be pushed to github as this makes pushing/pulling a pain. Trained models should be left in the 'final_proj/models' in the scratch directory.
