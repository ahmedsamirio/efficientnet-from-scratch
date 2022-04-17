# efficientnetv1-from-scratch

In this notebook I'll explore building an efficient net from scratch, following by an attempt to recreate the paper steps into achieving its final results.
I think that I should go into this project through these steps to make it easy:

- [ ]  Implement an MBConv layer
- [ ]  Implement an efficientnet baseline
- [ ]  Test efficientnet on fastai imagenette using paper configuration and compare with resent
- [ ]  Implement neural architecture search 


EfficientNets are similar to ResNets in that they consist of bottleneck layers. However, EfficientNets use <strong>MBConv (Mobile Inverted Bottleneck Convolutional Blocks)</strong> followed by <strong>SEBlocks (Squeeze and Excitation Blocks)</strong>

## MBConv block
### What is an MBConv block?

An MBConv block is the building block of MobileNetV2, and here is an excerpt from the MobilNetV2 papers describing it.

> Our network pushes the state
of the art for mobile tailored computer vision models,
by significantly decreasing the number of operations and
memory needed while retaining the same accuracy.

An MBConv layer module is an <strong><em>inverted residual with linear bottleneck</em></strong>.

This definition needs a little bit of dissection. First let's take a look at a residual block.

![residual block](https://miro.medium.com/max/1140/1*D0F3UitQ2l5Q0Ak-tjEdJg.png)

A residual block (bottleneck layer) is a module which basically adds it's input to the final output of the block. We can see that it has ReLU non-linearity, and in the ResNet architecture, the number of channels generally tends to expand, and inside the block the bottleneck occures in decreasing the channels, then increasing it back again.

![resnet](https://www.researchgate.net/publication/336642248/figure/fig1/AS:839151377203201@1577080687133/Original-ResNet-18-Architecture.png)

#### So how does an MBConv differ from Residual Block?

1. Channels depth increases within the block then they decrease upon output 
2. ReLU isn't used in the output layer and only used within the expansion zone

<img src="https://production-media.paperswithcode.com/methods/Screen_Shot_2020-06-06_at_10.08.25_PM.png" width="400" align="center" />

### Why use an MBConv Layer?

1. More efficient
2. Reduce computational time

### Now let's implement it using fastai
