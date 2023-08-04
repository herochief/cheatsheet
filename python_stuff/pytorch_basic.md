# pytorch Basics

# starting

Firstly, we need to create NN layer. \
This Layer will serve as our machine learning arcitechture

### Class

We need to create a class for our network or model.

```
class Net(nn.Module):
    def __init__(self):
        super().__init__()
```
This is the important headers to begin. \
The `Net` some times can be model in other codes.

### __init__

In this function, we need to specify the layers. \
Note that I said layers, not activation functions.

```
class Net(nn.Module):
    def __init__(self):
        super().__init__() # just run the init of parent class (nn.Module)
        self.conv1 = nn.Conv2d(1, 32, 5) # input is 1 image, 32 output channels, 5x5 kernel / window
        self.conv2 = nn.Conv2d(32, 64, 5) # input is 32, bc the first layer output 32. Then we say the output will be 64 channels, 5x5 kernel / window
        self.conv3 = nn.Conv2d(64, 128, 5)

        x = torch.randn(50,50).view(-1,1,50,50)
        self._to_linear = None
        self.convs(x)

        self.fc1 = nn.Linear(self._to_linear, 512) #flattening.
        self.fc2 = nn.Linear(512, 2)
```
This is to define the nodes and layers, like 1000 nodes to 10 nodes with Fully connected.

### forward

torch forward function is a special function. This function will run regardless of being called, unique to the torch library. \
This Function is to define the activation functions for each layers that were specified previously.

```
def forward(self, x):
        x = self.convs(x)
        x = x.view(-1, self._to_linear)  # .view is reshape ... this flattens X before 
        x = F.relu(self.fc1(x))
        x = self.fc2(x) # bc this is our output layer. No activation here.
        return F.softmax(x, dim=1)
```

### Summary

Overall for this section of creating the Network, we have 3 parts:
1. Class to define the Networt
2. Define the layers
3. Deine the activation functions for the layers.

This is what it will look like combined

```
import torch
import torch.nn as nn
import torch.nn.functional as F

class Net(nn.Module):
    def __init__(self):
        super().__init__() # just run the init of parent class (nn.Module)
        self.conv1 = nn.Conv2d(1, 32, 5) # input is 1 image, 32 output channels, 5x5 kernel / window
        self.conv2 = nn.Conv2d(32, 64, 5) # input is 32, bc the first layer output 32. Then we say the output will be 64 channels, 5x5 kernel / window
        self.conv3 = nn.Conv2d(64, 128, 5)

        x = torch.randn(50,50).view(-1,1,50,50)
        self._to_linear = None
        self.convs(x)

        self.fc1 = nn.Linear(self._to_linear, 512) #flattening.
        self.fc2 = nn.Linear(512, 2) # 512 in, 2 out bc we're doing 2 classes (dog vs cat).

    def convs(self, x):
        # max pooling over 2x2
        x = F.max_pool2d(F.relu(self.conv1(x)), (2, 2))
        x = F.max_pool2d(F.relu(self.conv2(x)), (2, 2))
        x = F.max_pool2d(F.relu(self.conv3(x)), (2, 2))

        if self._to_linear is None:
            self._to_linear = x[0].shape[0]*x[0].shape[1]*x[0].shape[2]
        return x

    def forward(self, x):
        x = self.convs(x)
        x = x.view(-1, self._to_linear)  # .view is reshape ... this flattens X before 
        x = F.relu(self.fc1(x))
        x = self.fc2(x) # bc this is our output layer. No activation here.
        return F.softmax(x, dim=1)

if __name__ == '__main__':

net = Net()
outputs = net(input_tensor)

```
-----------------------------------------

# Creating the Data

In order to training, we need to create data for it. In this section, we will go through the a simple way of converting images to tensor, preparing it for training.

### Data required

First we need 2 things, images and their labels.

```
list_of_images = os.listdir(image_diectory)
OR
list_of_images = glob.glob1('.','*.jpg')
```

Load the images

```
for images_filename in list_of_images:
    img = cv2.imread(images_filename, cv2.IMREAD_GRAYSCALE)
```

### Converting the images to proper size.

The Neural Networks are fairly rigid. They require a consistance input size. \
Imagine those vegetable cutting machine. The output size is roughly the same as the cuts are the same, if its bigger, its cuts more away, it its smaller it cuts less away. 

More technically, If weights are trained from 20 nodes to 10 nodes. If the input is bigger, there cannot be weights for for the extra nodes. If its smaller, where do you start or end. eg, input 5 for 20 nodes, do you put all 5 from the top or do you put them in the end.

Either way, its best to have a consistant size.

