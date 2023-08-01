Cartpole
==========

# Table of Contents
<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

- [My Solution](#my-solution)
- [My Modifications](#my-modifications)
- [How to train/use](#how-to-trainuse)
  * [GNU/Linux](#gnulinux)
  * [Windows](#windows)
- [Limitations](#limitations)
- [Credits](#credits)

<!-- TOC end -->

- Cartpole is a classic game used for learning and introducing reinforcement learning.
- Its simple (just 4 inputs to the neural network) and easy to understand nature makes it the ideal project for beginners to reinforcement learning and neural networks in general.

# My Solution

- I have used `pytorch` as my primary library for the neural network.
- The model `cart-stable.pt` for trained for about 1000 generations, after which, it can run basically infinitely, without losing.
- For the actual game, I have used a modified version of the `gymnasium` library.

# My Modifications

- For my [purposes](https://github.com/dharmik2319/cs-exhibition), I modified the `cartpole.py` file in the `gymnasium` module for better viewing for the layman.
- It now has, in `human` rendering mode, a score counter, which just displays a modified version of the number of steps in an episode.
- I also heavily modified the scoring system. Using the default module, it took many more generations for the NN to become stable, compared to my mod. In my modified version, I made it so that the NN gets a negative reward for every episode for every unit that it strays farther from the center, in the X plane.
- This strict rewarding system made the NN play cartpole in a far more stable way.

# How to train/use

## GNU/Linux
- This *should* work properly with all Linux distros.

- First of all, clone this repo with

```bash
git clone https://github.com/dharmik2319/cartpole.git
```

- Then install all the required dependencies with 

```bash
pip install -r requirements.txt
```
- Now, for the modified `cartpole` environment, you can either replace your actual, original module files, or create a `venv`.
To replace the module in a local install, use

```bash
cp -R gymnasium/ ~/.local/lib/pythonX.XX/site-packages/gymnasium
```
Replace the X.XX with your python version (like 3.11 or 2.7).

- To run the trained model with a GUI, just do

```bash
python actor_critic.py
```

- To train your own model, just comment out the lines containing 
```python
time.sleep(1/24)
```
```python
env = gym.make("CartPole-v1", render_mode="human")
```
```python
model.load_state_dict(torch.load("./cart-stable.pt"))
```

- And uncomment these:
```python
torch.save(model.state_dict(), "./cart-stable.pt")
```
```python
env = gym.make("CartPole-v1")
```

- (Optional) And modify 50000 to any other number, (the steps till which you want an episode to last)
```python
for t in range(1, 50000):
```
***WARNING***: A higher number means more resource usage, so be careful and realistic when modifying it

- And lastly, you can also modify other parameters like the learning rate and the optimizer, and the number of layers and neurons.

## Windows

- Due to lack of support from the `gymnasium` library, you cannot run any environment with visuals (GUI) on Windows systems.

- But, you can follow the steps for [GNU/Linux](#gnulinux) and train the NN and also see its score in the CLI.

# Limitations

- Due to my limited `pygame` knowledge, and the way I implemented the scoring system, you cannot play a playable version of cartpole anymore, because it requires you to use `rgb-array` as rendering mode.

- The model can probably be much better, but due to time and computational constraints, I have not made it better.

- You are welcome to create a pull request to submit a more trained model, or to submit better, more documented code.

- This NN runs on a single core (and a single thread, I think). Making it multi-core would make performance skyrocket.

# Credits
- The template code was taken from `pytorch`'s examples.

- The `gymnasium` library which contains many environments useful for RL beginners.

