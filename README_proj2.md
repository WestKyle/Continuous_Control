

# Project 2: Continuous Control

### Introduction
In this project, we train an agent (or agents) to control a double jointed arm for reaching a goal position in the Unity ML-Agents Reacher Environment.  We actually have two environments to choose from:  one with just one agent, or one with 20 agents.  In the case with 20 agents, we have 20 arms to control independently.  Consequently, we can take advantage of the experience from all the agents to train the control model. 

### State Space
Our state space consists of 33 variables that include the position, rotation, velocity and angular velocity of the arm (each arm in the 20 agent case).  The agent(s) receives a reward of +0.1 for each time step in where the arm is in the goal location.

### Action Space
The agent(s) learns to control the arm with a vector of four values representing the torque of the two joint arm.  These values range from -1.0 to +1.0 in continuous floating point space.

### Solving the environment
Option 1, a single agent: Solving this environment requires training the agent to reach a score of +30 after 100 consecutive episodes. 
Option 2, 20 agents: train the agents such that the average score of all 20 agents, averaged over 100 consecutive episodes, reaches +30.  In this case, the total score of all 20 agents is summed after every episode and the average calculated.  When this average meets or exceeds +30 over 100 episodes, the environment is solved.

### Getting Started (using Udacity Workspace)
The Jupyter Notebook Continuous_Control.ipynb is already in the Workspace folder and loads when you enter the Udacity Workspace.  The first executable line loads all the required packages according to requirements.txt located in the included python folder.
Now running !pip -q install ./python results in two warnings:  

"ipython 6.5.0 has requirement prompt-toolkit<2.0.0,>=1.0.15, but you'll have prompt-toolkit 3.0.16 which is incompatible." 

"tensorflow 1.7.1 has requirement numpy>=1.13.3, but you'll have numpy 1.12.1 which is incompatible."

I found these warnings to be inconsequential for the project.

The Continuous_Control.ipynb notebook only takes the project as far as running one episode with randomly generated actions.  To solve the environmnent, I created notebook Continuous_Control_multi.ipynb for the 20 agent environment.  This notebook loads the 20 agent Unity ML-Agents Reacher environment and contains code cells to solve the environment using the deep deterministic policy gradient (DDPG) approach.  I created another Jupyter Notebook called Continuous_Control_20_wEPS.ipynb that also solves the environment, but uses epsilon to gradually reduce exploration with successive episodes.  This latter approach yields solves the environment faster and with more stable scoring than the former. 

For this project, I used two python files: a file to contain the actor and critic models, and a file containing the agent class for controlling and training the agent.  I'm using the DDPG approach, so the file model_ddpg.py contains the class definitions of the Actor and Critic fully-connected layer models using Pytorch. The Actor model is used to select an action based on the environment state input. The Critic model is used to generate the Q-values for the DDPG algorithm.  The ddpg_agent_pen_20.py file contains the Agent class definition.  The "pen" part of the file name indicates this file was derived from the code in the ddpg_agent.py found in the  ddpg-pendulum folder of the DRLND github repository: https://github.com/udacity/deep-reinforcement-learning. "20" in the file name indicates it is written for the 20 agent Reacher environment.  These two python files must be in the same folder as the Continuous_Control_20_wEPS.ipynb notebook.  There is also another file called ddpg_agent_pen_20_eps which is the same as ddpg_agent_pen_20.py, but is maintained to run with the Continuous_Control_20_wEPS.ipynb notebook to capture any changes that may result from runs that we do not want in the ddpg_agent_pen_20.py file.

### Getting Started (downloading the project environment onto your PC)
If you want to run this project from you PC, then do the following:

1. Make sure you have cloned this [git repository](https://github.com/udacity/deep-reinforcement-learning)

2. Follow the instructions [here](https://github.com/udacity/deep-reinforcement-learning#dependencies) to create a new conda environment, install the python packages and create the IPython kernel.  Note that the Python Environment is installed in accordance with the package list in deep-reinforcement-learning\python\requirements.txt

3. If you have not installed Unity yet, no problem, the environment is already built for you here:

One Agent:

Linux: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
Mac OSX: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
Windows (32-bit): click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip)
Windows (64-bit): click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)

20 Agents:

Linux: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
Mac OSX: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
Windows (32-bit): click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
Windows (64-bit): click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)


### Instructions
Follow the instructions in the jupyter notebook Continuous_Control.ipynb found in the p2_continuous-control/ folder of the DRLND GitHub repository you should have already cloned. Use the provided code cells to observe the environment state and action spaces.  Create your own code to control the agent(s) through the environment using the provided code as an example to guide you and your chosen DRL methods. 

For my project, you can find my Jupyter Notebook in the repository named Continuous_Control_multi.ipynb.  This notebook uses the 20 agent environment.  All the code cells are provided in this notebook for running the project and solving the environment.  You will also find a second Jupyter Notebook called Continuous_Control_20_wEPS.ipynb that also solves the 20 agent environment.  However, this version uses a decaying epsilon to gradually decrease agent exploration via the [Ornstein-Uhlenbeck noise process](https://en.wikipedia.org/wiki/Ornstein-Uhlenbeck_process) on successive episodes.  