```
IMG_SIZE = 50

for images_filename in list_of_images:
    img = cv2.imread(images_filename, cv2.IMREAD_GRAYSCALE)
    img = cv2.resize(img, (self.IMG_SIZE, self.IMG_SIZE))
```
### Creating a list

now with your images, you want to create a list with the image ans the corresponding label.

Note that the label must have a input of `[1,0]` \
This is one-hot. Its like a boolen table `[true,false]` \
```
[cat,dog,man]

input --> [0,0,1]
output --> man

eg.

cat = 0
dog = 1
number_of_classes = 2

classs = np.eye(number_of_classes)[dog]
```

Combine them
```
training_data = []
for images_filename in list_of_images:
    img = cv2.imread(images_filename, cv2.IMREAD_GRAYSCALE)
    img = cv2.resize(img, (self.IMG_SIZE, self.IMG_SIZE))
   
    training_data.append([np.array(img), np.eye(2)[dog])
```
### save to npy

save them

```
np.random.shuffle(self.training_data)
np.save("training_data.npy", self.training_data)
```

load them

```
training_data = np.load("training_data.npy", allow_pickle=True)
```

### Convert to tensor

```
training_data = np.load("training_data.npy", allow_pickle=True)
    print(len(training_data))
    X = torch.Tensor([i[0] for i in training_data]).view(-1,50,50)
    X = X/255.0
    y = torch.Tensor([i[1] for i in training_data])

    VAL_PCT = 0.1 # split in the training and testing
    val_size = int(len(X)*VAL_PCT)

    train_x = X[:-val_size]
    train_y = y[:-val_size]
    test_x = X[-val_size:]
    test_y = y[-val_size:]
```
### example
```
import cv2
from tqdm import tqdm
import os
import numpy as np

REBUILD_DATA = True # set to true to one once, then back to false unless you want to change something in your training data.

class DogsVSCats():
    IMG_SIZE = 50
    CATS = "images/Cat"
    DOGS = "images/Dog"
    TESTING = "PetImages/Testing"
    LABELS = {CATS: 0, DOGS: 1}
    training_data = []

    catcount = 0
    dogcount = 0

    def make_training_data(self):
        for label in self.LABELS:
            print(label)
            for f in tqdm(os.listdir(label)):
                if "jpg" in f:
                    try:
                        path = os.path.join(label, f)
                        img = cv2.imread(path, cv2.IMREAD_GRAYSCALE)
                        img = cv2.resize(img, (self.IMG_SIZE, self.IMG_SIZE))
                        self.training_data.append([np.array(img), np.eye(2)[self.LABELS[label]]])  # do something like print(np.eye(2)[1]), just makes one_hot 
                        print(np.eye(2)[self.LABELS[label]])

                        if label == self.CATS:
                            self.catcount += 1
                        elif label == self.DOGS:
                            self.dogcount += 1

                    except Exception as e:
                        pass
                        #print(label, f, str(e))

        np.random.shuffle(self.training_data)
        print((self.training_data.shape))
        np.save("training_data.npy", self.training_data)
        print('Cats:',dogsvcats.catcount)
        print('Dogs:',dogsvcats.dogcount)

if REBUILD_DATA:
    dogsvcats = DogsVSCats()
    dogsvcats.make_training_data()

```

# Inputing the data

Now we need to decide on the parameters.like epochs,learning rate, lost/cost function.

```
BATCH_SIZE = 50
EPOCHS = 30
optimizer = optim.Adam(net.parameters(),lr = 0.001)
loss_function = nn.MSELoss()
```
creating the loop epoch and batches

```
for epoch in range(EPOCHS):
        print ("epoch num:",epoch)
        for i in tqdm(range(0 , len(train_x) , BATCH_SIZE) ):
            batch_x = train_x[i:i+BATCH_SIZE].view(-1,1,50,50)
            batch_y = train_y[i:i+BATCH_SIZE]
            net.zero_grad()
            outputs = net(batch_x)
```

Determine the loss and update the network/model
```
            loss = loss_function(outputs,batch_y.cuda())                    
            loss.backward()
            optimizer.step()
```

testing the model
``` 
        correct = 0
        total = 0
        for i in tqdm(range(len(test_x))):
            real_class = torch.argmax(test_y[i])
            net_out = net(test_x[i].view(-1,1,50,50).cuda())[0]
            predicted_class = torch.argmax(net_out)
            if predicted_class == real_class:
                correct += 1
            total += 1
        
        print("accuracy", round(correct/total,3))   

```
save your weights and biases
```
torch.save({
            'epoch': epoch,
            'net_state_dict': net.state_dict(),
            'optimizer_state_dict': optimizer.state_dict(),
            'loss': loss,
            }, 'testing.pth') 

# testing.pth is the name for the file to be saved as.

```
### Example

