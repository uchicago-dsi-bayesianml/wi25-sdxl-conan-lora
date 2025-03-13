---
base_model: stabilityai/stable-diffusion-xl-base-1.0
library_name: diffusers
license: creativeml-openrail-m
inference: true
tags:
- stable-diffusion-xl
- stable-diffusion-xl-diffusers
- text-to-image
- diffusers
- diffusers-training
- lora
- stable-diffusion-xl
- stable-diffusion-xl-diffusers
- text-to-image
- diffusers
- diffusers-training
- lora
datasets:
- jugg1024/conan-gpt4-captions
language:
- en
pipeline_tag: text-to-image
---

<!-- This model card has been generated automatically according to the information the training script had access to. You
should probably proofread and complete it, then remove this comment. -->


# LoRA text2image fine-tuning - yifei28/sdxl-base-1.0-Conan-lora

These are LoRA adaption weights for stabilityai/stable-diffusion-xl-base-1.0. The weights were fine-tuned on the jugg1024/conan-gpt4-captions dataset. You can find some example images in the following. 

![Still from the Anime Character, Mark Zuckerberg](./image_0.jpg)
![Still from the Anime Character, Robert Downey Jr.](./image_1.jpg)
![Still from the Anime, Draco Malfoy](./image_2.jpg)
![Still from the Anime, Severus Snape](./image_3.jpg)


LoRA for the text encoder was enabled: True.

VAE used for training: madebyollin/sdxl-vae-fp16-fix.

#### How to use

```python
from diffusers import DiffusionPipeline

pipe = DiffusionPipeline.from_pretrained("stabilityai/stable-diffusion-xl-base-1.0")
pipe.load_lora_weights("yifei28/sdxl-base-1.0-Conan-lora")

prompt = "Still from the Anime, Elon Musk"
image = pipe(prompt).images[0]
```

#### Limitations and bias

Abnormal human features: twisted faces and low-quality body and facial features.
Only simple prompts yield better results, cannot handle long prompts. 

Note that due to the dataset we are fine-tuning on, only with some prefix, the style will transfer.
Example Prefix:
Still from the Anime, ...
Still from Anime Series, ...
Anime Series still of ...

We encourage people to try different prompts with different prefix.

## Training details

--validation_epochs=1   
--resolution=1024   
--train_text_encoder   
--train_batch_size=1   
--num_train_epochs=10   
--checkpointing_steps=1000
--gradient_accumulation_steps=8   
--learning_rate=1e-05   
--lr_warmup_steps=500   
--dataloader_num_workers=8   
--allow_tf32   
--mixed_precision="bf16"
--rank=16

### Please find the slides for presentation in this link
[Presentation](https://docs.google.com/presentation/d/1gq5uIRyTaOBXhCrzijFYoMQhtGrQAh_QZ5IXeKLyPNA/edit?usp=sharing)