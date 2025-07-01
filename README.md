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

DFP/DFP-Stain Training
====
We provide the training scripts


Reference
====
