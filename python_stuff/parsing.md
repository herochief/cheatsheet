# Parsing

In python, we learn of input functions. \
But. wouldn't it be nice if we could state the parameters beforehand. \
In other words, **parsing** data

I will go through each segment of parsing parameters. \
At the end of the tutorial, an example will be shown.

### Python Library

In order to create the situation for us to do our parsing abilities, we need a library.

To install: \
`$ pip install argparse`

In the python script, import the library: \
`import argparse`


### Initialising the a Argument Parser()

In essense there is no need to do this but it would make things earier. \
Furthermore, its common practise to do this.

`parser = argparse.ArgumentParser()`


### Creating the Arguments

To setup the arguments to input. we are going to use the `parser.add_arguments(---)` function. \
This will declare the arguments we want and how to indicate that this variable is the one we want to input a certain value into.

Syntax:
> `parser.add_argument("--variable_name", type=<dtype>, default=<value>, help="<what do i do>") `

Example:
> `parser.add_argument("--epoch", type=int, default=0, help="epoch to start training from")`

syntax | Description | example
----|-------|------
`"--variable_name"` | This will be the name of our flag, to indicate which variable our value goes to. | "--age"
`type=<dtype>`      | Declare the variable type | type = int
`default =<value>`  | If a variable was not declared outside, we still need a value. | default = 64
`help`              | Descript the variables usage | help ='batch size for training'

### After the arguments

Once we declare our arguments, we parse the arguments into a holder

`opt = parser.parse_args()`

### Using the variables

From now we use `opt.<variable_name>` to refer to our variables. \
Remember from our arguments , we have the variable name for our flag, we will use that to refer to the variables in the script.

eg.
```
parser.add_argument("--epoch", type=int, default=0, help="epoch to start training from")
opt = parser.parse_args()
epochs_count = opt.epoch
```
### Shell Scripts 

Say want to create a sh script with our parameters. \
We just have to indicate the flags and values

```
python testing.py \
--epoch 200 \
--batch_size 32 \
--start 10
```

**Note:** You can technically type it all into one line but I find this layer by layer neater.

**Note 2:** If you want to know the arguments and usage, use `-h` or `--help`

### Example

testing.py

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--x", type=int, default=0, help="Value of X")
parser.add_argument("--y", type=int, default=0, help="Value of Y")
opt = parser.parse_args()
x = opt.x
y = opt.y
print("The sum of x and y is ", x+y)
print("The sum of opt x and y is ", opt.x + opt.y)
```

run.sh
```
#! usr/bin/sh

python testing.py \
--x 9 \
--y 8
```






