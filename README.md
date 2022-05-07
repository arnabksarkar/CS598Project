# mimic-lstm

We are re-using the same code from this github branch. 

<a href="https://zenodo.org/record/1473691#.YlsZopPMJz9">Original repository</a>

<a href="https://zenodo.org/badge/latestdoi/155128190"><img src="https://zenodo.org/badge/155128190.svg" alt="DOI"></a>

This is a complete preprocessing, model training, and figure generation repo for "An attention based deep learning model of clinical events in the intensive care unit"

### Presentation
https://youtu.be/6lB1NkOd1HU

### Prerequisites
This repo requires the jupyter-notebook to be installed. Also, it would be easier to run this code using a mini-conda environment.  
Conda is not a required prerequisite, however it is recommended.

While using conda please use the `environment.yml` file to generate the conda environment. 

    conda env create -f environment.yml

For Mimic data, please get access by following instructions on Physionet website.

The pad_sequences.py file is required for rnn_mimic.py functionality. Additionally, the attention function adapted from Philippe Remy's Github has been cloned as attention_function.py and is required for the build_model function in rnn_mimic.py which assembles the LSTM-RNN with attention. All LSTM-RNNs were constructed in Tensorflow using the Keras API. Sklearn was used for validation metrics such as the AUROC. Numpy and Pandas libraries were required for table and matrix manipulation. 

### Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

#### Preprocessing Data

To begin, clone the mimic-lstm repository. Within the repository, create a folder called, "mimic_database" where the MIMIC-III will live. 
Then, request access from https://mimic.physionet.org/gettingstarted/access/, complete the required training course, and request the access to MIMIC-III. Download all MIMIC-III CSVs to "./mimic_database".

process_mimic.py contains classes for transforming the MIMIC-III tables into a pandas dataframe with the required feature columns. Specifically, the MimicParser class will provide all required methods for this operation. Moreover, the exact methods required to build the dataframe are listed at the bottom of the script. In order for this script to function, a number of dependencies are required and listed below. The "./mimic_database" folder will require a './mimic_database/mapped_elements" folder inside of it for the production of MIMIC-III dataframe intermediates. The MimicParser sequentially moves through tables of the MIMIC-III adding pieces of what is required. Not all MimicParser methods are required for operation.

#### Train Model
1. Team29_rnn_mimic_py39.py contains classes for transforming the pandas dataframe into a 3rd order tensor (batch_size, time_steps, features). It will require pad_sequences as an included dependency. the pickle_objects method will create training sets for vancomycin, sepsis, and MI. The train models will generate the models required for all figures. 
2. Team29_rnn_mimic_gru.py contains exact replica of Team29_rnn_mimic_py39.py class except it has GRU instead of LSTM to train the model.  
#### Evaluation
Models and figures are generated in the .ipynb notebook. Simply adjusting the target to 'MI', 'Sepsis', or 'Vancomycin' will generate the figures panels and images required for each part of the figure.





