# SkimLit-NLP-project 🗒️ 
The purpose of this notebook is to build an NLP model to make reading medical abstracts easier.

The [paper](https://arxiv.org/abs/1612.05251) we're replicating.

## Introduction of paper
Over 50 million scholarly articles have been published , and the number of articles published every year keeps increasing .

Approximately half of them are biomedical papers. While this repository of human knowledgeabounds with useful information that may unlock new, promising research directions or provide conclusive evidence about phenomena, it has become increasingly difficult to take advantage of all available information due to its sheer amount. Therefore, a technology that can assist a user to quickly locate the information of interest is highly desired, as it may reduce the time required to locate relevant information.

> When researchers search for previous literature,for example, they often skim through abstracts in order to quickly check whether the papers match their criteria of interest. This process is easier when abstracts are structured, i.e., the text in an abstract is divided into semantic headings such as `objective`, `method`, `result`, and `conclusion`. However, a significant portion of published paper abstracts is unstructured, which makes it more difficult to quickly access the information of interest. Therefore, classifying each sentence of an abstract to an appropriate heading can significantly reduce time to locate the desired information.

## What you see in this notebook ?

we're going to be trying out a bunch of diffrent models and seeing which one works best.
### Model_0 : BaseLine
Using Sklearn algorithms to build our first model . (This is not a deep learning model)

### Model_1 : Conv_1D with token embeddings
In this section we use Custom `TextVectorization` and `Embedding` layer and on the top of their we use `Convolutional` layer

### Model_2 : Feature extraction with pretrained token embeddings
For model 2 we use `Transfer Learning` to embedd our Tokens and on the top of that we use `Dense` layer

### Model_3 : Conv1D with character embedding
For model 3 , we use same architecture as model 1but instead of Token level embedding we use `Character Level embedding` .
***
> **From Model_4 to Model_7 we use several `Inputs`**
***

### Model_4 : Combining pretrained token embeddings + characters embeddings (hybrid)
For model_4 we go through these steps:
1. Create a token-level embedding model ( similiar `model_1`)
2. Create a character-level model (similiar to `model_3` with a slight  modification)
3. Combine 1 & 2 with concatenate(`layers.Concatenate`)
4. Build a series of output layers on top of 3 similar to Figure 1 and section 4.2 of Paper
5. Construct a model which takes tokens and chareacter-level sequences as inputs and produces sequence label probaabilities as output

### Model_5 : Pretrained token embeddings + character embedding + positional embedding
For model_5 , we use same architecture as model 4 and we add positional embedding to our model
### Model_6 : Using `SGD optmizer`
The authors of the paper used `SGD optimizers` , but we use `Adam optimizer` until now , so we check SGD optimizer .

### Model_7:Using `Label Smoothing`
same as `Model_5` , but we use `Label Smoothing` 
***

This is the final results : 

|Model_number|Model_name |accuracy | precision | recall | f1 |
|-----|----|----|----|----|----|
|Model_0|baseline_sklearn|0.721832|0.718647	|0.721832|	0.698925|
|Model_1|Conv1D_with_Token_Embed	|0.787038|	0.784098|	0.787038|	0.784447|
|Model_2|Pretrained_Token_Embed_with_Dense_layer|	0.713855|	0.714906|	0.713855|	0.711193|
|Model_3|Conv1D_with_Character_Embed|	0.683470|	0.715132|	0.683470|	0.693729|
|Moedl_4|Pretrained_Token + Characters_Embed|	0.747683|	0.753959|	0.747683|	0.749550|
|Model_5|Pretrained_Token + Characters + Positional_Embed|	0.846452|	0.846454|	0.846452|	0.845990|
|Model_6|Pretrained_Token + Characters + Positional_Embed_with_SGD	0.525288|	0.404653|	0.525288|	0.446659|
|**Model_7**|**Pretrained_Token + Characters + Positional_Embed_with_Label_Smothing**|	**0.848504**|	**0.847811**|	**0.848504**|	**0.848004**|
***
Thanks to `Daniel brouke` and `ZeroToMastery`!
