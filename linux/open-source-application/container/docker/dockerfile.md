# dockerfile

Images is the basis of the container, and each time you execute docker run, you specify which image to use as the basis for the container to run. Our previous examples all used images from the docker hub. Direct use of these images can only meet certain requirements. When the image does not meet our needs, we have to customize these images.

* Image customization is to customize the configuration and files added to each layer. If you can edit, install, build, and manipulate the commands for each layer, write them to a script, and use scripts to build and customize the image. This script is the dockerfile.
* Dockerfile is a text file that contains a single instruction \(Instruction\), each instruction constructs a layer, so the content of each instruction is to describe how the layer should be constructed.





