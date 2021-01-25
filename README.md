# kitti_completion
Code based on the work done by `Revisiting Sparsity Invariant Convolution: A Network for Image Guided Depth Completion`.
See https://github.com/godspeed1989/kitti_completion

## KITTI training data
Download the [raw KITTI dataset](http://www.cvlibs.net/datasets/kitti/raw_data.php) for training. Removal of calibration files is not necessary as the /split .txt files coordinate input training data. The entire dataset has 225GB+.

Flags for training are contained in the options.py file
Default settings expect that .png was converted to .jpeg. KITTI is in .png. Set the -- png flag in the run command to switch to -- png.

## Generate KITTI Test Submission
```
python dump_test.py --weight_path weights.pth --data_path /path/to/dir/has/test_depth_completion_anonymous --dump
```
If you want to view results, remove `--dump` flag.

## Training
```
python train_v2.py --data_path /path/to/kitti --split full
```
The path containing KITTI datasets should be organized like this:
```
working_directory/kitti
    raw/
        2011_09_26/
            2011_09_26_drive_0001_sync/
                image_02/
                image_03/
    test_depth_completion_anonymous/
        image/
        velodyne_raw/
    val_selection_cropped/
        image/
        velodyne_raw/
        groundtruth_depth/
    data_depth_annotated
        e.g. 2011_09_26_drive_0001_sync (combined contents from train/val. Train/val are not separate folders anymore)
            proj_depth
                groundtruth
                    image_02
                    image_03
                velodyne_raw
                    image_02
                    image_03
    depth_selection

```
