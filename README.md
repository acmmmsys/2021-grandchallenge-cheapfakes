# 2021-grandchallenge-cheapfakes

Challenge homepage: https://2021.acmmmsys.org/cheapfake_challenge.php
Paper Website: https://shivangi-aneja.github.io/projects/cosmos/

## Retrieving the test dataset 

Please request access to the test dataset by filling out the form [here](https://forms.gle/kTY4cZPfFKCG35YLA). 

## Original Paper and Source Code

We refer readers to the [paper](https://arxiv.org/abs/2101.06278) and [GitHub](https://github.com/shivangi-aneja/COSMOS) for more details.


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
