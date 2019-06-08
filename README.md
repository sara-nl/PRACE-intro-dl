# PRACE course: Introduction to High-Performance Machine Learning (1st day)

For the first session in this course we will use the [Cartesius supercomputer](https://userinfo.surfsara.nl/systems/cartesius) hosted at SURFsara. You will need to connect to them through the ssh protocol (natively installed on Linux and Mac).

For Windows users, we recommend to connect via ssh using [MobaXterm](https://mobaxterm.mobatek.net/) or, on Windows 10, using the [native bash environment](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)

## Connect to Cartesius

To connect to Cartesius, please open a terminal and use the following command:

    ssh ptcXXX@cartesius.surfsara.nl

Here "ptcXXX" is the login name that you received via email. Type in the password you received together with your login name and press Enter (note that the cursor may not move while introducing the password, but the typing will succeed).

This access to Cartesius is made available for duration of the course and at most one week after its finalization.

## Preparation for the hands-on sessions

Login to Cartesius, clone the git repository and generate a key pair.

    ssh ptcXXX@cartesius.surfsara.nl
    git clone https://github.com/sara-nl/PRACE-intro-dl.git
    
    ssh-keygen -t rsa

Press Enter three times. A key pair will be generated for you in directory .ssh. Copy the contents of the public key to file authorized_keys:

    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys

## Submit a job to Cartesius

When the session starts, please submit the following job to Cartesius:

    cd PRACE-intro-dl
    sbatch job.jupyter.gpu

Open a new terminal and do the following:

    ssh -L5XXX:localhost:5XXX ptcXXX@vis.cartesius.surfsara.nl

Note that you need to replace every "XXX" with the three digits of your login name.
   
Use this command to check your job:

   squeue –u $(whoami)
   
To cancel your job:

   scancel JobID
   
If your job is running, you can open your browser and go to localhost:5XXX (replace again XXX with the three digits of your login name). You should be able to see the Jupyter notebook now.

NOTE: the script job.jupyter.gpu includes a line with the reservation "ptc_course_1", which is valid only for the first day of the course. The script may be used later, but this reservation won't be valid anymore, and therefore will need to be changed or removed.

## Running the notebooks at home

To run the notebooks locally, please install [Anaconda](https://www.anaconda.com/distribution/).

Create a new Python 3 environment and install the following packages:
- `scikit-learn`
- `scikit-image`
- `numpy`
- `scipy`
- `pandas`
- `matplotlib`
- `seaborn`
- `keras`
- `keras-vis` installed from Github instead of Anaconda/PyPy.
- `tqdm`
- `jupyter`

Navigate to this directory and tart a Jupyer notebook in your environment using the cli:

```
jupyter notebook
```

