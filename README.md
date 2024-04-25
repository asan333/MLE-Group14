## About The Project

In this project, we use the Detectron 2 model and the cell nucleus dataset provided by Kaggle 2018 DataScienceBowl for the instance segmentation task. The dataset contains images of cells of different shapes and sizes, which are sampled at different microscope magnifications, light conditions, and staining methods. We chose MAP as the metric. We used the MAP achieved by the first place winner of the Kaggle competition and the Detectron 2 MAP values provided by Meta as the baseline, and the detailed analysis can be found in the report. [Report]()

Due to the computation limitation, I did this project on colab platform using T4 GPU.

<!-- GETTING STARTED -->

## Getting Started

Run the second cell to set up the environment for Detectron 2. It may take some time.

The dataset is converted to COCO Segmentation format by roboflow. [link](https://app.roboflow.com/ds/rMLP6Tydfk?key=SuzMFS2hUJ)

## Approach

To begin, the dataset was preprocessed and transformed into a COCO dataset. The model was trained within the Detectron2 framework, utilizing the Mask R-CNN framework with ResNet-50 plus FPN as the base network. To accelerate the initial learning process and enhance model performance, pre-training weights provided by Detectron2 were used for model initialization. Throughout the training process, various hyper-parameters were configured, including an initial learning rate of 0.0025, an SGD optimizer with a momentum of 0.9, and a learning rate tuning strategy with gradual decay. Periodic model evaluations were conducted using COCO Evaluator, assessing Average Precision (AP) and Intersection over Union Ratio (IoU). Furthermore, test-time augmentation (TTA) was implemented to assess model performance under diverse data augmentation conditions and ensure result stability and reliability.


## Results

The performance of the model is shown in table below. The model is strong in segmenting nuclei, especially when it comes to an IoU of 0.50, where the AP reaches 73.776%, indicating a high level of segmentation capability. However, as the conditions become more strict, such as under IoU=0.75, the AP drops to 55.046%, suggesting that while the model is effective in localizing and segmenting nuclei, its precision in capturing edge details needs improvement. This may be due to the model's insufficient refinement for edge segmentation and limited training epochs due to computational constraints; increasing the number of training epochs might help address this issue.

### Bbox Metrics

| Metric | IoU       | Area   | MaxDets | Value |
|--------|-----------|--------|---------|-------|
| AP     | 0.50:0.95 | all    | 100     | 0.485 |
| AP     | 0.50      | all    | 100     | 0.738 |
| AP     | 0.75      | all    | 100     | 0.551 |
| AP     | 0.50:0.95 | small  | 100     | 0.437 |
| AP     | 0.50:0.95 | medium | 100     | 0.775 |
| AP     | 0.50:0.95 | large  | 100     | -1.000|
| AR     | 0.50:0.95 | all    | 1       | 0.018 |
| AR     | 0.50:0.95 | all    | 10      | 0.170 |
| AR     | 0.50:0.95 | all    | 100     | 0.530 |
| AR     | 0.50:0.95 | small  | 100     | 0.484 |
| AR     | 0.50:0.95 | medium | 100     | 0.813 |
| AR     | 0.50:0.95 | large  | 100     | -1.000|

### Setm Metrics
| Metric | IoU       | Area   | MaxDets | Value |
|--------|-----------|--------|---------|-------|
| AP     | 0.50:0.95 | all    | 100     | 0.492 |
| AP     | 0.50      | all    | 100     | 0.738 |
| AP     | 0.75      | all    | 100     | 0.550 |
| AP     | 0.50:0.95 | small  | 100     | 0.444 |
| AP     | 0.50:0.95 | medium | 100     | 0.789 |
| AP     | 0.50:0.95 | large  | 100     | -1.000|
| AR     | 0.50:0.95 | all    | 1       | 0.018 |
| AR     | 0.50:0.95 | all    | 10      | 0.171 |
| AR     | 0.50:0.95 | all    | 100     | 0.537 |
| AR     | 0.50:0.95 | small  | 100     | 0.492 |
| AR     | 0.50:0.95 | medium | 100     | 0.816 |
| AR     | 0.50:0.95 | large  | 100     | -1.000|


Furthermore, APl is NaN, indicating a lack of large-sized target samples in the dataset. Comparing APs and APm reveals that the model performs most effectively on medium-sized nuclei but is less accurate on smaller objects. This discrepancy may be due to a scarcity of small-sized targets in the training samples or inadequate capture of details by the model's feature extraction layer.

Although our model's MAP score doesn't reach 0.63164, its performance (a MAP score of 0.492) can be ranked within the top 20% of submissions on the leaderboard.

### COCO Instance Segmentation Baselines with Mask R-CNN

| Name    | lrsched | traintime (s/iter) | inferencetime (s/im) | trainmem (GB) | boxAP | maskAP |
|---------|---------|--------------------|----------------------|---------------|-------|--------|
| R50-C4  | 3x      | 0.575              | 0.111                | 5.2           | 39.8  | 34.4   |
| R50-FPN | 3x      | 0.261              | 0.043                | 3.4           | 41.0  | 37.2   |

Additionally, Meta provides the baseline for the Mask R-CNN model, shown in table above. The R50-FPN model achieves a boxAP of 41.0 and a maskAP of 37.2. Upon comparison with table below, we can see that the model achieves a boxAP of 48.462 and a maskAP of 49.211, surpassing the baseline metrics.

### Bbox and Segm AP of the Model

| Name | AP     | AP50   | AP75   | APs    | APm    | APl |
|------|--------|--------|--------|--------|--------|-----|
| Bbox | 48.462 | 74.751 | 55.144 | 43.714 | 77.452 | nan |
| Segm | 49.211 | 73.776 | 55.046 | 44.371 | 78.880 | nan |


## License

Distributed under the MIT License. See `LICENSE` for more information.

<!-- ACKNOWLEDGEMENTS -->

## Acknowledgements

* [Vincent Bindschaedler](https://www.cise.ufl.edu/bindschaedler-vincent/)
* [Detectron 2](https://github.com/facebookresearch/detectron2)
* [RoboFlow](https://github.com/roboflow/notebooks)
* [Detectron 2 Tutorial](https://www.youtube.com/watch?v=R-N-YXzvOmY&ab_channel=DigitalSreeni)
* [RoboFlow Detectron 2 Tutorial](https://github.com/roboflow/notebooks/blob/main/notebooks/train-detectron2-segmentation-on-custom-data.ipynb)
* [Detectron 2 Baseline](https://github.com/facebookresearch/detectron2/blob/main/MODEL_ZOO.md)

## Thank you
