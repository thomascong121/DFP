# DFP
Code for Deep Feature Prompt

Training
====
For training the model, you may modify the `run.sh` file. Define `--data_folder` as the path to your dataset. We also provide our splits in the third section. To run, use `bash run.sh`

Testing
====
For testing the model, you may modify the `run.sh` file. Set `--resume` to True and define `--ckpt` as the path to your save model. To run, use `bash run.sh`

Trained Packages
====
We mainly provide benchmark for TCGA_IDH and UniToPath, since these two datasets have fixed training and testing setup. For CAMELYON16 and BRIGHT, there are no fixed benchmark due to the inconsistency in patch selection. 

| method | Dataset | Test acc. | Test f1 | url |
|-------------------|-------------------|---------------------|--------------------|--------------------|
| AdUni | ISIC2018 | 87.1% | 79.0% | [model](https://drive.google.com/file/d/1XN-jyzkBCiYMGUYNHMj3hwusx6ROwh_G/view?usp=sharing) |
| AdUni+upsample | ISIC2018 | 88.2% | 79.8% | [model](https://drive.google.com/file/d/1BjjxmuvIn23ZuLye52U0V3Xf3Q5rAbYX/view?usp=sharing) | 
| AdUni | APTOS2019 | 83.3%  | 69.4%| [model](https://drive.google.com/file/d/13-mWo2_VHvU8CE5ObCQm7Y76m9VXLvus/view?usp=sharing) |
| AdUni+upsample | APTOS2019 | 83.9% | 71.1% | [model](https://drive.google.com/file/d/1ceGo_NYSqmp4jdTWg-GWjnDNpTxnvdp7/view?usp=sharing) | 

Reference
