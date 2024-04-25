## About The Project

In this project, we use the Detectron 2 model and the cell nucleus dataset provided by Kaggle 2018 DataScienceBowl for the instance segmentation task. The dataset contains images of cells of different shapes and sizes, which are sampled at different microscope magnifications, light conditions, and staining methods. We chose MAP as the metric. We used the MAP achieved by the first place winner of the Kaggle competition and the Detectron 2 MAP values provided by Meta as the baseline, and the detailed analysis can be found in the report.[Report]()
Due to the computation limitation, I did this project on colab platform using T4 GPU.

<!-- GETTING STARTED -->

## Getting Started

Run the second cell to set up the environment for Detectron 2. It may take some time.

The dataset is converted to COCO Segmentation format by roboflow. [link](https://app.roboflow.com/ds/rMLP6Tydfk?key=SuzMFS2hUJ)
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
