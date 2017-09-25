![](https://s1.ax1x.com/2017/09/24/QzeaQ.png) <br>
# **Table Contents**
- **What is DeepRec** 
- **Data Format**
- **How to Use**
- **Benchmark Results**
- **References**

## What is DeepRec
DeepRec is a tool, which contains a variety of classic deep learning models, such as dnn, ipnn, opnn, deepWide, deepFM.We will continue to improve the tool.

## Data Format
The data format of LIBFFM is:
label  field1 : feature1 : value1  field2 : feature2 : value2...<br>
field and feature should be non-negative integers, **field index start by 1**, **feature index start by 1**
## How to Use
in order to use the tool, you just need to edit the configuration file.
for example:
```
git clone git@bitbucket.org:lujaindong/deeprec.git
cd deeprec/
cd config/
```
then you edit **network.yaml** based on your needs.
finally
```
python main.py
``` 
network.yaml for deepFM is as follows
``` 
#data
#data format:ffm
data:
     train_file  :  data/300w_train1_T4.process.ffm
     eval_file  :  data/300w_valid1_T4.process.ffm
     test_file  :  data/300w_test1_T4.process.ffm
     #infer_file  :  data/infer.entertainment.no_inter.norm.fieldwise.userid.txt
     FIELD_COUNT :  39
     FEATURE_COUNT : 255716
     data_format : ffm

#model
#model_type:deepFM or deepWide or dnn or ipnn or opnn or fm or lr
model:
    model_type : opnn
    dim : 10
    layer_sizes : [400, 400, 400]
    activation : [relu, relu, relu]
    dropout : [0.0, 0.0, 0.0]
#    load_model_name : ./checkpoint/epoch_1


#train
#init_method: normal,tnormal,uniform,he_normal,he_uniform,xavier_normal,xavier_uniform
train:
    init_method: tnormal
    init_value : 0.1
    embed_l2 : 0.0001
    embed_l1 : 0.0000
    layer_l2 : 0.0001
    layer_l1 : 0.0000
    learning_rate : 0.001
    loss : log_loss
    optimizer : adam
    epochs : 6
    batch_size : 4096

#show info
#metric :'auc','logloss', 'group_auc'
info:
    show_step : 10
    save_epoch : 4
    metrics : ['auc','logloss']
```
[parameter description](https://github.com/lu-jian-dong/learngit/wiki/Parameter-Description)
 
## Benchmark Results
our benchmark data is part of data which sample 300w from criteo dataset([dataset](https://www.kaggle.com/c/criteo-display-ad-challenge)), dealing with long tail features and continuous features

model | logloss | train time per epoch/s|
----|------|------| 
lr | 0.4702 | 81.9| 
fm | 0.4602 | 96.8 |   
dnn | 0.4562 | 458.0 |  
ipnn | 0.4549 | 452.6 |  
opnn | 0.4542 | 452.5 |  
deepWide | 0.457 | 467.1 | 
deepFM | 0.4559 | 769.9 | 
## References
- [A Factorization-Machine based Neural Network for CTR Prediction](https://arxiv.org/abs/1703.04247)
- [Deep Learning over Multi-field Categorical Data: A Case Study on User Response Prediction](https://arxiv.org/abs/1601.02376)
- [Product-based Neural Networks for User Response Prediction](https://arxiv.org/abs/1611.00144)
- [Wide & Deep Learning for Recommender Systems](https://arxiv.org/abs/1606.07792)
- [product-nets](https://github.com/Atomu2014/product-nets)

