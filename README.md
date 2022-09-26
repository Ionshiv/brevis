# Specialised Extraction of Image Data featURes
## SEIDR - A BREVIS Derivative

This repository contains a project derived from Brevis at https://github.com/aktgpt/brevis. It contains the code developed for this article https://doi.org/10.1371/journal.pone.0258546 writteb ny Håkan Wieslander, Ankit Gupta, Ebba Bergman, Erik Hallström, and Philip J Harrison.

All credit for the original work to the highly skilled developers involved in that paper. 


The content and structure of the repo is given by the following: 

```sh
.
├── README.md
├── seidr
│   ├── data                : python scripts for loading the datasets required
│   ├── loss                : for loss functions not included in PyTorch
│   ├── model               : python scripts for the various neural networks
│   ├── test                : scripts requied when running the models in test mode
│   ├── train               : scripts requied when running the models in train mode
│   └── utils               : utility functions (e.g. for converting the images to numpy arrays for faster data loading)
│
├── configs                 : .json files for running the models to reconstruct the three fluorescence channels
│                       
└── exp_stats               : .csv files for image statistics and train/test splits 
    
```

The data should be structured as:
```sh
.
|--"Image-set"       :Base folder where images are stored
|   |-- "Input"      :What magnification the images are images at
    |-- "Target"           :where the nuclei masks are stored
        |-- "Target-overall"
            |-- "Target-nuclei"
```


## Data

Data for this project is named after the plate-experiment number, and is sectioned into [ROW] [COL] / [Channel]. Each Channel file is a time-lapse video.

## Training

To train the models, modify the content in the config file that you want to run. For instance change the path to the data under "data" - "folder" and the training validation and test splits csv files under "data" -- ""train_csv_file", "validation_csv_file" and "test_csv_file". You can also specify other things such as model configurations, optimizers, learning rate ...

To start training execute for instance for nuclei channel:
```sh
python3 -m seidr -c configs/nuclei_train.json 
```

## Inference

To run the pre-trained models on your own data, edit the config for the respective channel and put the `"run_mode"` to `"test"` and the path to the model in `"model_path"` in `"test"`. The data should be formatted in the same way as the mentioned on Data above. Then, to run the inference simply run the same command:
```sh
python3 -m seidr -c configs/nuclei_train.json 
```
