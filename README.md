## Deep Q Networks - Automated Trading on multiple stocks

## Dataset
- The used dataset is a synthetically generated dataset for three different assets using the `Alpha Vantage API`, that allows accessing both historic and real time stock data.
- There is a correlation between all the three generated dataset, this is achieved by tuning several parameters during generation. 

*This dataset is provided for the Data Science Mini-Project model by the University of Bristol in association with HSBC for experimentation purpose only.*

- The induced correlation between the datasets in that the *stock prices tend to rise from Tuesday and fall down by the end of week or Friday.*


## Setting up the environment

**Force install python 2.7 in an environment with conda**

`conda create --override-channels -c defaults -n py27 python=2.7`

**Activate the environment** (Environment Name is py27)

`conda activate py27`

else

`source activate py27`

**Install Requirements from txt file**

`pip install -r requirements.txt`

**In case of any errors or warning Install the specific versions using commands below**

* Tensorflow: `pip install tensorflow==1.15`

* Keras: `pip install Keras==2.2.4`

---

**Training Deep Q Agent**

`python run.py --mode train`

**Testing Deep Q Agent**

`python run.py --mode test --weights <Saved Weights>`

---
## Model Brief

**Agent**
- Based on Q-learning (DQN a Q-learning variant)
- **DQN Agent** a value-based agent runs on train to estimate future rewards.

**Environment**
- 3-stock trading environment (A,B,C)
**State**
- stocks owned, current stock prices, cash in hand
- close price is used for each stock

**Action State**
Action: sell (0), hold (1), buy (2)
- selling -> sell all shares
- buying -> buy as many shares possible
- when buying multiple stocks, equally distribute cash in hand and utilize the balance

The model is a feedforward ANN, a multilayer perceptron.

**Training Information**
- Number of episodes 2000
- Train and Test Split (50-50) with 10328 instances each
- Epochs 2
- Batch size 64

**Training Hardware used**
- Cloud compute with 16GB Ram and NVIDIA Tesla P100
---
### Model Architecture
The DQN model uses Markov Decision Processes (MDPs) to learn from experience.


<img src="images/markov decision process.png" width="700" height="400">

The Q values are estimated using a neural network. And the network is trained using the Bellman equation using iterative steps as shown below.


<img src="images/bellman equation.png" width="500" height="600">

The Train and Test performance of the model are as shown below. The DQN model was able to generate a profit when trained for 2000 episodes.


<img src = "images/Custom_RL performance.png" width="1000" height="300">


## References: 
Machine learning on Trading
- https://github.com/stefan-jansen/machine-learning-for-trading
- https://github.com/ShuaiW/teach-machine-to-trade
- https://github.com/DrAshBooth/BristolStockExchange
