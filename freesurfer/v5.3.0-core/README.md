## vistalab/freesurfer-core

This dockerfile will create a docker image with a functioning (headless) version of Freesurfer (v5.3.0) without the ```subjects```, ```trctrain```, and ```average``` data. 

* You MUST read and agree to the license agreement and [register with MGH before you use the software](https://surfer.nmr.mgh.harvard.edu/registration.html). 
* Once you get your license please edit the license file to reflect your license. 
* You can also change ```build.sh``` to edit the tag for the image (default=vistalab/freesurfer-core).
* The resulting image is ~2.9GB
* This image WILL NOT WORK with commands that depend on data within ```subjects```, ```trctrain```, or ```averages``` directories.

### Build the Image
To build the image, either download the files from this repo or clone the repo:
```
git clone https://github.com/vistalab/docker
cd docker/freesurfer/v5.3.0-core/
./build.sh
```

### Example Usage ###
To run a Freesurfer command (e.g., ```mri-convert```) from this image you can do the following:
```
docker run --rm -ti \
  -v </path/to/input/data>:/input \
  -v </path/for/output/data>:/opt/freesurfer/subjects \
  vistalab/freesurfer-core \
  mri_convert [options] <in volume> <out volume>
```
* Note that you are mounting the directory (```-v``` flag) which contains your data in the container at ```/input``` and mounting the directory where you want your output data within the container at ```/opt/freesurfer/subjects``` - which is Freesurfer's default subjects directory. 

* The name of the freesurfer executable and the args (relative to the contianer) should be provided at the end of the ```docker run``` command. Remember that if those inputs are files or other resources, they must also be mounted in the container and the full path to them (again, relative to the container) must be provided. 



