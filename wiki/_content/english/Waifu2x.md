This article covers installing, using and training [waifu2x](https://github.com/nagadomi/waifu2x), image super-resolution for anime-style art using deep convolutional neural networks.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Upscaling](#Upscaling)
    *   [2.2 Noise Reduction](#Noise_Reduction)
    *   [2.3 Upscaling & Noise Reduction](#Upscaling_.26_Noise_Reduction)
*   [3 Training](#Training)
    *   [3.1 Dependencies](#Dependencies)
    *   [3.2 waifu2x source](#waifu2x_source)
    *   [3.3 Command line tools](#Command_line_tools)
        *   [3.3.1 Noise Reduction](#Noise_Reduction_2)
        *   [3.3.2 2x Upscaling](#2x_Upscaling)
        *   [3.3.3 Noise Reduction + 2x Upscaling](#Noise_Reduction_.2B_2x_Upscaling)
    *   [3.4 Train your own models](#Train_your_own_models)
        *   [3.4.1 Data Preparation](#Data_Preparation)
        *   [3.4.2 Train a Noise Reduction(level1) model](#Train_a_Noise_Reduction.28level1.29_model)
        *   [3.4.3 Train a Noise Reduction(level2) model](#Train_a_Noise_Reduction.28level2.29_model)
        *   [3.4.4 Train a 2x UpScaling model](#Train_a_2x_UpScaling_model)
        *   [3.4.5 Train a 2x and noise reduction fusion model](#Train_a_2x_and_noise_reduction_fusion_model)
*   [4 Docker](#Docker)
*   [5 See also](#See_also)

## Installation

To directly use waifu2x, install [waifu2x-git](https://aur.archlinux.org/packages/waifu2x-git/) pakage. There are other alternates for using waifu2x, just search `waifu2x` in AUR.

**Tip:** If you have an NVIDIA GPU, you can install [cuda](https://www.archlinux.org/packages/?name=cuda) to significantly speed up the conversion process.

## Usage

waifu2x is avaliable with command `waifu2x`. For detailed options, run `waifu2x --help`

### Upscaling

Use `--scale_ratio` parameter to specify scale ratio you want. And `-i` with input file name, `-o` with output file name:

```
waifu2x --scale_ratio 2 -i my_waifu.png -o 2x_my_waifu.png

```

### Noise Reduction

Use `--noise_level` parameter(`1` or `2`) to specify noise reduction level:

```
waifu2x --noise_level 1 -i my_waifu.png -o lucid_my_waifu.png

```

And you can use `--jobs` to specify number of threads launching at same time, benifit for multi-core CPU :

```
waifu2x --jobs 4 --noise_level 1 -i my_waifu.png -o lucid_my_waifu.png

```

### Upscaling & Noise Reduction

`--scale_ratio` and `--noise_level` can be combined, so you can:

```
waifu2x --scale_ratio 2 --noise_level 1 -i my_waifu.png -o 2x_lucid_my_waifu.png

```

**Tip:** If you are finding a batch operation interface, you can have a look at this [waifu2x wrapper script](https://gist.github.com/frantic1048/0970e86c4304b322270edc0ab36dd6a8)

## Training

To train custom models, **an NVIDIA graphical card is required** because waifu2x uses [CUDA](https://developer.nvidia.com/cuda-zone) for computing. Then you need to prepare below develop dependencies and waifu2x source.

### Dependencies

Install:

*   [lua51](https://www.archlinux.org/packages/?name=lua51)
*   [cuda](https://www.archlinux.org/packages/?name=cuda)
*   [snappy](https://www.archlinux.org/packages/?name=snappy)
*   [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick)
*   [torch7-git](https://aur.archlinux.org/packages/torch7-git/)
*   [torch7-trepl-git](https://aur.archlinux.org/packages/torch7-trepl-git/)
*   [torch7-sys-git](https://aur.archlinux.org/packages/torch7-sys-git/)
*   [torch7-cutorch-git](https://aur.archlinux.org/packages/torch7-cutorch-git/)
*   [torch7-nn-git](https://aur.archlinux.org/packages/torch7-nn-git/)
*   [torch7-cunn-git](https://aur.archlinux.org/packages/torch7-cunn-git/)
*   [torch7-image-git](https://aur.archlinux.org/packages/torch7-image-git/)
*   [torch7-xlua-git](https://aur.archlinux.org/packages/torch7-xlua-git/)
*   [torch7-dok-git](https://aur.archlinux.org/packages/torch7-dok-git/)
*   [torch7-optim-git](https://aur.archlinux.org/packages/torch7-optim-git/)
*   [lua51-graphicsmagick-git](https://aur.archlinux.org/packages/lua51-graphicsmagick-git/)
*   [lua51-cjson](https://aur.archlinux.org/packages/lua51-cjson/)
*   [lua51-csvigo-git](https://aur.archlinux.org/packages/lua51-csvigo-git/)
*   [lua51-snappy-git](https://aur.archlinux.org/packages/lua51-snappy-git/)

It is recommended to install below *optional* [cuDNN](https://developer.nvidia.com/cudnn) library and bindings package. With them you can enable cuDNN backend for training, which have a significant speed up.

You need to manually downlaod a cudnn binary pack from [NVIDIA cuDNN site](https://developer.nvidia.com/cudnn) during installing [cudnn](https://www.archlinux.org/packages/?name=cudnn).

*   (optional)[cudnn](https://www.archlinux.org/packages/?name=cudnn)
*   (optional)[torch7-cudnn-git](https://aur.archlinux.org/packages/torch7-cudnn-git/):

### waifu2x source

Fetch waifu2x source code from GitHub:

```
git clone --depth 1 https://github.com/nagadomi/waifu2x.git

```

Enter source directory. Now you can test waifu2x command line tool:

```
th waifu2x.lua

```

### Command line tools

**Note:** If you have installed cuDNN library, you can use cuDNN with `-force_cudnn 1` option. cuDNN is too much faster than default kernel.

#### Noise Reduction

```
th waifu2x.lua -m noise -noise_level 1 -i input_image.png -o output_image.png

```

```
th waifu2x.lua -m noise -noise_level 0 -i input_image.png -o output_image.png
th waifu2x.lua -m noise -noise_level 2 -i input_image.png -o output_image.png
th waifu2x.lua -m noise -noise_level 3 -i input_image.png -o output_image.png

```

#### 2x Upscaling

```
th waifu2x.lua -m scale -i input_image.png -o output_image.png

```

#### Noise Reduction + 2x Upscaling

```
th waifu2x.lua -m noise_scale -noise_level 1 -i input_image.png -o output_image.png

```

```
th waifu2x.lua -m noise_scale -noise_level 0 -i input_image.png -o output_image.png
th waifu2x.lua -m noise_scale -noise_level 2 -i input_image.png -o output_image.png
th waifu2x.lua -m noise_scale -noise_level 3 -i input_image.png -o output_image.png

```

For more, see [waifu2x#command-line-tools](https://github.com/nagadomi/waifu2x#command-line-tools).

### Train your own models

**Note:** If you have installed cuDNN library, you can use cuDNN kernel with `-backend cudnn` option. And, you can convert trained cudnn model to cunn model with `tools/rebuild.lua`.

**Note:** The command that was used to train for waifu2x's pretraind models is available at `appendix/train_upconv_7_art.sh`, `appendix/train_upconv_7_photo.sh`. Maybe it is helpful.

#### Data Preparation

Genrating a file list.

```
find /path/to/image/dir -name "*.png" > data/image_list.txt

```

**Note:** You should use noise free images.

Converting training data:

```
th convert_data.lua

```

#### Train a Noise Reduction(level1) model

```
mkdir models/my_model
th train.lua -model_dir models/my_model -method noise -noise_level 1 -test images/miku_noisy.png
# usage
th waifu2x.lua -model_dir models/my_model -m noise -noise_level 1 -i images/miku_noisy.png -o output.png

```

You can check the performance of model with `models/my_model/noise1_best.png`.

#### Train a Noise Reduction(level2) model

```
th train.lua -model_dir models/my_model -method noise -noise_level 2 -test images/miku_noisy.png
# usage
th waifu2x.lua -model_dir models/my_model -m noise -noise_level 2 -i images/miku_noisy.png -o output.png

```

You can check the performance of model with `models/my_model/noise2_best.png`.

#### Train a 2x UpScaling model

```
th train.lua -model upconv_7 -model_dir models/my_model -method scale -scale 2 -test images/miku_small.png
# usage
th waifu2x.lua -model_dir models/my_model -m scale -scale 2 -i images/miku_small.png -o output.png

```

You can check the performance of model with `models/my_model/scale2.0x_best.png`.

#### Train a 2x and noise reduction fusion model

```
th train.lua -model upconv_7 -model_dir models/my_model -method noise_scale -scale 2 -noise_level 1 -test images/miku_small.png
# usage
th waifu2x.lua -model_dir models/my_model -m noise_scale -scale 2 -noise_level 1 -i images/miku_small.png -o output.png

```

You can check the performance of model with `models/my_model/noise1_scale2.0x_best.png`.

For latest information, see [waifu2x#train-your-own-model](https://github.com/nagadomi/waifu2x#train-your-own-model).

## Docker

See [waifu2x#docker](https://github.com/nagadomi/waifu2x#docker).

## See also

*   [waifu2x GitHub repository](https://github.com/nagadomi/waifu2x)