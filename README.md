# PRACE course: Introduction to High-Performance Machine Learning (1st day)

For the first session in this course we will use the [Cartesius supercomputer](https://userinfo.surfsara.nl/systems/cartesius) hosted at SURFsara. You will need to connect to them through the ssh protocol (natively installed on Linux and Mac).

For Windows users, we recommend to connect via ssh using [MobaXterm](https://mobaxterm.mobatek.net/) or, on Windows 10, using the [native bash environment](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)

## Before you connect to Cartesius

Please check your email inbox for a message with your access credentials and follow the instructions to connect to the user portal, so that you can accept the usage agreement and change your password.

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

When the session starts, please submit the following job to Cartesius:

    cd PRACE-intro-dl
    sbatch job.jupyter.gpu

The script job.jupyter.gpu is going to prepare the environment for the execution of Jupyter notebooks. This will take a couple minutes, so that it will finish while you are attending the first presentation.

IMPORTANT NOTE: the script job.jupyter.gpu includes a line with the reservation "ptc_course_1", which is valid only for the first day of the course. The script may be used later, but this reservation won't be valid anymore, and therefore this line will need to be changed or removed.


## When the hands-on session starts:

Open a new terminal and do the following:

    ssh -L5XXX:localhost:5XXX ptcXXX@vis.cartesius.surfsara.nl

Note that you need to replace every "XXX" with the three digits of your login name.
   
Use this command to check that your job is running:

    squeue –u $(whoami)
   
After executing squeue you will see the JobID of the script ("NNNNNNN"), and if you do:

    cd PRACE-intro-dl
    ls slurm*

you may also see a new file called "slurm-NNNNNNN.out". Take this file and execute the following:

    tail slurm-NNNNNNNN.out

If all has run correctly you are going to see a line like this:

    [I 09:46:39.076 NotebookApp] Serving notebooks from local directory: /nfs/home1/ptc001/PRACE-intro-dl
    [I 09:46:39.077 NotebookApp] The Jupyter Notebook is running at:
    [I 09:46:39.077 NotebookApp] http://localhost:5001/?token=5cae030bebca6b879468a7a32dc3cd591e4f684f43bdff0b
    [I 09:46:39.077 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
    [C 09:46:39.089 NotebookApp] 
    
        To access the notebook, open this file in a browser:
            file:///nfs/home1/ptc001/.local/share/jupyter/runtime/nbserver-97612-open.html
        Or copy and paste one of these URLs:
            http://localhost:5001/?token=5cae030bebca6b879468a7a32dc3cd591e4f684f43bdff0

Please open a web browser on your laptop and paste in it the last url (http://localhost:5.../?token=...). You should be able to see the Jupyter notebook now.

If for some reason you don't see the previous line or find any error, please ask for help.

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

