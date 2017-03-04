# MinGW
A binary snapshot of the MinGW development tools (currently only contains gcc/g++ related packages).

My goal here is to provide a simplified git based "install" of all the packages required to build without an actual install process. This is similar to following the manual installation process ("only attempted by more experienced users") but without the requirement of being an advanced user.

References to specific snapshots in this repository can then be used in repeatable build systems. Specifically, those which attempt to produce identical binaries by avoiding dependencies on the host system (by including the exact toolchain, SDK's, etc. used).  This repository is essentially to work-around for MinGW not being versioned as a whole but rather on a per component basis.

# Assumptions

1. Users are primarily concerned with command line tools and builds
2. Users understand how environment variables work (e.g. inheritance) and are comfortable managing them.

# Prerequisites

1. Install git: https://git-scm.com/download/ (or whatever distribution you prefer)

# Installation

1. Clone the repository using git

    ```dos
    git clone https://github.com/pmcmorris/MinGW.git
    ```
    
    Avoid locations which include spaces in the path (MinGW may not like that)
      
2. Add the binary folders to your path

    ```dos
    set MINGW_DIR=C:\users\me\where_ever_you_cloned_it
    set MSYS_DIR=%MINGW_DIR%\msys\1.0
    set PATH=%MINGW_DIR%\bin;%MSYS_DIR%\local\bin;%MSYS_DIR%\bin;%PATH%
    ```
    
    If you're doing repeatable builds, you probably don't want to update system or user environment variables and should stick to per process settings.
    
    The MinGW documentation is more cautious and suggests appending instead of prepending for compatibility. Prepending here is used to intentionally override any existing tools of the same name that may have come from other sources (e.g. Cmder, GitForWindows, etc.).

3. Update the MSYS fstab file to contain the installation folder

    Edit the install location in the %MSYS_DIR%/etc/fstab file:
    ```dos
    C:\users\me\where_ever_you_cloned_it   /mingw
    ```
    
    TODO: Write a script to make this edit and add the fstab to the local .gitignore

# Miscellaneous

Note: I've copied %MINGW_DIR%\bin\mingw32-make.exe to %MINGW_DIR%\bin\make.exe to override the default when simply 'make' is used. Otherwise, it will find the make.exe in the msys folder which uses an older version that I've encountered issues with in the past.

Last ran the MinGW package updater 2017-03-03.

# References

Discussion of manual installation process  
http://www.mingw.org/wiki/getting_started

Discussion of GCC installation process  
http://www.mingw.org/wiki/HOWTO_Install_the_MinGW_GCC_Compiler_Suite
