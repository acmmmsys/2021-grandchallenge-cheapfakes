# 2021-grandchallenge-cheapfakes

Challenge homepage: https://2021.acmmmsys.org/cheapfake_challenge.php  


## Retrieving the public test dataset 

Please request access to the public test dataset by filling out the form [here](https://forms.gle/kTY4cZPfFKCG35YLA). 

Note that by agreeing to the terms of use, you also agree to **follow the guidelines provided in the challenge description and not to use any dataset or material other than those explicitly provided for the challenge, in building your detector**.


## Original paper and source code

We refer readers to this [paper](https://arxiv.org/abs/2101.06278) and [GitHub repository](https://github.com/shivangi-aneja/COSMOS) for background information on the COSMOS study. Please note that these are for information purposes only: you can participate in the challenge without relying on the training strategy proposed in or any artifacts from the original study.


## Building your Docker image

To build your Docker image, you can run the following bash command:
```bash
cd <submission folder>
sudo docker build -t <docker tag> .
```

## Testing your Docker image

To test your Docker image, you can run the following bash command:
```bash
cd <submission folder>
docker run -v <path to test dataset>:/mmsys21cheapfakes > <output>.txt
```

## Submitting your Docker Image

To submit your Docker image, we recommend that you export it using the following bash command:

```bash
sudo docker save <docker tag> > mmsys21cheapfakes_<lastname>.tar
```

This command will produce a tar file of your Docker image which can then be sent via e-mail to the organizers.