```
if __name__ == '__main__':

    net = Net()

    training_data = np.load("training_data.npy", allow_pickle=True)
    print(len(training_data))
    X = torch.Tensor([i[0] for i in training_data]).view(-1,50,50)
    X = X/255.0
    y = torch.Tensor([i[1] for i in training_data])

    VAL_PCT = 0.1
    val_size = int(len(X)*VAL_PCT)

    train_x = X[:-val_size]
    train_y = y[:-val_size]
    test_x = X[-val_size:]
    test_y = y[-val_size:]
    print (len(train_x) ,len(test_x))

    BATCH_SIZE = 50
    EPOCHS = 30
    optimizer = optim.Adam(net.parameters(),lr = 0.001)
    loss_function = nn.MSELoss()
    evaluation_check = 5

    for epoch in range(EPOCHS):
        print ("epoch num:",epoch)
        for i in tqdm(range(0 , len(train_x) , BATCH_SIZE) ):
            batch_x = train_x[i:i+BATCH_SIZE].view(-1,1,50,50)
            batch_y = train_y[i:i+BATCH_SIZE]
            net.zero_grad()
            outputs = net(batch_x)

            loss = loss_function(outputs,batch_y)
            loss.backward()
            optimizer.step()

        correct = 0
        total = 0
        loss_np =loss.cpu().data.numpy()
        array_loss.append([count,loss_np]) 

        for i in tqdm(range(len(test_x))):
            real_class = torch.argmax(test_y[i])
            net_out = net(test_x[i].view(-1,1,50,50).cuda())[0]
            predicted_class = torch.argmax(net_out)
            if predicted_class == real_class:
                correct += 1
            total += 1

        print("accuracy", round(correct/total,3))      
        
        torch.save({
                'epoch': epoch,
                'net_state_dict': net.state_dict(),
                'optimizer_state_dict': optimizer.state_dict(),
                'loss': loss,
                }, 'testing.pth')
```


# GPU

If you put everything together, it would run okay. But it will be on CPU. \
If the data increases, we might need more processing power by using the GPU.

### Do i have GPU and how many ?

> `torcu.cuda.is_available()` ==> True or False
> `torcu.cuda.device_count()` ==> value

### How to use?

##### Tell the net which GPU to use:
```
device = torch.device('cuda:0')
net = Net().cuda() or net = Net().to(device) 
```
cuda:0  indicate the first index of the GPU. using second gpu is "cuda:1"

##### Indicate the part of the codes be on the GPU

1. From the loop part, create a function.
```
def training(net):
    for epoch in range(EPOCHS):
        print ("epoch num:",epoch)
        for i in tqdm(range(0 , len(train_x) , BATCH_SIZE) ):
            batch_x = train_x[i:i+BATCH_SIZE].view(-1,1,50,50)
            batch_y = train_y[i:i+BATCH_SIZE]
            net.zero_grad()
            outputs = net(batch_x)

            loss = loss_function(outputs,batch_y)
            loss.backward()
            optimizer.step()

        torch.save({
                'epoch': epoch,
                'net_state_dict': net.state_dict(),
                'optimizer_state_dict': optimizer.state_dict(),
                'loss': loss,
                }, 
                'testing.pth')

    if __name__ == "__main__":
        training(net)
```

2. The input must be converted to some cuda thing.

Any inputs into the `net()` need to be .cuda()

```
outputs = net(batch_x.cuda())
loss = loss_function(outputs,batch_y.cuda())
```

3. The output will be in cuda type, to make use of it like with loss value, we need to convert it numpy or something else at least.

```
loss = loss_function(outputs,batch_y.cuda())
loss_np =loss.cpu().data.numpy()
```
# All Together

