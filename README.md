# ML4SCI GSOC GENIE Task
## Common Task 2. Jets as graphs 
Jet Images are not our typical RGB images as the three channels(Track, ECAL and HCAL) represent raw sensor data. Classification between the quark and gluon cannot be done using our typical Image Classification algorithms. The provided literature suggests converting the images to point cloud format which will better represent the relation between each point cloud. This point cloud can be represented as graphs that can capture the relation between individual nodes using edges thus providing a better understanding of the data. Training classification models based on Graph Neural Networks on this dataset will provide us with a much better result compared to traditional ways.

## Task
1. Choose a graph-based GNN model of your choice to classify (quark/gluon) jets. Proceed as follows:
   - Convert the images into a point cloud dataset by only considering the non-zero pixels for every event.
   - Cast the point cloud data into a graph representation by coming up with suitable representations for nodes and edges.
   - Train your model on the obtained graph representations of the jet events.
2. Discuss the resulting performance of the chosen architecture.

## Training 
The data set was trained on three different architectures, among which one was finally selected, with the same parameters:
```
Learning Rate: 0.001
Optimizer: Adam
Loss: Cross Entropy loss
Epochs: 30
```
## Results
### Point Cloud Result
The following is a sample of the point cloud representation of the image: 
![Point Cloud Representation of Jets](images/point.png "Pint Cloud of the Jet")

### Classification Result

Model  | Training Loss | Validation Loss
------------- | ------------- | ----------
GCN  | 0.6790 | 0.7080
GAT | 0.6723 | 0.6970
GraphSAGE | 0.6857 | 0.7200

## Discussion
The **final architecture** chosen here is the **Graph Sage** architecture.

- Firstly, among all three architectures we experimented on Graph Sage performed just slightly better.

- From a computational point of view Graph Sage is much more efficient than the other two architectures.

- Although the performance between the models is more or less the same here it can change when we use large batches or a bigger subset of data. In such cases, Graph Attention Networks are better as they will capture the deeper relation between the nodes, due to the attention mechanism, much better as compared to Graph Sage but at a trade-off of performance.

- Another factor to consider here is how we are representing the Images as graph. We can choose different node features such as the Values of the channels or momentum etc or use Euclidian metric instead of adjacency to be in the edge embedding to enrich the graph more. This may help in capturing a better representation of the graph overall.
