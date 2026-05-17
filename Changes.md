# Changes
To use the model we forked the VirConv GitHub repository and made several changes to it.

The first modification was to change the models to output detection boxes for three classes.
The model configurations are stored in yaml files in root/tools/cfgs/models/kitti. 
Here were originally three files for the three variants, but these were only configured for single class 'Car' detections. 
We added three more yaml files with the appendage `_c3` to enable detection of three classes: 'Car', 'Pedestrian', 'Cyclist'.

The second change was to take the GitHub repository of the DMD³C model and import it to the root/tools folder. 
Here, in the root/tools/DMD3C folder, we created a new script `generateDepthPoints.py` which uses the DMD³C model to generate virtual points. 
In making this we instructed the LLM that wrote it to use the DMD³C model in the same way the PENet model was used in the VirConv paper, sharing the same functions and structure.
This code was reviewed by a human and tested to make sure it worked as intended.

In testing the input and layer StVD, the discard rates are controlled in the yaml files, but we simply used the `--set` command argument in the `train.py` script to adjust the discard rates on the fly.
`--set DATA_CONFIG.INPUT_DISCARD_RATE XX` and `--set MODEL.BACKBONE_3D.LAYER_DISCARD_RATE XX`.
Of note is that this `--set` argument must be placed last when running the commands, after all the other arguments.
