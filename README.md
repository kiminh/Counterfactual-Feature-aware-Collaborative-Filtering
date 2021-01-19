# [Code Submission] Neural Feature-aware Recommendation with Signed Hypergraph Convolutional Network



![image](https://github.com/code4review/TOIS/raw/master/img/intro.png)

## Requirements

- Python 3.6.9
- PyTorch 1.4.0 + cuda 10 
- numpy 1.16


## Project Structure

    .
    |-- __init__.py
    |-- data               # the directory of dataset:  the preprocessed Amazon Dataset, please contact xk18@mails.tsinghua.edu.cn to get the dataset
    |-- data_loader.py     # the dataloader class of our amazon dataset with textual feature 
    |-- main.py            # the training logic of our CFCF method. change the anchor_model as 1|2|3|4|5 to change to different logic
    |-- model              # the model directory. contain anchor model and the intervener model
    |   |-- CounterFea.py (deprecated)
    |   |-- IF_Qua.py
    |   |-- UF_Att.py
    |   |-- __init__.py
    |   |-- anchor_model.py # the f model in our paper
    |   `-- intervention_model.py # counter factual sample method
    |-- run_uif_matrix.py  
    `-- utils
        |-- QPC.py
        `-- eval.py       # inference code 

## Data Structure
download our dataset and unzip it in ./data/ directory.

data directory will like following: 

    data
    |-- Amazon_Instant_Video
        |-- Amazon_Instant_Video.formated
        |-- anchor.ptr
        |-- anchor_best.ptr
        |-- anchor_best43.ptr
        |-- anchor_best53.ptr
        |-- anchor_best_45.ptr
        |-- feature_id_dict
        |-- id_feature_dict
        |-- id_item_dict
        |-- id_user_dict
        |-- item_feature_quality_matrix
        |-- item_id_dict
        |-- predicted_item_feature_quality
        |-- predicted_user_feature_attention
        |-- sorted_ided_dataset
        |-- statistics
        |-- test_compute_user_items_dict
        |-- test_data
        |-- test_ground_truth_user_items_dict
        |-- train_data
        |-- train_user_negative_items_dict
        |-- train_user_positive_items_dict
        |-- user_feature_attention_matrix
        `-- user_id_dict
    |-- __init__.py
    |-- dataset_process.py
    |-- dataset_process_1.py

## Usage

1. Install all the required packages

2. Unzip the dataset in ./data directory and check every file is exists.

3. Run 
```
python main.py data_path=./data/Amazon_Instant_Video anchor_model=1  # train the anchor model and save it
mv ./data/Amazon_Instant_Video/anchor.ptr ./data/Amazon_Instant_Video/anchor_best.ptr  # change name of saved model to 'anchor_best.ptr'
python main.py data_path=./data/Amazon_Instant_Video anchor_model=2  # generate the counterfactual sample and finetune the anchor model (Raw CF model)
```