# DFP
Code for Deep Feature Prompt

Datasets
====
You can access and download the data from the following links:

**TCGA-IDH**: Access from [Google Drive](https://drive.google.com/drive/folders/1jgTOKWLtPzsxLic51glabGZdc-4aTdmG?usp=sharing)

**UniToPath**: Access from [IEEE-DataPort](https://ieee-dataport.org/open-access/unitopatho)

**CAMELYON16**: Access from [Offical Site](https://camelyon16.grand-challenge.org/Data/)

**BRIGHT**: Access from [BRIGHT Challenge](https://www.synapse.org/Synapse:syn26480664/files/)

Pre-Process
====
For WSI pre-processing, we mainly focus on cropping the slides into patches and then compress patch images into features. Since **TCGA-IDH** and **UniToPath** already provide the cropped patches, we will skip this step for them. For **CAMELYON16** and **BRIGHT**, we follow [CLAM](https://github.com/mahmoodlab/CLAM) to perform the pre-processing. Example codes are provided:

```
python3 create_patches_fp.py \
--source $DATA_DIRECTORY \
--save_dir $RESULTS_DIRECTORY \
--patch_size 256 \
--patch 

python3 extract_features_fp.py \
--model_name ViT_S_16 \
--data_h5_dir $DIR_TO_COORDS \
--data_slide_dir $DATA_DIRECTORY \
--csv_path $CSV_FILE_NAME \
--feat_dir $FEATURES_DIRECTORY \
--batch_size 512 \
--slide_ext .tif
```

Stain Prototype Learning
====
```
python3 histo_ft_extract.py \
--image_size $SIZE \
--csv_path $CSV_PATH \
--feat_dir $FEATURES_DIRECTORY \
--slide_dir $DATA_DIRECTORY \
```

Based on the information (e.g., coordinates, h5 files, etc) provided in the csv file, running the above code will extract and store the patch-level colour histogram feature in FEATURES_DIRECTORY for slides in DATA_DIRECTORY. In detail, the code in **histo_ft_extract.py** adopts the codes from [Histogram loss](https://github.com/mahmoudnafifi/HistoGAN) from histogram feature extraction and uses agglomerative clustering algorithm to perform clustering.

DFP/DFP-Stain Training
====
We provide the training scripts


Trained Packages
====
We mainly provide benchmarks for TCGA_IDH and UniToPath, since these two datasets have fixed training and testing setups. For CAMELYON16 and BRIGHT, there are no fixed benchmarks due to the inconsistency in patch selection. 

| MIL Classifier | Feature Extractor | Dataset | Test acc. | Test f1 | MIL | Prompt | Stain Prototype |
|-------------------|-------------------|---------------------|--------------------|--------------------|--------------------|--------------------|
| CLAM |  ResNet50 |TCGA-IDH | 87.1% | 79.0% | [model](https://drive.google.com/file/d/1XN-jyzkBCiYMGUYNHMj3hwusx6ROwh_G/view?usp=sharing) |--------------------|--------------------|
| CLAM+DFP |  ResNet50 |TCGA-IDH  | 88.2% | 79.8% | [model](https://drive.google.com/file/d/1BjjxmuvIn23ZuLye52U0V3Xf3Q5rAbYX/view?usp=sharing) | --------------------|--------------------|
| CLAM+DFP-Stain |  ResNet50 |TCGA-IDH | 83.3%  | 69.4%| [model](https://drive.google.com/file/d/13-mWo2_VHvU8CE5ObCQm7Y76m9VXLvus/view?usp=sharing) |--------------------|--------------------|
| CLAM |  ResNet50 |UniToPath | 87.1% | 79.0% | [model](https://drive.google.com/file/d/1XN-jyzkBCiYMGUYNHMj3hwusx6ROwh_G/view?usp=sharing) |--------------------|--------------------|
| CLAM+DFP |  ResNet50 |UniToPath  | 88.2% | 79.8% | [model](https://drive.google.com/file/d/1BjjxmuvIn23ZuLye52U0V3Xf3Q5rAbYX/view?usp=sharing) | --------------------|--------------------|
| CLAM+DFP-Stain |  ResNet50 |UniToPath | 83.3%  | 69.4%| [model](https://drive.google.com/file/d/13-mWo2_VHvU8CE5ObCQm7Y76m9VXLvus/view?usp=sharing) |--------------------|--------------------|

Reference
