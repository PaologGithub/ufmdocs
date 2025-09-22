# Python dependencies
First, make sure you have [CPython 3.13](https://www.python.org/downloads/release/python-313/) installed on your computer. You **cannot** use other version of python, only 3.13 is supported for now. 
Make sure too that you use python 3.13 while building, and not any other installed version. To be sure which version you use, use `python3.13` and not `python3` in the commands.

## Protobuf installation
Then, install [protobuf](https://pypi.org/project/protobuf/). I don't remember why we need version `3.20.0`, but as I remember, that's the latest supported version. To install protobuf, use this command:
```bash
python3.13 -m pip install protobuf===3.20.0
```

## Panda3D installation
To build Ursina For Mobile binaries, you need to build Panda3D on Android. **WARNING:** TO BUILD PANDA3D FOR ANDROID, YOU **CANNOT**, ON YOUR PC, USE A STABLE WHEEL OF PANDA3D.
So, it's required to use a beta wheel.


There are multiple wheel for multiple os, here are some:
- Windows (64 bit):
    ```bash
    python3.13 -m pip install https://buildbot.panda3d.org/downloads/b32d5c672441c280f7e799483d223e252cf9f797/panda3d-1.11.0.dev3788-cp313-cp313-win_amd64.whl
    ```
- Linux (64 bit):
    ```bash
    python3.13 -m pip install https://buildbot.panda3d.org/downloads/b32d5c672441c280f7e799483d223e252cf9f797/panda3d-1.11.0.dev3788-cp313-cp313-manylinux2014_x86_64.whl
    ```
- MacOS (Universal (Intel and Apple Silicon)(Not recommended)):
    ```bash
    python3.13 -m pip install https://buildbot.panda3d.org/downloads/b32d5c672441c280f7e799483d223e252cf9f797/panda3d-1.11.0.dev3788-cp313-cp313-macosx_11_0_universal2.whl
    ```
- MacOS (Intel - 64 bit):
    ```bash
    python3.13 -m pip install https://buildbot.panda3d.org/downloads/b32d5c672441c280f7e799483d223e252cf9f797/panda3d-1.11.0.dev3788-cp313-cp313-macosx_10_13_x86_64.whl
    ```
You can grab other wheel from the [buildbot](https://buildbot.panda3d.org/downloads/?C=M;O=A). Make sure you use wheels that have:
- `panda3d-1.11.0.devXXXX` version in the wheel
- `cp313` python version of the wheel