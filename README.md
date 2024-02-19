# Containerized Builds and Proces

## Purpose

The purpose of this repository is to have automated processes and builds of tools to facilitate development and avoid dependency mayhem.

## Structure

Every container is provided in any of 3 flavours: executable (like a Docker command), interactive (like a Docker entrypoint to BASH), or a special version (for archival). Specific instructions for running and building can be found under the specific container in the below List of Containers. The interactive flavour allows for keeping the state through multiple runs of an executable.

## Tools

_BASH_ for interactive sessions inside the containers.
_Docker_ for containerization.

## List of Containers

### GIMP DEV using Flatpak
A container of the Flatpak packaged latest development version of the GNU Image Manipulation Program (GIMP).
### Prerquisites
1. For Linux, use the command _xhost +_ . This allows running an X application on the host machine through Docker.
1. Build the Docker image using the command _docker build -t mm1ib/gimpdev-flatpak:interactive -f Dockerfile-GIMP-Flatpak-Interactive ._ .
### Executable Flavour
1. On the host machine, use the command _docker run --rm -it --privileged -v /run/dbus/system_bus_socket:/var/run/dbus/system_bus_socket -e DISPLAY=${DISPLAY} -v /tmp/.X11-unix:/tmp/.X11-unix --network host  --user root:root --mount type=bind,source=$HOME,target=$HOME mm1ib/gimpdev-flatpak:interactive_ . Both volumes are necessary for the X application to wwor, while the DISPLAY environemtn variable binds it to the host's display. The mount option is optional and should point to the directory where the images to be manipulated inside GIMP are.
1. Inside the container's BASH, use the command _flatpak run org.gimp.GIMP_ .
### Know Issues
The first run takes long time to get GIMP working, probably because of an issue between Flatpak and Docker. Further runs in the interactive session open seamlessly.
