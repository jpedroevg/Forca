# Qt and Ground Station Installation Guide

## Introduction

There are some issues related to installing Qt 5.12.12, especially when using an Ubuntu version other than 18.04. In this guide, you will learn how to install Qt 5.12.12, Qt Creator, and run the Ground Station code.

Before proceeding, make sure that you have a Qt account, as it will be required to log in to the installer.

---

# Distrobox Preparation

If you are using Ubuntu 18.04, you may skip to the next section. However, if you are using a different Ubuntu version, follow the steps below.

First, install Distrobox and a containerization engine (such as Podman):

```bash
sudo apt update
sudo apt install distrobox podman -y
```

Next, create the Ubuntu 18.04 container environment:

```bash
distrobox create --image ubuntu:18.04 --name qt18-env
```

To access the environment:

```bash
distrobox enter qt18-env
```

Once inside the container, install the required development and graphical packages:

```bash
sudo apt update
sudo apt install build-essential mesa-common-dev libglu1-mesa-dev \
libgl1-mesa-dev libx11-xcb1 libfontconfig1 libdbus-1-3 \
libxkbcommon-x11-0 libxcb-icccm4 libxcb-image0 \
libxcb-keysyms1 libxcb-randr0 libxcb-render-util0 \
libxcb-xinerama0 libxcb-xinput0 libxcb-xfixes0 -y
```

---

# Qt Installation

Inside the Ubuntu 18.04 environment, download the Qt version required to run the Ground Station source code.

After downloading, grant execution permissions to the installer:

```bash
wget https://download.qt.io/archive/qt/5.12/5.12.12/qt-opensource-linux-x64-5.12.12.run
chmod +x qt-opensource-linux-x64-5.12.12.run
```

Now, launch the installer.

> It is recommended to install all available modules to avoid missing dependency issues later.

If you are running this on a modern host system (such as Ubuntu 24.04), force the X11 backend to make the graphical installer work properly:

```bash
# Force XCB platform to launch the installer
QT_QPA_PLATFORM=xcb ./qt-opensource-linux-x64-5.12.12.run
```

After installation, export Qt Creator to your applications menu to make it easier to launch:

```bash
# Inside container qt18-env:
distrobox-export --app {Qt_path_installation}/Tools/QtCreator/bin/qtcreator
```

---

# Finalizing the Setup

At this point, Qt Creator should be available in your applications menu, probably identified as:

```text
Qt Creator (on qt18-env)
```

Clone the Ground Station repository:

```bash
git clone git@github.com:ProVANT-Project/ProVANT_GroundStation.git
```

Finally, open the project using the Qt Creator installation you just configured.

Remember to verify whether the settings in:

```text
Tools -> Options -> Kits
```

are configured correctly.

Have fun!
