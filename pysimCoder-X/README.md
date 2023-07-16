# pysimCoder, SHV and NuttX containerised development environment
 
Launch the docker image using
```
$ docker run --rm --env="DISPLAY" --net=host -v $XAUTHORITY:/tmp/.Xauthority -e XAUTHORITY=/tmp/.Xauthority --privileged hchaal/rcp-dev
```
Add the argument
```
--device=/dev/ttyACM0
```
to the command above to be able to connect the container to your host machine USB port. 
You may need to check your specific port first. To do this plug in your board, for example: nucleo-f446re, to your host machine USB port then run:
```
dmesg | tail -20
```

To launch pysimCoder in the container run:
```
psc
```

This version include the Silicon-Heaven application (SVH) which enable modifying parameters of the RT task and plotting signals on-the-fly. To launch SVH run:
```
shv
```

NuttX files are included in: /NUTTX/nuttx and /NUTTX/apps.

Additional tools included in this version are:

- thunar: file manager (GUI).
- gedit: simple text editor (GUI).
- nano: text editor (on terminal).
- minicom: serial communication.





