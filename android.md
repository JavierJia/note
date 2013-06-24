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