```
import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
from tqdm import tqdm
import numpy as np

class Net(nn.Module):
    def __init__(self):
        super().__init__() # just run the init of parent class (nn.Module)
        self.conv1 = nn.Conv2d(1, 32, 5) # input is 1 image, 32 output channels, 5x5 kernel / window
        self.conv2 = nn.Conv2d(32, 64, 5) # input is 32, bc the first layer output 32. Then we say the output will be 64 channels, 5x5 kernel / window
        self.conv3 = nn.Conv2d(64, 128, 5)

        x = torch.randn(50,50).view(-1,1,50,50) # random to create size
        self._to_linear = None
        self.convs(x)

        self.fc1 = nn.Linear(self._to_linear, 512) #flattening.
        self.fc2 = nn.Linear(512, 2) # 512 in, 2 out bc we're doing 2 classes (dog vs cat).

    def convs(self, x):
        # max pooling over 2x2
        x = F.max_pool2d(F.relu(self.conv1(x)), (2, 2))
        x = F.max_pool2d(F.relu(self.conv2(x)), (2, 2))
        x = F.max_pool2d(F.relu(self.conv3(x)), (2, 2))

        if self._to_linear is None:
            self._to_linear = x[0].shape[0]*x[0].shape[1]*x[0].shape[2]
        return x

    def forward(self, x):
        x = self.convs(x)
        x = x.view(-1, self._to_linear)  # .view is reshape ... this flattens X before 
        x = F.relu(self.fc1(x))
        x = self.fc2(x) # bc this is our output layer. No activation here.
        return F.softmax(x, dim=1)

def training(net):
    array_loss = []
    array_acc = []
    count = 1
    for epoch in range(EPOCHS):
        print ("epoch num:",epoch)
        for i in tqdm(range(0 , len(train_x) , BATCH_SIZE) ):
            batch_x = train_x[i:i+BATCH_SIZE].view(-1,1,50,50)
            batch_y = train_y[i:i+BATCH_SIZE]
            net.zero_grad()
            outputs = net(batch_x.cuda())

            loss = loss_function(outputs,batch_y.cuda())
            
                
            count += 1
            #print('loss:',loss_np)
            loss.backward()
            optimizer.step()

        correct = 0
        total = 0
        loss_np =loss.cpu().data.numpy()
        array_loss.append([count,loss_np]) 

        if ((epoch%evaluation_check)== 0 ) or epoch == (EPOCHS-1):
            for i in tqdm(range(len(test_x))):
                real_class = torch.argmax(test_y[i])
                net_out = net(test_x[i].view(-1,1,50,50).cuda())[0]
                predicted_class = torch.argmax(net_out)
                if predicted_class == real_class:
                    correct += 1
                total += 1

            print("accuracy", round(correct/total,3))      
            array_acc.append([count,round(correct/total,3)]) 
        
        
        torch.save({
                'epoch': epoch,
                'net_state_dict': net.state_dict(),
                'optimizer_state_dict': optimizer.state_dict(),
                'loss': loss,
                }, 'testing.pth')
    np.save("plotting1.npy", array_loss)
    np.save("plotting2.npy", array_acc)
    print(array_loss)

if __name__ == '__main__':

    device = torch.device('cuda:0')
    net = Net().cuda()
    #net = Net()

    training_data = np.load("training_data.npy", allow_pickle=True)
    print(len(training_data))
    X = torch.Tensor([i[0] for i in training_data]).view(-1,50,50)
    X = X/255.0
    y = torch.Tensor([i[1] for i in training_data])

    VAL_PCT = 0.1
    val_size = int(len(X)*VAL_PCT)

    train_x = X[:-val_size]
    train_y = y[:-val_size]
    test_x = X[-val_size:]
    test_y = y[-val_size:]
    print (len(train_x) ,len(test_x))

    BATCH_SIZE = 50
    EPOCHS = 30
    optimizer = optim.Adam(net.parameters(),lr = 0.001)
    loss_function = nn.MSELoss()
    evaluation_check = 5

    training(net)

```

# Model Summary

Once we create a model or network, we check if it can run, In hopes that the number of input and output channels are correct. However, we do not realy know if the model we created is actually the model we expected. 

To view the layers in the model or the model architecture, we can use summary to check the flow of the inputs.

### 1.  Import the library

`from torchsummary import summary`

### 2.  Code as per normal

Setup thr network as how you would to train or test. The whole idea is to basically have the function run through the network and take a look into the network.

eg.
```
class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        ...

    def forward(self, x):
        ...
        return output

if __name__ == '__main__':
    
    net = Net()
    
    input_tensor = torch.rand((1,3,32,32))
    output = net( input_tensor )

```

### 3. Now use the summary function

In the function there are 2 parts to input. \
The model and the input size.

> Syntax: `summary( < model > ,< input size >) `

eg. \
Assume you have an input size of `3 channel, 32 height, 32 width`.

```
if __name__ == '__main__':
    
    net = Net()
    net = net.cuda()
    summary(net,(3,32,32))
```

The terminal will print the model architecture.

```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1         [-1, 64, 100, 100]           1,792
            Conv2d-2         [-1, 64, 100, 100]          36,928
            Conv2d-3         [-1, 64, 100, 100]          36,928
       BatchNorm2d-4         [-1, 64, 100, 100]             128
              ReLU-5         [-1, 64, 100, 100]               0
            Conv2d-6         [-1, 3, 100, 100]           36,928
       BatchNorm2d-7         [-1, 3, 100, 100]              128
          
================================================================
Total params: 112,832
Trainable params: 112,832
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.11
Forward/backward pass size (MB): 19.06
Params size (MB): 1.2
Estimated Total Size (MB): 20.03
----------------------------------------------------------------
```