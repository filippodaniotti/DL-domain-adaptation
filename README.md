<a target="_blank" href="https://colab.research.google.com/github/filippodaniotti/DL-domain-adaptation/blob/master/notebooks/domain_adaptation.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Unsupervised Domain Adaptation

In this project we will try to solve a domain adaptation task. 

In particular, we will be focues on the task of **unsupervised domain adaptation (UDA)**.  Given a source labelled dataset and a target unlabelled dataset, we are tasked to find a model that perform well on the target unlabelled dataset. More formally, we call $X_S = \{(x_1,y_1),(x_2,y_2)...(x_n,y_n)\}$  the source dataset and $X_T = \{(x_1),(x_2)...(x_n)\}$  the target unlabelled dataset.

More specifically the dataset tested is a subset of [Adaptiope](https://openaccess.thecvf.com/content/WACV2021/papers/Ringwald_Adaptiope_A_Modern_Benchmark_for_Unsupervised_Domain_Adaptation_WACV_2021_paper.pdf), a dataset specifically designed as a domain adaptation benchmark. We will be using only these labels:

```python
[
    "backpack",
    "bookcase", 
    "car jack", 
    "comb", 
    "crown", 
    "file cabinet", 
    "flat iron", 
    "game controller", 
    "glasses", 
    "helicopter", 
    "ice skates", 
    "letter tray", 
    "monitor", 
    "mug", 
    "network switch", 
    "over-ear headphones", 
    "pen", 
    "purse", 
    "stand mixer", 
    "stroller"
]
```

and the testing will be limited to the domains of ` product images ` and ` real word `. The ` synthetic ` domain will be ignored.

# Team

| First name | Last name | ID | Email | 
| ----- | ----- | --- | -------- |
| Michele | Yin | 229359 | michele.yin@studenti.unitn.it | 
| Giovanni | Ambrosi | 232252 | giovanni.ambrosi@studenti.unitn.it | 
| Filippo | Daniotti | 232087 | filippo.daniotti@studenti.unitn.it |

# Notebooks
In the [notebooks](notebooks/) directory you will find two items:
* [domain_ataptation.ipynb](notebooks/domain_adaptation.ipynb): contains the delivered code for the actual project; you can also access [here](https://colab.research.google.com/drive/1gHuVmc-eliiw63bhxs-GCMvgKh7kCt7W?usp=sharing) as read-only the working copy we used in our drive
* [scrapped_approaches.ipynb](notebooks/scrapped_approaches.ipynb): contains some code we wrote but later scrapped from the main notebook 

## How to run 
This instructions refer only to the [domain_ataptation.ipynb](notebooks/domain_adaptation.ipynb) notebook
1. Make sure to check the `Configuration` cell
2. Ensure you have the `Adaptiope.zip` archive in the correct path (get it [here](https://gitlab.com/tringwald/adaptiope))
3. Run the setup cell groups:
    * initial setup
    * dataset preparation
    * data loaders
    * plotting
    * shared components
4. Run pretty much any cell you want

If you want to load the serialized weights from our experiments:
1. Copy the weights from the [`trained_models`](trained_models/) directory to any directory in your environment, e.g. `weights/`
2. Set the appropriate `MODELS_BASEPATH` constant in the `Configuration` cell, e.g. `gdrive/MyDrive/weights`
3. Then, say that you want to load and thest the $P \rightarrow R$ of the `Self Supervision`
   - go to the `Finetune ResNet18 on P -> R` cell under the `Self Supervision` block
   - run the `Load` cell block
   - now you will have the weights in your gdrive working directory
   - try to run the `Test` cell group to see the results

# Results

In the following table you can find a recap of the accuracy values we achieved from our experiments.

We highly suggest to check out the [domain_ataptation.ipynb]([notebooks/domain_adaptation.ipynb](https://colab.research.google.com/drive/1gHuVmc-eliiw63bhxs-GCMvgKh7kCt7W?usp=sharing)) notebook to see all the plots we used for the evaluation. In particular, you will find:
* t-SNE plots
* Confusion matrices
* Error images
* Class-wise confidence value on predictions

| Model       | R -> P      | P -> R      | Absolute Gain R->P | Absolute Gain P->R | Percentage Gain P | Percentage Gain R |Upper Bound P | Upper Bound R| 
| ----------- | ----------- | ----------- | ---------- | ---------- |  ---------- | ---------- |  ---------- | ---------- | 
| Source Only      | 93.00       | 73.00       | --- ( max 3.00)| --- (max 18.25) | --- | --- |96.00 | 91.25 |
| Masked Image      | 89.00       | 73.75       |- 4.00 | 0.75 | - 133 %| 4 %|
| MMD      | 93.00       | 80.25       | 0.00 | 7.25| 0 % | 40 % |
| CORAL      | 89.75       | 81.00       | - 3.25 | 8.00| - 108 %| 44 %|
| LMMD      | 95.00       | 85.00       | 2.00 | 12.00| 66 % | 66 % |
| Confidence Label Coral   | 95.25        | 84.50       |2.25 | 12.25|  75 % | 64 %|
| Confidence Triplet Margin Distance  | 94.00        | 82.75      | 1.00 | 10.25| 33 %| 53 %|
| LMMD over multiple layers  | 95.75        | **88.00**       | 2.75| **15.00** | 92 %| 82 %|
| Confidence Label Coral over multiple layers  | **96.00**        | 87.75       | **3.00**| 14.75 | 100 %| 81 %|
| DANN  | 93.75        | 77.50   | 0.75 | 4.50 | 25 % | 25 %|
| ADDA  | 87.75        | 83.75   | -5.75 | 10.75 | - 158 % | 70 %|
| ADDA Symmetric  | 94.50        | 84.50   | 1.50 | 11.50 | 92 % | 60 %|
| Data augmented Confidence Label Coral over multiple layers  | 95.25        | 86.50   | 2.25 | 12.25 | 92 % | 74 %|
| Data augmented DANN  | 93.00        | 73.50   | 0.00 | 0.50 |  % |  %|
| Data augmented ADDA Symmetric  | 94.00        | 84.25   | 1.00 | 11.25 |  % |  %|
| Self-Supervised  | 93.50        | 78.75   | 0.50 | 5.75 | 16 % | 32 %|
| Self-Supervised Distribution Alignment  | 93.50        | 78.75   | 0.50 | 5.75 | 16 % | 32 %|
