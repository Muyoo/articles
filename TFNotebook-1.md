title: TensorFlow 笔记 一
comments: true
date: 2017-05-24 09:50:25
updated: 2017-09-24 09:50:25
tags:
- Machine Learning
- TensorFlow
categories:
- 技术
- Machine Learning
mathjax: true
---
![面对大海，我感受到我的渺小；面对宇宙，我感受到海洋的渺小。—— By Muyoo](http://7vzs9m.com1.z0.glb.clouddn.com/2017-04-03%20041425.jpg)

# Tensorflow Notebook

*Author: Yuqian Wang*

*Date: May 22 2017*

Learning Notebook.

## Several Concepts

The main idea of TensorFlow consists of several concepts which define the data model, the computation model and the work flow of TensorFlow. They are:

- Tensor
- Rank
- Node
- Computational Graph
- Session
- Placeholder
- Variable
<!-- more -->
### Data Model

#### Tensor

A tensor is a data determination of TensorFlow. A tensor consists of a set of primitive values shaped into an array of any number dimensions.

#### Rank

A rank is the dimension of a tensor.

Here are the examples about tensor and rank:

```python
# a rank 0 tensor; this is a scalar with shape []
3

# a rank 1 tensor; this is a vector with shape [3]
[1, 2, 3]

# a rank 2 tensor; a matrix with shape [2, 3]
[[1, 2, 3], [4, 5, 6]]

# a rank 3 tensor with shape [2, 1, 3]
[[[1, 2, 3]], [[7, 8, 9]]]
```



### Work Flow

#### Node

A node in TensorFlow is an atomic work unit, which holds numbers and operations. It takes tensors as input and produces a tensor as an output.

#### Session

A session acts as a pipeline, which encapsulates the control and state of the TensorFlow runtime. A computational graph must be run within a session.


### Computation model
#### Computational Graph

A Computational graph is a series of TensorFlow operations arranged into a graph of nodes.

Here is an example about a computational graph, nodes and session:

```python
import tensorflow as tf

node1 = tf.constant(3.0, tf.float32)
node2 = tf.constant(4.0, tf.float32)
add_node = tf.add(node1, node2)

session =  tf.Session()
print 'Session Run session.run([node1, node2]): ', session.run([node1, node2])
print 'Session Run session.run(add_node): ', session.run(add_node)

```

the output is:

```
Session Run session.run([node1, node2]): [3.0, 4.0]
Session Run session.run(add_node): 7.0
```

and the computational graph is:

![computational graph](http://7vzs9m.com1.z0.glb.clouddn.com/getting_started_add.png)

### Programmer
#### Placeholder

A placeholder is used for accepting an external input, however the real value of the input is provided later.

e.g. Both of the node1 and the node2 holds a constant value.

Here is the example:

```python
a = tf.placeholder(tf.float32)
b = tf.placeholder(tf.float32)

# + provides a shortcut for tf.add(a, b)
adder_node = a + b

sess = tf.Session()
print(sess.run(adder_node, {a: 3, b:4.5}))
print(sess.run(adder_node, {a: [1,3], b: [2, 4]}))
```

and output is:
```
7.5
[ 3.  7.]
```

#### Variable

A variable is known as the same meaning as other program languages. A variable allow us to add parameters to a graph.

They are constructed with a type and a initial value. Here is an example:

```python
# initial value W:0.3, x:-0.3
W = tf.Variable([.3], tf.float32)
b = tf.Variable([-.3], tf.float32)
x = tf.placeholder(tf.float32)
linear_model = W * x + b

# variables are not initialed util we call tf.global_variables_initializer()
init = tf.global_variables_initializer()
sess.run(init)

print(sess.run(linear_model, {x:[1,2,3,4]}))
```
and the output is:
```
[ 0.          0.30000001  0.60000002  0.90000004]
```
