# IBM Z Optimized for TensorFlow Documentation

## Table of Contents
1. [Overview](#Overview)
2. [Downloading the IBM Z Optimized for TensorFlow Container Image](#Downloading-the-IBM-Z-Optimized-for-TensorFlow-Container-Image)
3. [Model Validation](#Model-Validation)
4. [Execution on the Integrated Accelerator for AI and on CPU](#Execution-on-the-Integrated-Accelerator-for-AI-and-on-CPU)
5. [Using the Code Samples](#Using-the-Code-Samples)
6. [Logging Levels](#Logging-Levels)
7. [Removing the IBM Z Optimized for TensorFlow Container Image](#Removing-the-IBM-Z-Optimized-for-TensorFlow-Container-Image)
8. [Frequently Asked Questions](#Frequently-Asked-Questions)
9. [Working with us](#Working-with-us)
10. [Licenses](#Licenses)
11. [Disclaimer](#Disclaimer)

## Overview

Welcome to our Open-Beta program for [IBM Z Optimized for TensorFlow](https://community.ibm.com/community/user/ibmz-and-linuxone/blogs/prashantha-subbarao/2022/06/30/ibm-z-optimized-for-tensorflow). 

[TensorFlow](https://www.TensorFlow.org/) is an open source machine learning framework. It has a comprehensive set of tools that enable model development, training, and inference. It also features a rich, robust ecosystem.

On IBM z16™ hardware, TensorFlow can leverage new inference acceleration capabilities. Specifically, **TensorFlow core 2.7** is now available with support for the IBM Integrated Accelerator for AI that leverages the [IBM z Deep Neural Network Library](https://github.com/IBM/zDNN). This enablement will allow TensorFlow core 2.7 to transparently target the accelerator for a number of compute-intensive operations. The Open-Beta container image has been released through the IBM Z and LinuxONE Container Registry. Please visit the section [Downloading the IBM Z Optimized for TensorFlow Container Image](#Downloading-the-IBM-Z-Optimized-for-TensorFlow-Container-Image) to get started.

## Downloading the IBM Z Optimized for TensorFlow Container Image

Downloading the IBM Z® Optimized for TensorFlow container image requires credentials for the IBM Z and LinuxONE Container Registry, [icr.io](https://icr.io).

Documentation on obtaining credentials to `icr.io` is located [here](https://ibm.github.io/ibm-z-oss-hub/main/main.html).

Once credentials to `icr.io` are obtained and have been used to login to the registry, you may pull the IBM Z Optimized for TensorFlow container image with the following code block:

```bash
# docker or podman*
docker pull icr.io/ibmz/ibmz-optimized-for-tensorflow:1.0
```

In the `docker pull` command, the version specified above is `1.0`. This is based on the version available in the IBM Z and LinuxONE Container Registry. 

In the event you need to obtain a new version of the container image, or you want to view additional information about the container image, you may view that information [here](https://ibm.github.io/ibm-z-oss-hub/containers/ibmz-optimized-for-tensorflow.html).

**Note. This documentation will refer to image/containerization commands in terms of Docker. If you are utilizing Podman, please replace `docker` with `podman` when using our example code snippets.*

## Model Validation
The below list of models, but not limited to, trained on x86 or IBM Z, demonstrate focused optimizations that transparently target the accelerator for a number of compute-intensive operations during inferencing.

- BERT
- DenseNet121
- DenseNet169
- DenseNet201
- InceptionResNetV2
- InceptionV3
- NASNetLarge
- ResNet101
- ResNet101V2
- ResNet152
- ResNet152V2
- ResNet50
- Resnet50V2
- VGG16
- VGG19
- Xception
- YOLOv4

*Many of these models can be found [here](https://www.tensorflow.org/versions/r2.7/api_docs/python/tf/keras/applications).*

## Execution on the Integrated Accelerator for AI and on CPU

IBM Z Optimized for TensorFlow follows IBM's [train anywhere and deploy on IBM Z](https://www.ibm.com/blogs/systems/leveraging-ai-on-ibm-z-and-ibm-linuxone-for-accelerated-insights/) strategy.

### Default Execution Paths

- When using IBM Z Optimized for TensorFlow on an IBM z16™ system, TensorFlow core 2.7 graph execution will transparently target the Integrated Accelerator for AI for a number of compute-intensive operations during inferencing with no changes necessary to TensorFlow models.

- When using IBM Z Optimized for TensorFlow on an IBM z15™ system, TensorFlow core 2.7 will transparently target the CPU with no changes necessary to TensorFlow models.

### Modifying Default Execution Paths

To manually enforce which execution path should be followed, you may change the environment variable, `ZAIUDEVICES`, before execution starts. 

- To transparently target the Integrated Accelerator for AI
  - `export ZAIUDEVICES=1` or `unset ZAIUDEVICES`

- To only transparently target the CPU
  - `export ZAIUDEVICES=0`

*Note. If problems are encountered when training a model, please `export ZAIUDEVICES=0` then try training your model.*

## Using the Code Samples
- Documentation for our code samples can be found [here](samples).

## Logging Levels

To obtain logging data about inferencing workloads, please use the information below.

The following table lists different logging levels.
Each logged message has an associated logging level that categorizes the message. 

### DTLOG_LEVEL

IBM Z Optimized for TensorFlow includes `DTLOG_LEVEL` that produces logging messages regarding support for the IBM Integrated Accelerator for AI. This logging information should be used when [working with us](#Working-with-us).

| Level      | Description |
| -----------| ----------- |
| trace      | Everything that is occurring in the application       |
| debug      | Diagnostic information about the application   |
| info       | General and useful progress information about the application |
| warning    | Events that may produce potential problems in the application |
| error      | Events that cause the application to perform abnormally |
| fatal      | Severe errors that expect the application to abort |

The default `DTLOG_LEVEL` is `info`. To change the `DTLOG_LEVEL`, use the following example code snippet.

The below code snippet sets `DTLOG_LEVEL` to `trace`. To set the `DTLOG_LEVEL` to any other logging level you'd prefer, replace `trace` with the level of your choice.

```
export DTLOG_LEVEL=trace
```

*Note. This is not an all-encompassing list of logging methods with respect to TensorFlow. Please reference the [TensorFlow](https://www.TensorFlow.org/) documentation for more information about logging.*

## Removing the IBM Z Optimized for TensorFlow Container Image

In the event where you need to remove the IBM Z Optimized for TensorFlow container image, you may follow the below steps. 

1. Find the image id for the IBM Z Optimized for TensorFlow image by running `docker images`
2. Delete the IBM Z Optimized for TensorFlow image by running `docker rmi IMAGE_ID` 

If an in-use error occurs while attempting to delete the container image, use the `docker ps -a` command to show any running containers. Use the [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)  and [docker rm](https://docs.docker.com/engine/reference/commandline/rm/) commands to remove the running instances of the container. Then re-run the `docker rmi` command as illustrated above in step 2.

*Note. As a reminder, if you are Podman user, please replace `docker` with `podman` in the example code snippets provided above.*

## Frequently Asked Questions
- Q: Where can I get the IBM Z Optimized for TensorFlow container image?
  - A: Please visit this link [here](https://ibm.github.io/ibm-z-oss-hub/containers/ibmz-optimized-for-tensorflow.html).

- Q: Why are there multiple TensorFlow container images in the IBM Z and LinuxONE Container Registry?
  - A: You may have seen multiple TensorFlow container images in IBM Z and LinuxONE Container Registry, namely [ibmz/tensorflow](https://ibm.github.io/ibm-z-oss-hub/containers/tensorflow.html) and [ibmz/ibmz-optimized-for-tensorflow](https://ibm.github.io/ibm-z-oss-hub/containers/ibmz-optimized-for-tensorflow.html). 
  
    - The **"ibmz/tensorflow"** container image does not have support for the IBM Integrated Accelerator for AI. The "ibmz/tensorflow" only transparently targets the CPU. It does not have any optimizations referenced in this document. 
    
    - The **"ibmz/ibmz-optimized-for-tensorflow"** container image includes support for TensorFlow core 2.7 graph execution to transparently target the IBM Integrated Accelerator for AI. The "ibmz/ibmz-optimized-for-tensorflow" container image also allows it's users to transparently target the CPU. This container image contains the optimizations referenced in this document and has been released in the Open-Beta program for IBM Z Optimized for TensorFlow.

- Q: Where can I run the IBM Z Optimized for TensorFlow container image?
  - A: You may run the IBM Z Optimized for TensorFlow container image on IBM Linux on Z or IBM® z/OS® Container Extensions (IBM zCX).

## Working with us

Want to report a bug, request a feature, or provide us feedback? 

Contact us directly at [aionz@us.ibm.com](aionz@us.ibm.com) and become a member of the [AI on IBM Z Community](https://ibm.biz/aionibmz-community).

## Licenses

- Open-Beta (Early Release) license agreement can be found [here](https://www14.software.ibm.com/cgi-bin/weblap/lap.pl?li_formnum=L-BMYR-CEPKAE)
- The registered trademark Linux® is used pursuant to a sublicense from the Linux Foundation, the exclusive licensee of Linus Torvalds, owner of the mark on a worldwide basis.
- TensorFlow, the TensorFlow logo and any related marks are trademarks of Google Inc
- Additional license and notice files are within the `licenses-and-notices` directory of this repository. You may access the folder [here](licenses-and-notices).

## Disclaimer

IBM's statements regarding its plans, directions and intent are subject to change or withdrawal without notice at IBM's sole discretion. Information regarding potential future products is intended to outline our general product direction and it should not be relied on in making a purchasing decision. The information mentioned regarding potential future products is not a commitment, promise, or legal obligation to deliver any material, code or functionality. Information about potential future products may not be incorporated into any contract. The development, release, and timing of any future features or functionality described for our products remains at our sole discretion.
