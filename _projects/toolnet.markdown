---
layout: page
title: ToolNet
description:
img: /assets/img/toolnet.png
importance: 3
---

## Using Commonsense Generalization for Predicting Tool Use for Robot Plan Synthesis

This implementation contains all the models mentioned in the paper for next-tool prediction along with next-action prediction. Code available [here](https://github.com/reail-iitd/commonsense-task-planning).

## Contents 
- Introduction
- Environment Setup
- Directory Structure
- Setup Web Interface for Data Collection
- Dataset
- Training models

## Introduction

<img src="screenshot.png" width="900" align="middle">

In order to effectively perform activities in realistic environments like a home or a factory, robots often require tools. Determining if a tool could be effective in accomplishing a task can be helpful in scoping the search for feasible plans. This work aims at learning such "commonsense" to generalize and adapt to novel settings where one or more known tools are missing with the presence of unseen tools and world scenes. Towards this objective, we crowd-source a data set of humans instructing a robot in a Physics simulator perform tasks involving multi-step object interactions with symbolic state changes. The data set is used to supervise a learner that predicts the use of an object as a tool in a plan achieving the agent’s goal. The model encodes the agent’s environment, including metric and semantic properties, using gated graph convolutions and incorporates goal- conditioned spatial attention to predict the optimal tool to use. We demonstrate generalization for predicting tool use for objects unseen in training data by conditioning the model on pre-trained embeddings derived from a relational knowledge source such as ConceptNet. Experiments show that the learned model can accurately predict common use of tools based on spatial context, semantic attribute of objects and goals specifications and effectively generalize to novel scenarios with world instances not encountered in training.

{% capture details %}
```bash
$ python3 -m venv commonsense_tool
$ source commonsense_tool/bin/activate
(commonsense_tool) $ git clone https://github.com/reail-iitd/commonsense-task-planning.git
(commonsense_tool) $ cd commonsense-task-planning
(commonsense_tool) $ pip3 install -r requirements.txt
```

We used a system with 32GB RAM CPU and 8GB graphics RAM to run our simulator. The models were trained using the same system. The simulator and training pipeline has been tested on MacOS and Ubuntu 16.04.

{% endcapture %}
{% capture summary %}Environment Setup{% endcapture %}{% include details.html %}

{% capture details %}
To execute the website that is needed for data collection, use the following command:
```bash
$ python3 app.py --randomize
```
The website can now be accessed by using the link (http://0.0.0.0:5000/).
For all the arguments that can be provided look at the help provided,

```bash
$ python3 app.py --help
```
{% endcapture %}
{% capture summary %}Setup Web Interface for Data Collection{% endcapture %}{% include details.html %}

{% capture details %}
Download the dataset [here](https://drive.google.com/open?id=18dmWjDjz3DPYZTFv92vAnMssK2YFZh3j). Unzip it and put in the repository folder.

Here is how the dataset structure should look like:

```
dataset
├── home
├── factory
└── test
    ├── home
    └── factory
```

The dataset is organized as follows. We have 8 different goals and 10 different world instances for both the domains, home and factory. Each domain has 8 directories corresponding to the goals possible for the domain. These goals itself, contain directories for the 10 different world instances. Each goal for each world instance in a particular domain thus has a number of different human demonstrations, and these are saved in the form of a .datapoint file for each plan. This is a pickled instance of the Datapoint class found in `src/datapoint.py` and contains all the information needed about the plan. Refer to the [class](src/datapoint.py) for more information.

{% endcapture %}
{% capture summary %}Dataset{% endcapture %}{% include details.html %}

{% capture details %}
Please ensure that the dataset is downloaded before proceeding with this step.

All the trained models can be found [here](https://drive.google.com/open?id=1Kw65B55DehnteO1hwLUk0k1rWw2eCTl0). 

All the models mentioned in the paper can be trained through the command

```bash
$ python3 train.py $DOMAIN $TRAINING_TYPE $MODEL_NAME $EXEC_TYPE
```
Here DOMAIN can be home/factory.

TRAINING_TYPE can be as follows:

| TRAINING_TYPE                     | Meaning                     
| --------------------------------- | --------------------------- 
| **gcn**                           | Tool prediction model predicting most probable tool using inital state  
| **gcn_seq**                       | Tool sequence prediction model, which predicts the sequence of tools that will be used in the plan      
| **action**                        | Action prediction model which does not use the trained tool prediction model
| **action_tool**                   | Action prediction model which uses the trained tool prediction model

MODEL_NAME specifies the specific PyTorch model that you want to train. Look at `src/GNN/models.py` or `src/GNN/models.py` to specify the name. They are specified here for reference.

| MODEL_NAME                     | Name in paper                     
| -------------------------------| --------------------------- 
| **GGCN**                           | GGCN
| **GGCN_Metric**                    | GGCN+Metric
| **GGCN_Metric_Attn**               | GGCN+Metric+Attn
| **GGCN_Metric_Attn_L**             | GGCN+Metric+Attn+L    
| **GGCN_Metric_Attn_L_NT**          | GGCN+Metric+Attn+L+NT
| **GGCN_Metric_Attn_L_NT_C**        | GGCN+Metric+Attn+L+NT+C
| **GGCN_Metric_Attn_L_NT_C_W**      | GGCN+Metric+Attn+L+NT+C+W
| **Final_\***                       | These are ablated model with the best GGCN_Metric_Attn_L_NT_C_W model - the * component.

EXEC_TYPE can be as follows:

| EXEC_TYPE                         | Meaning                     
| --------------------------------- | --------------------------- 
| **train**                         | Train the model 
| **accuracy**                      | Determine the prediction accuracy for tool/action prediction model on the given dataset     
| **ablation**                      | Determine tool prediction accuracies for ablated models of the form Final_*
| **generalization**                | Calculate accuracies of all models on generalization test set
| **policy**                        | Run the action model for the given dataset and determine percentage task completion using the model as a policy in approximate simulated environment.

To train the best tool prediction model, use the following command
```bash
python3 train.py home gcn GGCN_Metric_Attn_L_NT_C train
```

To test the tool prediction accuracies of all ablated models, use the following command
```bash
python3 train.py home gcn GGCN ablation
```

To test the generalization accuracies of all models, use the following command
```bash
python3 train.py home gcn GGCN generalization
```

To train the best tool sequence prediction model, use the following command
```bash
python3 train.py home gcn_seq GGCN_Metric_Attn_L_NT_C train
```
{% endcapture %}
{% capture summary %}Training{% endcapture %}{% include details.html %}

## Supplementary Video

<p align="center">
<iframe width="800" height="450"
src="https://www.youtube.com/embed/1GVGcgoBpxg" 
frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen></iframe></p>

## License

BSD-2-Clause. 
Copyright (c) 2020, Rajas Basal, Shreshth Tuli, Rohan Paul, Mausam
All rights reserved.

See License file for more details.

## Cite this work
Paper available on <i>arxiv</i>: [http://arxiv.org/abs/2006.05478](http://arxiv.org/abs/2006.05478).
```
@article{bansal2020toolnet,
  title={ToolNet: Using Commonsense Generalization for Predicting Tool Use for Robot Plan Synthesis},
  author={Bansal, Rajas and Tuli, Shreshth and Paul, Rohan and Mausam},
  journal={arXiv preprint arXiv:2006.05478},
  year={2020}
}
```
