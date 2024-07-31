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
|-------------------|-------------------|---------------------|--------------------|--------------------|--------------------|--------------------|--------------------|
| CLAM |  ResNet50 |TCGA-IDH | 79.2% | 78.5% | [model](https://drive.google.com/file/d/1F4cKGE0q35l_iEfd2vk1E6WrQBMdoO_R/view?usp=drive_link) |--------------------|--------------------|
| CLAM+DFP |  ResNet50 |TCGA-IDH  | 80.5% | 80.0% | [model](https://drive.google.com/file/d/1_QK2fdYR_Sw8FtaK2PA6j6092hvxXbVP/view?usp=drive_link) | [prompt](https://drive.google.com/file/d/1lm7Kp9ma95kkXJ89VXYyhQhlbNnPztFl/view?usp=drive_link)|--------------------|
| CLAM+DFP-Stain |  ResNet50 |TCGA-IDH | 81.2%  | 80.5%| [model](https://drive.google.com/file/d/1cvw7YRVB5yEiiIO_9rAWxiM0vYEkCdSX/view?usp=drive_link) |[prompt](https://drive.google.com/file/d/1AvbP_C9AkwCaqCJ-jm1oXfhN8w2hWeUD/view?usp=drive_link)|[prototype](https://drive.google.com/file/d/1RxLHPjuKK7xeu7mUuVstT8mhHk_fQpBU/view?usp=drive_link)|
| CLAM |  ResNet50 |UniToPath | 68.1% | 51.5% |[model](https://drive.google.com/file/d/107WFwhmRdlFQgRR0ejYSOyuqeJR6NO-u/view?usp=drive_link) |--------------------|--------------------|
| CLAM+DFP |  ResNet50 |UniToPath  | 70.5% | 55.4% | [model](https://drive.google.com/file/d/19_bcVjNwuYTNKCReJ-7Ep6zNXJcqmfCx/view?usp=drive_link) | [prompt](https://drive.google.com/file/d/1W-_TOkDb5mtQv2Z8UjzLtN0zDhLbNPIv/view?usp=drive_link)|--------------------|
| CLAM+DFP-Stain |  ResNet50 |UniToPath | 70.5%   | 59.0%| [model](https://drive.google.com/file/d/1cvw7YRVB5yEiiIO_9rAWxiM0vYEkCdSX/view?usp=drive_link) |[prompt](https://drive.google.com/file/d/1AvbP_C9AkwCaqCJ-jm1oXfhN8w2hWeUD/view?usp=drive_link)|[prototype](https://drive.google.com/file/d/1h92RKLoMcTdI3uWO4inb1m1iFtz-xRJt/view?usp=drive_link)|

| MIL Classifier | Feature Extractor | Dataset | Test acc. | Test f1 | MIL | Prompt | Stain Prototype |
|-------------------|-------------------|---------------------|--------------------|--------------------|--------------------|--------------------|--------------------|
| CLAM |  ViT_S_16 |TCGA-IDH | 79.1% | 78.5% |[model](https://drive.google.com/file/d/1wVRJYmfsJ1GIP095KKgosUi6fzhEsQbS/view?usp=drive_link) |--------------------|--------------------|
| CLAM+DFP |  ViT_S_16 |TCGA-IDH  | 80.5% | 79.8% | [model](https://drive.google.com/file/d/1qzDmbg6BYO0W3W4QP-xjRIWDzNxxCEI-/view?usp=drive_link) | [prompt](https://drive.google.com/file/d/1QRmSmQTT_d_la7X8KnzZRSGrFLWQygyZ/view?usp=drive_link)|--------------------|
| CLAM+DFP-Stain |  ViT_S_16 |TCGA-IDH | 80.5%|80.0%|[model](https://drive.google.com/file/d/1tQAZk_HNfvPqELNkodEq3ExGr2vmKbl4/view?usp=drive_link) |[prompt](https://drive.google.com/file/d/1dykDMLCPT8cdAwT6a5LvOkzYrR_nPuwG/view?usp=drive_link)|[prototype](https://drive.google.com/file/d/1RxLHPjuKK7xeu7mUuVstT8mhHk_fQpBU/view?usp=drive_link)|
| CLAM |  ViT_S_16 |UniToPath | 62.5% | 46.7% |[model](https://drive.google.com/file/d/1-kGRIESZvFVkZNeJJKHTDWLOOIWK2eBH/view?usp=drive_link) |--------------------|--------------------|
| CLAM+DFP |  ViT_S_16 |UniToPath  | 69.3% | 60.9% | [model](https://drive.google.com/file/d/1iJGznj6vwdl7pLFl0d9Vsg9mikveg6BQ/view?usp=drive_link) | [prompt](https://drive.google.com/file/d/1vhoHKxmg_V-9hs2dhlPPxckNVLT0w2na/view?usp=drive_link)|--------------------|
| CLAM+DFP-Stain |  ViT_S_16 |UniToPath |70.5%|63.4%|[model](https://drive.google.com/file/d/1awBNjA0um3DOVdOvfPU8KSO1j40TM6KY/view?usp=drive_link) |[prompt](https://drive.google.com/file/d/1NJ0FVdxKpqmVkVAntkg6BTtGjinc2E6r/view?usp=drive_link)|[prototype](https://drive.google.com/file/d/1h92RKLoMcTdI3uWO4inb1m1iFtz-xRJt/view?usp=drive_link)|

Reference
