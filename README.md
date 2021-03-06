# Candy
Candy: Self-driving in Carla Environment.

<img src="https://github.com/createamind/candy/blob/master/screenshots/candy.png" width="500"/>

What is candy? A model with the structure: Hierarchical Observation -- Plan&Policy -- Hierarchical Actions

We use VAE/GAN/Glow for world representation, and do RL/IL/Planning/MCTS upon it.


## Demo

### Performance

Car drifting (more to be uploaded):

<img src="https://github.com/createamind/candy/blob/master/screenshots/drift.gif" width="300" style="display:inline"/>

City navigation:

<img src="https://github.com/createamind/candy/blob/master/screenshots/carla_long.gif" width="300" style="display:inline"/>

### VAE

Real:

<div>
    <img src="https://github.com/createamind/candy/blob/master/screenshots/real1.png" width="250" style="display:inline"/>
    <img src="https://github.com/createamind/candy/blob/master/screenshots/real2.png" width="250" style="display:inline"/>
</div>

Reconstructed: (With hidden state of size 50, running for 1 hour on a single GTX1080Ti)

<div>
    <img src="https://github.com/createamind/candy/blob/master/screenshots/reconstruct1.png" width="250" style="display:inline"/>
    <img src="https://github.com/createamind/candy/blob/master/screenshots/reconstruct2.png" width="250" style="display:inline"/>
</div>


## Running Candy
(This project is still working in progress.)
* Download Carla-0.8.2 from [here][carlarelease].
* Start CarlaUE4 engine in server mode, using commands from [here][carlagithub].

        ./CarlaUE4.sh -windowed -ResX=800 -ResY=600 -carla-server -benchmark -fps=10
    
* Install Carla PythonClient using:

        pip install ~/carla/PythonClient

* Install Openai baselines under instructions [here][baseline].
* Install required packages:

        pip install numpy tensorflow-gpu msgpack msgpack-numpy pyyaml tqdm gym opencv-python scipy pygame pillow
    
* Start the program by running:

        CUDA_VISIBLE_DEVICES=0 python main.py -m Town01 -l

* Visualization: After running the following command, open localhost:6006 on the browser.

        tensorboard -logdir=./logs



[carlagithub]: http://carla.readthedocs.io/en/latest/running_simulator_standalone/
[carlarelease]: https://github.com/carla-simulator/carla/releases
[baseline]: https://github.com/openai/baselines


## Candy Features
* Combining imitation learning and reinforcement learning. Candy can learn make its first turn in 40 minutes(Single GTX1080Ti) from scratch (randomize policy network).
* VAE unsupervised learning for world model construction.
* Persistent training process and flexible architecture.

## Todo
- [x] Depth, framestack as input.
- [x] Prioritized replay for better VAE learning.
- [x] PPO.
- [x] Imitation learning.
- [x] Stop when collide.
- [x] Visualize parameter transition.
- [x] Less summary.
- [ ] Better VAE.
- [ ] Solve catastrophic forgetting problem.
- [ ] Better RL.
- [ ] What & Where correspondence. Map data as auxilary task, using part of the hidden state.
- [ ] Distributed data collection.
- [ ] Lidar!
- [ ] Test Strategy?
- [ ] World recurrent transition model.
- [ ] Guiding commands following. (Or integrate with map)
- [ ] Traffic rules learning: Traffic Lights.
- [ ] Traffic rules learning: Signs.
- [ ] Implement MCTS.
- [ ] Auxilary tasks.
- [ ] Openai Glow?
- [ ] Speed, Depth, Orientation as inputs.
- [ ] Policy embedding? Curiosity, Attention, Memory?
- [ ] The ability of planning
- [ ] Math representation, Language acuisition
- [ ] Attentional VAE
- [ ] Attention for Representation explanation.

## Ideal Features

* Curiosity-based Attention, Supervised Attention, loop-control-Attention, Interpretable Attention.
* VAE + modelbased planning + video prediction + MCTS.
* GQN, what-where in any place (Better generalization).
* guiding commands following (HRL, Multi-tasking).
* From implicit to explicit: Meta-learning, Rule Learning (Experiments from imaginary room).
* Stronger world model with enhanced VAE(maybe with attention).

## Code Components
* main.py: Main file. It Deals with Carla environment.
* carla_wrapper.py: Wrap main.py, buffer information for the model.
* candy_model.py: Main model file. It is for building the big graph of the model.
* modules/* : Building blocks of the model, used in candy_model.py.


