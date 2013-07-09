# Adapter
An Adapter object acts as a bridge between an AdapterView and the underlying data for that view.The Adapter provides access to the data items. The Adapter is also responsible for making a View for each item in the data  

# Intent
An Intent is an object that provides runtime binding between separate components (such as two activities). The Intent represents an app’s "intent to do something." You can use intents for a wide variety of tasks, but most often they’re used to start another activity.

# adb cmd
## install 

    adb install /path/to/apk
    adb -s device-name install /path/to/apk

## reinstall
Reinstall the program, the original data will stay

    adb install -r /path/to/apk
    adb -s device-name install /path/to/apk

## uninstall
Uninstall everything, including data and program

    adb uninstall com.package.foo 

## push 
To copy a file from the computer to an android device connected via usb, use this:

    adb push /path/to/local/file /mnt/sdcard/path/to/file

## run an application

    adb shell am start -n com.package.name/com.package.name.ActivityName

# creat a sdcard on emulator
The easiest one is using eclipse to edit the adt, it will be found at /mnt/sdcard on device

The other way is to using adt tools, the details is found here :
http://androidblogger.blogspot.com/2009/02/tutorial-how-to-emulate-sd-card-with.html

## adb devices 
When it showed that 

    adb devices:
    ????  no permissions

fix it using root:

    sudo /path/to/adb kill-server
    sudo /path/to/adb start-server
    sudo /path/to/adb devices

# using ant to build the package
Reference is on http://www.androidengineer.com/2010/06/using-ant-to-automate-building-android.html

Build from exist eclipse-adt project

    android update project -p . -n my-project
    Options:
      -l --library    : Directory of an Android library to add, relative to this
                        project's directory.
      -p --path       : The project's directory. [required]
      -n --name       : Project name.
      -t --target     : Target ID to set for the project.
      -s --subprojects: Also updates any projects in sub-folders, such as test
                        projects.

# Add third part META-INF/services into apk
Followed the reference : http://stackoverflow.com/questions/16898409/keep-meta-inf-services-files-in-apk/17066147#17066147

I created a custom_rules.xml with the followin targets to copy files in META-INF/services into the unaligned and unsigned apk.

    <project name="add-services">
    <target name="-post-package" depends="-custom-copy" />
    <target name="-copy-custom">
        <zip destfile="${out.packaged.file}"
             update="true"
             basedir="${source.absolute.dir}"
             includes="${custom.copy}" />
    </target>
    </project>

And in ant.properties I added the line

    custom.copy=META-INF/services/**

Now I just have to copy relevant files from libraries to the META-INF/services-folder of my own project to include them in the apk. This gives me full control over which classes to be loaded by ServiceLoader.

# command line create/start emulator

    android list avd
    emulator -avd "name" or emulator @"name"

# command line store logcat
    
    adb logcat > logcat.log

# command line translate ndk memory dump
 
    ndk-stack -sym libs/armeabi-v7a/ -dump logcat.log | more


