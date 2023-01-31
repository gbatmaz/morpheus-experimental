# Morpheus Experimental

Morpheus Experimental is a staging/collaboration/experimental area for development. This directory contains prototypes of cybersecurity workflows and pipelines which are still being developed and are in the alpha testing stage.

Prototype contributions from the community are welcome. A prototype should include at minimum a tutorial-style notebook, model file, sample data, training script, inference script, and documentation. More information can be found in the [Contributing Guide](CONTRIBUTING.md).

## Getting Started

We recommend building morpheus experimental from source in an environment with a modern GPU with at least 16GB of memory.

### General Requirements
- Pascal architecture 16GB GPU or better
- [Git LFS](https://git-lfs.github.com/)
- [Jupyter](https://jupyter.org/install)


### Clone the Repository

```bash
MORPHEUS_EXPERIMENTAL_ROOT=$(pwd)/morpheus-experimental
git clone https://github.com/nv-morpheus/morpheus-experimental $MORPHEUS_EXPERIMENTAL_ROOT
cd $MORPHEUS_EXPERIMENTAL_ROOT
```

### Build Morpheus Experimental Container

To assist in building a Morpheus Experimental container, several scripts have been provided in the `./docker` directory. To build the "release" container, run the following:

```bash
./docker/build_container.sh
```

This will create an image named `nvcr.io/nvidia/morpheus/mor_exp:${MORPHEUS_EXPERIMENTAL_VERSION}-runtime` where `$MORPHEUS_EXPERIMENTAL_VERSION` is replaced by the output of `git describe --tags --abbrev=0`.

To run the built "release" container, use the following:

```bash
./docker/run_container.sh
```

You can specify different Docker images and tags by passing the script the `DOCKER_IMAGE_TAG`, and `DOCKER_IMAGE_TAG` variables respectively. For example, to run version `v22.09.00a` use the following:

```bash
DOCKER_IMAGE_TAG="v22.09.00a-runtime" ./docker/run_container.sh
```

### Prototype Specific Requirements
To get started with a specific prototype additional requirements must be installed into your environment. Each prototype directory contains its own `requirements.txt` file. 

```bash 
cd ${MORPHEUS_EXPERIMENTAL_ROOT}/${PROTOTYPE}
pip install -r requirements.txt
```

To run the morpheus pipeline for the prototype follow the instructions for setting up your morpheus environment found in the [main morpheus repo](https://github.com/nv-morpheus/Morpheus#getting-started-with-morpheus)


# Current Cybersecurity Workflow Prototypes

## [DGA Detection via AppShield](/appshield-dga-detection)
This model is a convolution neural network model trained to classify URL domains generated by Domain-Generation-Algorithms. Domain generation algorithms (DGA) are algorithms seen in various families of malware that are used to periodically generate a large number of domain names that can be used as rendezvous points with their command and control servers. Input data comes from AppShield.

## [Phishing URL Detection via AppShield](/phishing-url-detection)
This model is a binary classifier to label phishing URLs and non-phishing URLs obtained from host process data. Input data comes from AppShield.

## [String Resemblance Grouping](/string-resemblance-grouping)
This technique syntactically groups system log messages and finds group representatives for data exploration and triage.

## [Detection of Anomalous  authentication using Relational Graph Neural Network (RGCN)](/anomalous-auth-detection)
This model shows an application of a graph neural network for anomalous authentication detection in Azure-AD signon heterogeneous graph. An Azure-AD signon dataset  includes four types of nodes, authentication, user, device and service application nodes are used for modeling. A relational graph neural network (RGCN)is used to identify anomalous authentications from azure-ad signon input.

## [Asset Clustering using Windows Event Logs](/asset-clustering)
This model is a clustering algorithm to assign each host present in the dataset to a cluster based on aggregated and derived features from Windows Event Logs of that particular host.

# Repo Structure
Each prototype has its own directory that contains everything belonging to the specific prototype. Directories can include the following subfolders and documentation:

## models

Model files for public release (ONNX preferred to pytorch/tensorflow)

## datasets

Samples of training data and inference dataset with model output to be used to test training and inference scripts. Links to  publicly available datasets are also welcome.

## training-tuning

A script and python notebook showing how to train or fine-tune the model. The tutorial-style notebook takes sample training data file as an input and creates a model file. It is reliable and repeatable (ie. set seed values). If variables are used in script (ie. epochs, learning_rate) set defaults to those used to achieve metrics reported in documentation. It includes a `requirements.txt` file with dependencies and versions used for training. 

## inference

A non-morpheus pipeline script that contains data loading, preprocessing, model loading, inference, postprocessing, and serialized output file. It uses desired morpheus pipeline variables as input variables to the script (ie. threshold=0.6). It produces a reliable and repeatable output file from the inference dataset. It includes `requirements.txt` file with dependencies and versions used for non-morpheus inference.

## morpheus-pipeline (optional)
All the necessary files for a full Morpheus pipeline of the prototype similar to pipelines found in [Morpheus Examples](https://github.com/nv-morpheus/Morpheus/blob/-/examples) with it's own `requirements.txt` files. 

## model documentation

A README.md that contains the following information for each model:

 - **Model/prototype name** - Name of the model
 - **Use case** - Specific use case the model targets
 - **Version** - Version of the model (major.minor.patch)
 - **Model overview** - General description
 - **Model architecture** - General model architecture
 - **Requirements** - text file containing dependencies
 - **Training** - Training dataset and paradigm
 - **Training data** - description of training data
 - **Training epochs** - Number of epochs used during training
 - **Training batch size** - Batch size used during training
 - **GPU model** - Family of GPU used during training
 - **Training script** - How to run training script
 - **Model accuracy** - Accuracy of the model when tested (Precision, Recall, F1, etc)
 - **Memory footprint** - Memory required by the model
 - **How to use this model** - Circumstances where this model is useful
 - **Input data** - Typical data that is used as input to the model
 - **Output** - Type and format of model output
 - **Out-of-scope use cases** - Use cases not envisioned during development
 - **Ethical considerations** - Ethical analysis of risks and harms
 - **References** - Resources used in model development
 
