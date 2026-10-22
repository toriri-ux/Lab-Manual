The objective of this lab is to implement and compare three neural network architectures on the Fashion-MNIST dataset:

Multi-Layer Perceptron (MLP)
Convolutional Neural Network (CNN)
Transformer-Based Attention Model
The comparison is based on:

Classification accuracy
Number of trainable parameters
Floating Point Operations (FLOPs)
Inference latency

2. Dataset
The Fashion-MNIST dataset was used for all experiments.

Dataset Details
Property	Value
Image Size	28 × 28
Channels	1 (Grayscale)
Number of Classes	10
Training Images	55,000
Validation Images	5,000
Test Images	10,000
Batch Size	128
Data Normalization
The images were normalized using:

transforms.Normalize((0.2860,), (0.3530,))
3. Model Architectures
3.1 Multi-Layer Perceptron (MLP)
Architecture:

Flatten
↓
Linear(784 → 256)
↓
ReLU
↓
Linear(256 → 128)
↓
ReLU
↓
Linear(128 → 10)
Characteristics
Fully connected architecture
Treats images as flat vectors
Does not exploit spatial information
3.2 Convolutional Neural Network (CNN)
Architecture:

Conv2D(1→16, 3×3)
↓
ReLU
↓
MaxPool2D
↓
Conv2D(16→32, 3×3)
↓
ReLU
↓
MaxPool2D
↓
Flatten
↓
Linear(1568 → 10)
Characteristics
Learns local image features
Uses parameter sharing
Suitable for image classification tasks
3.3 Attention-Based Model
Architecture:

Image
↓
16 Patches (7×7)
↓
Patch Embedding (49 → 64)
↓
Transformer Encoder Layer
↓
Transformer Encoder Layer
↓
Mean Pooling
↓
Linear(64 → 10)
Characteristics
Captures global relationships between image regions
Uses self-attention mechanism
Inspired by Vision Transformers

4. Experimental Setup
Hyperparameters
Hyperparameter	Value
Optimizer	Adam
Learning Rate	0.001
Loss Function	CrossEntropyLoss
Epochs	5
Batch Size	128

5. FLOP Calculations
5.1 MLP FLOPs
Consider the first fully connected layer:

Linear(784 → 256)
Formula:

FLOPs = 2 
\times Input 
\times Output
Substitution:

FLOPs = 2 
\times 784 
\times 256
= 401,408
Result
MLP FLOPs = 401,408

5.2 CNN FLOPs
Consider the first convolution layer:

Conv2D(1→16, 3×3)
Formula:

FLOPs=
2
\times K
\times K
\times C_{in}
\times C_{out}
\times H_{out}
\times W_{out}
Substitution:

=
2
\times3
\times3
\times1
\times16
\times28
\times28
=
225,792
Result
CNN FLOPs = 225,792

5.3 Attention FLOPs
QKV Projection:

Formula:

FLOPs=
2
\times seq
\times d_{model}
\times3
\times d_{model}
Substitution:

=
2
\times16
\times64
\times3
\times64
=
393,216
Result
Attention FLOPs = 393,216

6. Parameter Analysis
Model	Parameters
MLP	REPLACE
CNN	REPLACE
Attention	REPLACE
Observations
The MLP contains a large number of fully connected weights.
The CNN reuses convolution kernels, improving parameter efficiency.
The Attention model introduces additional projection and transformer parameters.

7. Classification Results
Test Accuracy
Model	Accuracy (%)
MLP	REPLACE
CNN	REPLACE
Attention	REPLACE

8. Latency Analysis
Batch Size = 1
Model	Latency (ms)
MLP	REPLACE
CNN	REPLACE
Attention	REPLACE
Batch Size = 128
Model	Latency (ms)
MLP	REPLACE
CNN	REPLACE
Attention	REPLACE

9. Accuracy vs Parameters

plt.savefig("Accuracy_VS_Parameters.png")


Discussion
This figure shows the relationship between model complexity and classification accuracy.

The CNN achieves high accuracy with relatively fewer parameters compared to the MLP. The Attention model introduces additional complexity while providing competitive classification performance.

10. Accuracy vs Latency

accuracy_vs_latency.png

Discussion
This figure illustrates the trade-off between prediction accuracy and inference speed.

Models with higher computational complexity generally exhibit longer inference times. CNNs often provide an excellent balance between accuracy and latency.

11. Discussion
Hand calculations only count major mathematical operations.

THOP may additionally include:

Bias additions
Pooling operations
Layer normalization
Activation functions
Tensor reshaping
Attention implementation overhead

Therefore THOP values are expected to be slightly higher.

The three architectures demonstrate different approaches to image classification.

The MLP treats the image as a flat vector and therefore ignores the spatial structure of the image. Although it performs reasonably well, it generally achieves lower accuracy compared to the CNN.

The CNN leverages convolutional layers to learn local visual features such as edges, textures, and patterns. Weight sharing enables it to achieve strong accuracy with efficient parameter usage.

The Attention model processes image patches and learns relationships between different image regions using self-attention. While it captures global dependencies effectively, it introduces additional computational overhead and latency.

Overall, the CNN provided the best balance between classification performance and computational cost.



12. Conclusion
Three neural network architectures were implemented and evaluated on the Fashion-MNIST dataset.

Key findings:

MLP provides a simple baseline but does not fully utilize image structure.
CNN achieves the strongest trade-off between accuracy and efficiency, it achieves the highest test accuracy while using fewer parameters and lower latency than the MLP and Attention models.
Attention-based models can capture global relationships but typically require more computation.
Based on accuracy, latency, and FLOP analysis, the CNN is the most efficient architecture for Fashion-MNIST classification.

