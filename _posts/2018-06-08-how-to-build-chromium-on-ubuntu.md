---
title:  How to build chromium on Ubuntu
tags:
  - Linux
  - Bugs
  - C++
---

Here's how to build chromium on Ubuntu, in order to reproduce chrome's performance bug.

<!--more-->

1.Install depot_tools
Clone the depot_tools repository:
```
$ git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```
Add depot_tools to the end of your PATH (you will probably want to put this in your ~/.bashrc or ~/.zshrc). Assuming you cloned depot_tools to /path/to/depot_tools:
```
$ export PATH="$PATH:/path/to/depot_tools"
```
When cloning depot_tools to your home directory do not use ~ on PATH, otherwise gclient runhooks will fail to run. Rather, you should use either $HOME or the absolute path:
```
$ export PATH="$PATH:${HOME}/depot_tools"
```

2.Get the code
Create a chromium directory for the checkout and change to it (you can call this whatever you like and put it wherever you like, as long as the full path has no spaces):
```
$ mkdir ~/chromium && cd ~/chromium
```
Run the fetch tool from depot_tools to check out the code and its dependencies.
```
$ fetch --nohooks chromium
```
If you don't want the full repo history, you can save a lot of time by adding the --no-history flag to fetch.
Expect the command to take 30 minutes on even a fast connection, and many hours on slower ones.
If you've already installed the build dependencies on the machine (from another checkout, for example), you can omit the --nohooks flag and fetch will automatically execute gclient runhooks at the end.
When fetch completes, it will have created a hidden .gclient file and a directory called src in the working directory. The remaining instructions assume you have switched to the src directory:
```
$ cd src
```

3.Install additional build dependencies
Once you have checked out the code, and assuming you're using Ubuntu, run build/install-build-deps.sh
You may need to adjust the build dependencies for other distros. There are some notes at the end of this document, but we make no guarantees for their accuracy.

4.Run the hooks
Once you've run install-build-deps at least once, you can now run the Chromium-specific hooks, which will download additional binaries and other things you might need:
```
$ gclient runhooks
```

5.Setting up the build
Chromium uses Ninja as its main build tool along with a tool called GN to generate .ninja files. You can create any number of build directories with different configurations. To create a build directory, run:
```
$ gn gen out/Default
```

6.Build Chromium
Build Chromium (the “chrome” target) with Ninja using the command:
```
$ ninja -C out/Default chrome
```
You can get a list of all of the other build targets from GN by running gn ls out/Default from the command line. To compile one, pass the GN label to Ninja with no preceding “//” (so, for //chrome/test:unit_tests use ninja -C out/Default chrome/test:unit_tests).
 It will take several hours to build.

7.Run Chromium
Once it is built, you can simply run the browser:
```
$ ./out/Default/chrome
```
8.Running test targets
You can run the tests in the same way. You can also limit which tests are run using the --gtest_filter arg, e.g.:
```
$ out/Default/unit_tests --gtest_filter="PushClientTest.*"
```
