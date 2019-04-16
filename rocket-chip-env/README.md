# rocket-chip-env

## Features
The `rocket-chip-env` docker image has `riscv-tools` and `Xilinx Vivado` installed and is ready to build a `rocket-chip` from scratch targeting either the `verilator` or an actual FPGA. This image can also compile and run `Chisel` code.

## Running for the first time
Download this docker image with:
```bash
docker pull docker.csse.rose-hulman.edu/neuroprocessor-group/deca-docker/rocket-chip-env
```
Now `cd` into the directory with the Rocket Chip project you're working on (probably `deca/`). For example, if you're using the [`deca`](https://ada.csse.rose-hulman.edu/neuroprocessor-group/deca) repository as the base for your project, `cd` into the `deca` directory. Now, to create a new docker container from this docker image, run:
```bash
docker run -it --name rcenv -v $(pwd):/project -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY docker.csse.rose-hulman.edu/neuroprocessor-group/deca-docker/rocket-chip-env
```
* `-it` - creates an interactive terminal for you to type commands into.
* `--name rcenv` - names this container `rcenv`.
* `-v $(pwd):/project` - mounts your current directory to `/project` in this container. You could alternatively replace `$(pwd)` with the absolute path on your host computer to whatever folder you want to mount at `/project` in this container.
* `-v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY` - handles connecting programs like `Vivado` running in this container to your display outside the container.

## Running subsequent times
See [`README.md`](../README.md#running-containers-subsequent-times) in this directory's parent directory.

## Building
You probably won't need to rebuild this image from scratch as you can just download a prebuilt image from this repo's docker registry. If you do rebuild this image, you'll need around 60 GB of free space on your computer.

First, you'll need to download [Vivado 2016.2](https://www.xilinx.com/member/forms/download/xef.html?filename=Xilinx_Vivado_SDK_2016.2_0605_1.tar.gz). This download requires you to create an account with Xilinx. Place the downloaded file (named `Xilinx_Vivado_SDK_2016.2_0605_1.tar.gz`) in this directory and then run the following:
```bash
# Make sure to replace <version> with your version number for the image you're building
docker build . -t docker.csse.rose-hulman.edu/neuroprocessor-group/deca-docker/rocket-chip-env:<version>
```
Note: this build will take some time and a large amount of disk space

### `install_config.txt`
`install_config.txt` is a configuration file required for installing `Vivado`. A `install_config.txt` file is already included in this directory, so you don't need to make a new one. Details of these config files and how to generate them can be found here: https://www.xilinx.com/html_docs/xilinx2018_2/sdsoc_doc/generating-configuration-file-toz1504034318049.html