# C++ with Meson
Install Meson and requirements
```bash
sudo apt install python3 python3-pip python3-setuptools python3-wheel ninja-build libgtk-3-dev
```
```bash
pip3 install --user meson ninja
```

Everything installed right you can configure and build the build system by running `meson build`. If the folder `build` already exists, you can run `meson --reconfigure build` to let meson run the configuration again and update the build folder.
With the build folder existing, `cd build` and run `ninja`. Ninja will gather all dependencies and build every executable for you at once. All executables are then gathered in your build folder. In short summary:
```bash
meson builddir && cd builddir
meson compile
meson test
```

## Hello World
We start with the most basic programm "Hello World". First create the C file which holds the source. 
Then create a Meson build description and write it in a file called `meson.build`. That's all we need. Build the application with the command:
```bash
meson setup builddir
cd builddir
meson compile
```
Once the executable is built it run: 
```bash
./demo
```

## Adding dependencies
More complex programms need dependencies and other files. The Meson file includes all instructions to find and use libraries, like GTK+:
```
project('tutorial', 'c')
gtkdep = dependency('gtk+-3.0')
executable('demo', 'main.c', dependencies : gtkdep)
```
To add multiple libraries, simply use seperate `dependency()` calls
```
gtkdeps = [dependency('gtk+-3.0'), dependency('gtksourceview-3.0')]
```

All infos and more about Meson on their [Homepage](https://mesonbuild.com)