<a target="_blank" href="https://colab.research.google.com/github/filippodaniotti/DL-domain-adaptation/blob/master/domain_adaptation.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Unsupervised Domain Adaptation

In this notebook we will try to solve a domain adaptation task.

In particular we will be focues on the task of **unsupervised domain adaptation (UDA)**. 

Given a source labelled dataset and a target unlabelled dataset, we are tasked to find a model that perform well on the target unlabelled dataset.

Where $X_S = \{(x_1,y_1),(x_2,y_2)...(x_n,y_n)\}$ is the source dataset and $X_T = \{(x_1),(x_2)...(x_n)\}$ is the target unlabelled dataset.

More specifically the dataset tested is a subset of `Adaptiope`, a dataset specifically designed as a domain adaptation benchmark. 

We will be using only these labels:

```
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

and the testing will be limited to the domains of  ` product images ` and ` real word `. The ` synthetic ` domain will be ignored.

# Team

| First name | Last name | ID | Email | 
| ----- | ----- | --- | -------- |
| Michele | Yin | 229359 | michele.yin@studenti.unitn.it | 
| Giovanni | Ambrosi | 232252 | giovanni.ambrosi@studenti.unitn.it | 
| Filippo | Daniotti | 232087 | filippo.daniotti@studenti.unitn.it |

# How to run 
1. Make sure to check the `Configuration` cell
2. Ensure you have the `Adaptiope.zip` archive in the correct path
3. Run the setup cell groups:
    * initial setup
    * dataset preparation
    * data loaders
    * plotting
    * shared components
4. Run pretty much any cell you want

# Results

Check out [our notebook](https://colab.research.google.com/drive/1gHuVmc-eliiw63bhxs-GCMvgKh7kCt7W?usp=sharing) on Colab with cell outputs!

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
