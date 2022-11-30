# Cifar10 FedAvg and FedSGD with Secure Multiparty Computation (SMC)

N parties hold n subsets of the Cifar10 training dataset. After each few epochs of local training, they calculate the average of their local weights to use for the next training round. SMC protocol used is Shamir's Secret Sharing. Local Training only. 

## Requirements:

Python, Pytorch, Torchvision, Numpy, Matplotlib, Jupyter-Notebook

## Configuration

Configuration can be adjusted in the first few lines.

```python
# basic configuration
weight_averaging = False # use weight averaging? If off, all parties only train with local data
smc = False # use SMC for weight averaging? If off, weights are shared without any privacy guarantees.
n_epochs = 30 # number of total training rounds
weight_sharing_every_x_epoch = 5 # weight sharing after x training rounds. 1 = FedSGD, >1 = FedAvg
num_parties = 5 # number of ditributed parties. If set to 1, one party holds all data 
model = "alex" #"small" for small model, "alex" for AlexNet


#more advanced settings
equal_model = True # Do not train last shared model again
only_share_in_last_round = False # Only average weights one time at the end of local training
```

## Results

### AlexNet

#### 3 parties

no weight sharing, 20 epochs -> 72% accuracy

weight sharing every epoch (FedSGD), 20 epochs -> 74% accuracy

weight sharing every 5 epochs (FedAvg), 20 epochs -> 74% accuracy 

#### 5 parties

no weight sharing, 40 epochs -> 68% accuracy

no weight sharing, 60 epochs -> 67% accuracy

weight sharing every epoch (FedSGD), 40 epochs -> 78% accuracy

weight sharing every 5 epochs (FedAvg), 40 epochs -> 78% accuracy

weight sharing every epoch (FedSGD), 60 epochs -> 81% accuracy



#### 1 party (Baseline)

20 epochs -> 83% accuracy 

30 epochs -> 82% accuracy

40 epochs -> 82% accuracy 

60 epochs -> 81% accuracy

### Small Model

5 parties, no weight averaging, 30 epochs -> 58% accuracy

5 parties, weight averaging every 5 epochs (FedAvg), 30 epochs,  -> 62% accuracy

1 party, 30 epochs -> 75% accuracy

