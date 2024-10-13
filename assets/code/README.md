<h2 align="center">
  <b>Unsupervised Discovery of Object-Centric Neural Fields</b>
</h2>

---

## Installation
Please run `conda env create -f environment.yml` to install the dependencies.

## Datasets
We gathered four datasets (Room-Texture, Room-Furniture, Kitchen-Matte, Kitchen-Shiny) for evaluating uOCF, and a subset of Objaverse for learning object priors. The datasets are available at [link (Google Drive)](https://drive.google.com/drive/folders/1OCxKQZTsOwls7lFjdNdXAedeXkUHKqJO?usp=sharing).

Note that we need to generate a depth image for each input image, and the MiDAS depth estimator is used in our experiments. Refer to their repo[https://github.com/isl-org/MiDaS] for more details.

### Dataset organization

Each file begins with the prefix `{id:05d}_sc{scene_id:04d}_az{az_id:02d}`, and suffix includes `.png` for the image file, `_RT.txt` for the camera pose, and `_intrinsics.txt` for the camera intrinsics. The focal length and principal point are normalized, i.e., $f'_x = f_x / W, f'_y = f_y / H, c'_x = c_x * 2 / W - 1, c'_y = c_y * 2 / H - 1$, where $H$ and $W$ are the height and width of the image, respectively.

When running the scripts, please specify the path to the dataset by modifying the DATAROOT on the first line.

## Pretrained Models
We provide the pretrained models for uOCF. The models are available at [link (Google Drive)](https://drive.google.com/file/d/10fTKsUYy0poIexuRwZF2uHWlogz7vkSp/view?usp=sharing).

## Testing
To test the pretrained model, please run the following command:
```
bash scripts/DATASET-NAME/test-noplane.sh
```
where DATASET-NAME is one of (Room-Texture, Kitchen-Matte, Kitchen-Shiny).

## Training
(Optional, we have provided pre-trained checkpoints) Run the following command to train the model from stage 1
```
bash scripts/object-prior-learning/train-stage1-noplane.sh
```

Note that sometimes it yields undisired results (e.g., either the foreground or the background is totally black). If this happens after training for 1 epoch (~1000 iterations), you may stop the training and re-run the command.

Then run the following command to train the model from stage 2, note that Room-Furniture use the same stage 1 model as Room-Texture.
```
bash scripts/DATASET-NAME/train-stage2-noplane.sh
```
where DATASET-NAME is one of (Room-Texture, Kitchen-Matte, Kitchen-Shiny).




