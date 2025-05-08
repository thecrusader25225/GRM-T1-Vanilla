# GRM-T1-Vanilla

## Setup installation

### 1. Install miniconda

follow miniconda docs

### 2. Activate conda environment
```shell
conda create --name gauge_reader python=3.8 -y
conda activate gauge_reader
```

### 3. Install Poetry

```shell
curl -sSL https://install.python-poetry.org | python -
```

### 4. Install the project dependencies

```shell
poetry install
```

### 5. Install pytorch

We use torch version 2.0.0.

```shell
conda install pytorch==2.0.0 torchvision==0.15.0 torchaudio==2.0.0 -c pytorch -c nvidia
```

### 6. Install mmocr

Refer to this page for installation <https://mmocr.readthedocs.io/en/dev-1.x/get_started/install.html>
We use the version dev-1.x

```shell
pip install -U openmim
mim install mmengine==0.7.2
mim install mmcv==2.0.0
mim install mmdet==3.0.0
mim install mmocr==1.0.0
```

We use the following versions: mmocr 1.0.0, mmdet 3.0.0, mmcv 2.0.0, mmengine 0.7.2.
If for some reason the installation fails refer to https://github.com/open-mmlab/mmcv/issues/2938.
We found that it is essential that we have Pytorch version 2.0.0

### 7. Install yolov8

We use ultralytics version 8.0.66

```shell
pip install ultralytics
```

### 8. Install sklearn

We use scikit-learn version 1.2.2

```shell
pip install -U scikit-learn
```

### 9. Run pipeline script

The pipeline script can be run with the following command:

```shell
python app/pipeline.py --detection_model app/models/gauge_detection_model.pt --segmentation_model app/models/segmentation_model.pt --key_point_model app/models/key_point_model.pt --base_path output --input uploads --debug --eval
```

For the input you can either choose an entire folder of images or a single image. Both times the result will be saved to a new run folder created in the `base_path` folder. For each image in the input folder a separate folder will be created.

In each such folder the reading is stored inside the `result.json` file. If there is no such reading, one of the pipeline stages failed before a reading could be computed. Best check the log file which is saved inside the run folder, to see where the error came up. There will also be a `error.json` file saved to the image folder, which computes some metrics to check without any labels how good our estimate is.

Additionally if the `debug` flag is set then the plots of all pipeline stages will be added to this folder. If the `eval` flag is set then there will also be a `result_full.json` file created. This file contains the data of the individual stages of the pipeline, which is used when evaluating in the script `full_evaluation.py`.

## Acknowledgments

This project uses the following open-source software:

- [analog_gauge_reader](https://github.com/mauritsreitsma/analog_gauge_reader) licensed under the [MIT License](https://opensource.org/licenses/MIT).
