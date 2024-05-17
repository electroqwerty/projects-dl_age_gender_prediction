### Project Overview:

The objective was to create a multitask learning model trained on the [UTKFaces dataset](https://www.kaggle.com/jangedoo/utkface-new). The classification goals were to predict the Age and Gender of individuals in the photographs. The dataset comprised over 23,000 images.

My multitask approach utilized **binary classification for gender** and **regression for age.** 

I manually curated the dataset, removed all outlier images. These **outliers included black and white photos, images not containing faces, incorrectly labeled photos, and some with severe distortion.**

Approximately 910 photos were removed during this process.

The pretrained model of choice was **ResNet18**. I did not opt for larger ResNet models due to my hardware limitations, although I believe more powerful models could yield significantly better predictions.

The challenging aspects of this project included:

- Addressing data imbalance in terms of Age and Race.
- Determining the best method to calculate total loss, considering the combination of regression with binary classification.
- Implementing the LIME explainer.

Attempts to over-sample minority classes through data augmentation resulted in decreased model performance, leading to the decision to utilize the raw data for the final model.

Overall, I am not entirely pleased with the results. Despite my efforts, I was unable to overcome certain limitations. Nevertheless, it was a complex and compelling project, marking my first try at multitask learning and the accompanying challenges.

### Explaining Some Project Requirements:

#### Model Bias:

From multiple runs of samples using LIME explainers, I did not observe any apparent bias in terms of gender or age.

Residual analysis indicated a tendency to predict younger ages for older individuals and vice versa. Given the suboptimal model performance, I would not consider these findings to be substantial concerns. More refinement of age predictions is necessary before properly evaluating bias. At this stage, predictions that seem somewhat random may not be truly indicative of bias.

#### Potential Scenarios of Model Bias:

If the model's dataset does not maintain proportional representation of all ages across genders and races, biases are likely to emerge.

Hence, model bias would mirror the biases present in the data. Addressing this issue is crucial for understanding any other potential biases in the model.

Racial biases for individuals with darker or lighter skin tones are conceivable, with the model potentially misinterpreting skin tone as too relevant feature for classification.

Such biases might be identified by examining the features the model focuses on for these specific demographic groups, using tools like LIME or other analytical methods.

#### Potential Deployment Domains (Assuming Optimal Model Functioning):

- Social media platforms could use it for automatic age identification.
- Content moderation systems could leverage it to identify minors in online content.
- Demographic analytics could employ it to survey social media profiles for demographic insights.

#### Domains Where Deployment Is Inadvisable:

- Real-time video feeds may not be suitable, depending on the exact nature of the requirements.
- Identity verification systems, as the model is not trained for individual face recognition but rather broader demographic features.
- Medical facial diagnosis or mood determination based on imagery, as the model is not designed for such specialized tasks.

----

#### Tensorboard logs and model names:


Explanation of tensorboard models.

*1. benchmark_classifier_regression/version_0* - totals loss calculated as simple sum of age and gender loss, no weights

Name of this model in the notebook: Benchmark model 1

*2. benchmark_classifier_regression/version_1* - same mode, asabove just have * 0.001 to age loss in order to compare them more intuitively.

Name of this model in the notebook: Benchmark model 2

*3. STROONG_second/version_0* - This is where AdamW instead of Adam was introduced, also lr was changed and weight decay was added.

STROONG_second/version_2 - another run of the same model.

Name of this model in the notebook: Benchmark model 3

*4.final_model_max_85_for_lime/version_1.* - The model I used in LIME with age limit to 85.

Download the face_classifier_logs.zip file. 

How to run (Code for terminal): `tensorboard --logdir "path to unziped file/face_classifier_logs`

After you run this, in terminal window you will have some localhost link available to click, example : http://localhost:6007/ or 6006 ..

Note: - I used (base) conda environment to run this in, environment might differ for you.

----
License: MIT License
