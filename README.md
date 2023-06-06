# Stable Diffusion Version 2
![t2i](assets/stable-samples/txt2img/768/merged-0006.png)
![t2i](assets/stable-samples/txt2img/768/merged-0002.png)
![t2i](assets/stable-samples/txt2img/768/merged-0005.png)

This repository contains [Stable Diffusion](https://github.com/CompVis/stable-diffusion) models trained from scratch, compatible with the downloadable checkpoints from HuggingFace

## Requirements

You should already be carrying a relatively new version of Python3 with you. Execute the following steps to install the following virtual environment
```bash
# install virtualenv package
python -m pip install virtualenv

# create virtual environment and activate
virtualenv stable-diffusion
source stable-diffusion/bin/activate

# install requirements
python -m pip install -r requirements.txt
``` 

## Interview
You will be implementing a single step of the DDIM denoising process. Refer to [this blog post](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/#speed-up-diffusion-model-sampling) for the mathematical derivation of the proof. Specifically, you will be implementing part of the `p_sample_ddim` function inside `ldm/mdoels/diffusion/ddim.py`

### Setup
First download the checkpoint
```bash
wget https://huggingface.co/stabilityai/stable-diffusion-2-1-base/resolve/main/v2-1_512-ema-pruned.ckpt
```
> If this takes too long, then don't use the `--ckpt` flag in the command below and comment out lines 30-41 in `scripts/txt2img.py`

Run the sampling script until you hit the breakpoint, which is where you will begin your implementation. The script will download some extra models the first time you run it.
```bash
python -m scripts.txt2img \
  --prompt "a professional photograph of an astronaut riding a horse" \
  --config configs/stable-diffusion/v2-inference.yaml \
  --H 512 --W 512 --device cpu \
  --ckpt v2-1_512-ema-pruned.ckpt
```