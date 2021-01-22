Working with ERA5 using Dask and AWS Fargate
============================================

This example uses AWS CloudFormation to create an Amazon SageMaker Jupyter Notebook and AWS Fargate cluster for using Dask for distributed computation over large data volumes.

The Jupyter notebook shows an example of how to use Dask to load netcdf files directly from S3. The mean and standard deviation of the loaded data are then computed to demonstrate how Dask can be used to accelerate computations over large data volumes. Finally, time series are pulled from the loaded data to demonstrate how to select specific locations in a raster field.

### Getting started

[![cloudformation-launch-stack](cloudformation/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=era5&templateURL=https://s3.amazonaws.com/docs.opendata.aws/cloudformation/era5-fargate.yaml)

1. Launch the stack, by default it will be in the `us-east-1` region (since that's where the ERA5 data is) but you can change it to any region you prefer.
2. On the Parameters page, enter your `DaskWorkerGitToken` which is a GitHub OAuth Token. See below for how to get one if you don't have it. You can leave all the other parameters alone for now.
3. Hit `next` twice, agree that you know this will create IAM resources.
4. Wait for the stack to create, and then navigate to the `Outputs` tab for the link to your Jupyter Notebook.

#### Github OAuth Token

The AWS services require a GitHub OAuth token to be able to build the Docker container image for the Dask worker & scheduler nodes. To generate the token go to [https://github.com/settings/tokens](https://github.com/settings/tokens). It is enough for the token to only have `public_repo` permissions.


### Architecture

![architecture](cloudformation/architecture.png)

### Extra Packages
- intake
- intake-stac
- sat-search
- rioxarray
- geopandas

### Jupyter Lab
You can access conda environments via a terminal - trying to install geopandas and rioxarray into the conda_dask3py environment just wasn't happening.  A which -a pip gives you the environment path and you can install them in the environment directory with the local pip3 to save some time.  Installing from notebooks seemed to install to the system environment instead.
