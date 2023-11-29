# Backdoor detector for BadNets
Designed a backdoor detector for BadNets trained on the YouTube Face dataset using the pruning defense. It is part of ECE-GY-9163 Machine Learning for Cybersecurity Lab 4.

### Author: 
Pratham Mehta (pm3483)

### Goal: 
Design a backdoor detector for BadNets trained on the YouTube Face dataset using the pruning defense.

## Directories present in this repository:
```bash
├── data 
    └── cl
        └── valid.h5 // this is clean validation data used to design the defense
        └── test.h5  // this is clean test data used to evaluate the BadNet
    └── bd
        └── bd_valid.h5 // this is sunglasses poisoned validation data
        └── bd_test.h5  // this is sunglasses poisoned test data
├── models
    └── bd_net.h5
    └── bd_weights.h5
├── architecture.py
└── eval.py // this is the evaluation script
└── repaired_model_2.h5 // (Model with 2% Threshold)
└── repaired_model_4.h5 // (Model with 4% Threshold)
└── repaired_model_10.h5 // (Model with 10% Threshold)
└── Lab4.ipynb // (Python Notebook)
```

## Dependencies
   1. Python 3.6.9
   2. Keras 2.3.1
   3. Numpy 1.16.3
   4. Matplotlib 2.2.2
   5. H5py 2.9.0
   6. TensorFlow-gpu 1.15.2

## Instructions to run this repository
1. Download the validation and test datasets from [here](https://drive.google.com/drive/folders/1Rs68uH8Xqa4j6UxG53wzD0uyI8347dSq?usp=sharing) and store them under `data/` directory.
2. The dataset contains images from YouTube Aligned Face Dataset. We retrieve 1283 individuals and split into validation and test datasets.
3. bd_valid.h5 and bd_test.h5 contains validation and test images with sunglasses trigger respectively, that activates the backdoor for bd_net.h5.

## Instructions for Executing Scripts
1. Detailed instructions for executing the pruning defense can be found outlined in a sequential process within the Python notebook.
2. The model weights for b_prime are saved in the main directory.

## RESULTS
### The Backdoor model which was Repaired
| Threshold | Channel Pruned | Clean Accuracy | Attack Success Rate |
|-----------|----------------|----------------|---------------------|
| 2         | 75% (45)       | 95.90          | 100.00              |
| 4         | 80% (48)       | 92.29          | 99.98               |
| 10        | 86.7% (52)     | 84.54          | 77.21               |

### Retrained Net
| Threshold | Channel Pruned | Clean Accuracy | Attack Success Rate |
|-----------|----------------|----------------|---------------------|
| 2         | 75% (45)       | 95.74          | 100.0               |
| 4         | 80% (48)       | 92.12          | 99.98               |
| 10        | 86.7% (52)     | 84.33          | 77.21               |

      
      E.g., `python3 eval.py data/cl/valid.h5 data/bd/bd_valid.h5 models/bd_net.h5`. This will output:
      Clean Classification accuracy: 98.64 %
      Attack Success Rate: 100 %

##  Important Notes
Please use only clean validation data (valid.h5) to design the pruning defense. And use test data (test.h5 and bd_test.h5) to evaluate the models. 
