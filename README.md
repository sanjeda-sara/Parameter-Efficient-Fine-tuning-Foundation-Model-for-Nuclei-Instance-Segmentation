# Parameter-Efficient-Fine-tuning-Foundation-Model-for-Nuclei-Instance-Segmentation


This repository has been created as a part of the Medical Image Computing course (CAP 5516), conducted by Dr. Chen Chen to present the thirst assignment of the Spring 2025 semester.

The repository contains the following:
               1. Complete Executing (.ipynb file)
               2. Project Report
               3. The "mobile_sam.pth" file which needs to be in the same directory as the main file to run this code

The dataset used in this project is publicly available at: https://www.kaggle.com/datasets/ipateam/nuinsseg 

#Description: 

The NuInsSeg dataset is a comprehensive and fully annotated collection designed for nuclei instance segmentation in H&E-stained histological images. Sourced from the NuInsSeg Kaggle repository, it consists of PNG image files and corresponding TIFF mask files, systematically organized by organ type. This dataset provides a valuable resource for evaluating segmentation models in histopathology.

The model utilized for this task is based on MobileSAM, a lightweight adaptation of the Segment Anything Model (SAM) that uses a TinyViT backbone. To enhance training efficiency and adapt the model to the dataset, LoRA (Low-Rank Adaptation) is employed. LoRA is selectively applied to all linear layers within the image encoder, enabling parameter-efficient fine-tuning. Meanwhile, the prompt encoder and original SAM weights remain frozen, except for the decoder and the LoRA-injected components. This configuration reduces the number of trainable parameters to approximately 4.18 million out of a total 10.25 million, which accounts for roughly 40.78% of the model's capacity.
The codebase features a custom data loader named NuInsSegDatasetFunction, which handles image resizing and normalization tailored to the segmentation task. Fine-tuning is achieved through the LoRALinearFunction, a custom module that wraps all nn.Linear layers in the SAM encoder for efficient adaptation. The training loop includes forward and backward passes with loss computation using BCEWithLogitsLoss, followed by optimization steps.
For post-processing, the watershed algorithm is applied to refine the segmentation masks and ensure clear instance separation. Model performance is evaluated using three key metrics: Dice Score, Aggregated Jaccard Index (AJI), and Panoptic Quality (PQ), providing a comprehensive assessment of segmentation accuracy and instance-level precision.

The code was executed for 5 epoch, 10 epoch and 20 epoch to see the outcome. More details are provided in the ".ipynb" file regarding the execution.
