# MimicGen

<p align="center">
  <img width="95.0%" src="docs/images/mimicgen.gif">
</p>

This repository contains the official release of data generation code, simulation environments, and datasets for the [CoRL 2023](https://www.corl2023.org/) paper "MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations". 

The released datasets contain over 48,000 task demonstrations across 12 tasks and the MimicGen data generation tool can create as many as you'd like.

Website: https://mimicgen.github.io

Paper: https://arxiv.org/abs/2310.17596

Documentation: https://mimicgen.github.io/docs/introduction/overview.html

For business inquiries, please submit this form: [NVIDIA Research Licensing](https://www.nvidia.com/en-us/research/inquiries/)

-------
## Latest Updates
- [07/09/2024] **v1.0.0**: Full code release, including data generation code
- [04/04/2024] **v0.1.1**: Dataset license changed to [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/), which is less restrictive (see [License](#license))
- [09/28/2023] **v0.1.0**: Initial code and paper release

-------

## Useful Documentation Links

Some helpful suggestions on useful documentation pages to view next:

- [Getting Started](https://mimicgen.github.io/docs/tutorials/getting_started.html)
- [Launching Several Data Generation Runs](https://mimicgen.github.io/docs/tutorials/launching_several.html)
- [Reproducing Published Experiments and Results](https://mimicgen.github.io/docs/tutorials/reproducing_experiments.html)
- [Data Generation for Custom Environments](https://mimicgen.github.io/docs/tutorials/datagen_custom.html)
- [Overview of MimicGen Codebase](https://mimicgen.github.io/docs/modules/overview.html)

## Troubleshooting

Please see the [troubleshooting](https://mimicgen.github.io/docs/miscellaneous/troubleshooting.html) section for common fixes, or submit an issue on our github page.

## License

The code is released under the [NVIDIA Source Code License](https://github.com/NVlabs/mimicgen/blob/main/LICENSE) and the datasets are released under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## How to add cameras
* add a camera into simulator xml
The xml files are at robosuite/models/assets/arenas/pegs_arena.xml and robosuite/models/assets/arenas/table_arena.xml. And you need to insert camera descriptions into certain lines. Here is an example where you can add a new camera "YOUR_NEW_CAM_NAME" with camera position (x,y,z) and camera rotation (w,x,y,z). This is [a useful link](https://www.andre-gaschler.com/rotationconverter/) to figure out rotations.
```
...
<!-- new camera -->
  <camera mode="fixed" name="sideview2" pos="0. -1.5 1.4879572214102434" quat="0.7933533 0.6087614 0 0" />
  <camera mode="fixed" name="backview" pos="-0.8 0.7 1.2" quat=" 0.4777144 0.1530459 -0.5213338 -0.6903455 " />
  <camera mode="fixed" name="spaceview" pos="0.85 0 1.55" quat="0.6341848 0.3127453 0.3127453 0.6341848"/>
  <camera mode="fixed" name="YOUR_NEW_CAM_NAME" pos="x y z" quat="w x y z"/>
<!-- new camera ends-->
...
```
* test it
python mimicgen/robomimic/robomimic/scripts/playback_dataset.py --dataset=YOUR_DATA_PATH/demo.hdf5 --render_image_names=NEW_CAM_NAME --video_path=SAVE_VIDEO_PATH/playback_dataset.mp4 --n=2

## How to convert a raw (state-only) dataset hdf5 to a (state-obs-action) dataset?
python mimicgen/robomimic/robomimic/scripts/dataset_states_to_obs.py --dataset=YOUR_DATA_PATH/square_d2.hdf5 --output_name=YOUR_DATA_PATH/square_d2_spaceview_rel.hdf5 --done_mode=2 --camera_height=128" --camera_width=128 --n=5 --num_workers=1 --exclude-next-obs --compress --main_camera=CAMERA_NAME --depth
## Citation

Please cite [the MimicGen paper](https://arxiv.org/abs/2310.17596) if you use this code in your work:

```bibtex
@inproceedings{mandlekar2023mimicgen,
    title={MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations},
    author={Mandlekar, Ajay and Nasiriany, Soroush and Wen, Bowen and Akinola, Iretiayo and Narang, Yashraj and Fan, Linxi and Zhu, Yuke and Fox, Dieter},
    booktitle={7th Annual Conference on Robot Learning},
    year={2023}
}
```
