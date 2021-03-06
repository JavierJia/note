# Android codename || version || API level
http://source.android.com/source/build-numbers.html

# Good Tutorials
http://www.androidhive.info/

# Adapter
An Adapter object acts as a bridge between an AdapterView and the underlying data for that view.The Adapter provides access to the data items. The Adapter is also responsible for making a View for each item in the data  

# Intent
An Intent is an object that provides runtime binding between separate components (such as two activities). The Intent represents an app’s "intent to do something." You can use intents for a wide variety of tasks, but most often they’re used to start another activity.

# Install ia32-libs for adb
Only works for 12.10 Ubuntu
```
sudo dpkg --add-architecture i386
sudo apt-get update 
sudo apt-get install ia32-libs
```

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

# write/read permission to sd card:

    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /

# ndk-stack
http://mogoweb.net/archives/133

# Test devices version:
```Java
if (Build.VERSION.SDK_INT >= 11) {
    queryTask.executeOnExecutor(AsyncQueryTask.SERIAL_EXECUTOR,
    s.toString());
} else {
    queryTask.execute(s.toString());
}
```
# Power monitor
http://powertutor.org/

# About the guesture
http://stackoverflow.com/questions/937313/android-basic-gesture-detection

# Start Activity Transition
if we want to change the animation of transition between different activities we need to define the xml file for it.
http://stackoverflow.com/questions/5151591/android-left-to-right-slide-animation

# Service
## OnBind
onBind only works once while the first client bind. The rest directly use it

# Read the contact 
The best example: http://www.coderzheaven.com/2011/06/13/get-all-details-from-contacts-in-android/

The answers from stackoverflow are also good:
http://stackoverflow.com/questions/1721279/how-to-read-contacts-on-android-2-0

```java
public void readContacts(){
ContentResolver cr = getContentResolver();
Cursor cur = cr.query(ContactsContract.Contacts.CONTENT_URI,
null, null, null, null);

if (cur.getCount() > 0) {
while (cur.moveToNext()) {
String id = cur.getString(cur.getColumnIndex(ContactsContract.Contacts._ID));
String name = cur.getString(cur.getColumnIndex(ContactsContract.Contacts.DISPLAY_NAME));
if (Integer.parseInt(cur.getString(cur.getColumnIndex(ContactsContract.Contacts.HAS_PHONE_NUMBER))) > 0) {
System.out.println("name : " + name + ", ID : " + id);

// get <span id="IL_AD7" class="IL_AD">the phone</span> number
Cursor pCur = cr.query(ContactsContract.CommonDataKinds.<span id="IL_AD8" class="IL_AD">Phone</span>.CONTENT_URI,null,
ContactsContract.CommonDataKinds.Phone.CONTACT_ID +" = ?",
new String[]{id}, null);
while (pCur.moveToNext()) {
String phone = pCur.getString(
pCur.getColumnIndex(ContactsContract.CommonDataKinds.Phone.NUMBER));
System.out.println("phone" + phone);
}
pCur.close();


// get email and type


Cursor emailCur = cr.query(
        ContactsContract.CommonDataKinds.Email.CONTENT_URI,
        null,
        ContactsContract.CommonDataKinds.Email.CONTACT_ID + " = ?",
        new String[]{id}, null);
while (emailCur.moveToNext()) {
    // This would allow you get several <span id="IL_AD6" class="IL_AD">email addresses</span>
    // if the email addresses were stored in an array
    String email = emailCur.getString(
            emailCur.getColumnIndex(ContactsContract.CommonDataKinds.Email.DATA));
    String emailType = emailCur.getString(
            emailCur.getColumnIndex(ContactsContract.CommonDataKinds.Email.TYPE));

    System.out.println("Email " + email + " Email Type : " + emailType);
}
emailCur.close();

// Get note.......
String noteWhere = ContactsContract.Data.CONTACT_ID + " = ? AND " + ContactsContract.Data.MIMETYPE + " = ?";
String[] noteWhereParams = new String[]{id,
    ContactsContract.CommonDataKinds.Note.CONTENT_ITEM_TYPE};
Cursor noteCur = cr.query(ContactsContract.Data.CONTENT_URI, null, noteWhere, noteWhereParams, null);
if (noteCur.moveToFirst()) {
    String note = noteCur.getString(noteCur.getColumnIndex(ContactsContract.CommonDataKinds.Note.NOTE));
    System.out.println("Note " + note);
}
noteCur.close();

//Get Postal Address....

String addrWhere = ContactsContract.Data.CONTACT_ID + " = ? AND " + ContactsContract.Data.MIMETYPE + " = ?";
String[] addrWhereParams = new String[]{id,
    ContactsContract.CommonDataKinds.StructuredPostal.CONTENT_ITEM_TYPE};
Cursor addrCur = cr.query(ContactsContract.Data.CONTENT_URI,
        null, null, null, null);
while(addrCur.moveToNext()) {
    String poBox = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.POBOX));
    String street = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.STREET));
    String city = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.CITY));
    String state = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.REGION));
    String postalCode = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.POSTCODE));
    String country = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.COUNTRY));
    String type = addrCur.getString(
            addrCur.getColumnIndex(ContactsContract.CommonDataKinds.StructuredPostal.TYPE));

    // Do something with these....

}
addrCur.close();

// Get Instant Messenger.........
String imWhere = ContactsContract.Data.CONTACT_ID + " = ? AND " + ContactsContract.Data.MIMETYPE + " = ?";
String[] imWhereParams = new String[]{id,
    ContactsContract.CommonDataKinds.Im.CONTENT_ITEM_TYPE};
Cursor imCur = cr.query(ContactsContract.Data.CONTENT_URI,
        null, imWhere, imWhereParams, null);
if (imCur.moveToFirst()) {
    String imName = imCur.getString(
            imCur.getColumnIndex(ContactsContract.CommonDataKinds.Im.DATA));
    String imType;
    imType = imCur.getString(
            imCur.getColumnIndex(ContactsContract.CommonDataKinds.Im.TYPE));
}
imCur.close();

// Get Organizations.........

String orgWhere = ContactsContract.Data.CONTACT_ID + " = ? AND " + ContactsContract.Data.MIMETYPE + " = ?";
String[] orgWhereParams = new String[]{id,
    ContactsContract.CommonDataKinds.Organization.CONTENT_ITEM_TYPE};
Cursor orgCur = cr.query(ContactsContract.Data.CONTENT_URI,
        null, orgWhere, orgWhereParams, null);
if (orgCur.moveToFirst()) {
    String orgName = orgCur.getString(orgCur.getColumnIndex(ContactsContract.CommonDataKinds.Organization.DATA));
    String title = orgCur.getString(orgCur.getColumnIndex(ContactsContract.CommonDataKinds.Organization.TITLE));
}
orgCur.close();
}
```

# Redirect the printf() code inside App
```
adb shell stop
adb shell setprop log.redirect-stdio true
adb shell start
```
Then you can view the output of your "printf()" statements by looking at the "LogCat" window of Eclipse Debugger, or by typing this on a command line:
```
adb logcat
```

# Android nkd-build for all chip set:
Inside Application.mk file declare this
```
APP_ABI := all
```

# Build openssl
Android has a openssl lib, so we don't need to build a static library. 
This is a good resource:
https://github.com/guardianproject/openssl-android
```
OPENSSL_HOME="$HOME/software/openssl-android"
if [ ! -d $OPENSSL_HOME ];then
git clone https://github.com/guardianproject/openssl-android.git $OPENSSL_HOME
cd $OPENSSL_HOME
# Change the version of 4.* into the exist one by checking 
# $ANDROID_NDK_HOME/toolchain/*-androideabi-4.*
$ANDROID_NDK_HOME/ndk-build NDK_TOOLCHAIN_VERSION=4.6
cp -r libs/armeabi/*.so $ANDROID_STANDALONE_TOOLCHAIN/user/lib/
cp -r include/openssl   $ANDROID_STANDALONE_TOOLCHAIN/user/include/
fi              
```

# Some system intent:
http://beta.appinventor.mit.edu/learn/reference/other/activitystarter.html
## Call 
```
Intent intent = new Intent(Intent.ACTION_CALL);
intent.setData(Uri.parse("tel:" + "133999"));
startActivity(intent);
```
## SMS
```
Intent smsIntent = new Intent(Intent.ACTION_VIEW);
smsIntent.setType("vnd.android-dir/mms-sms");
smsIntent.putExtra("address", "949xxx");
smsIntent.putExtra("sms_body", "msg");
```
## To certain contact:
```
ContentResolver resolver = getContentResolver();
Cursor cursor = resolver.query(
    ContactsContract.Contacts.CONTENT_URI, null,
    ContactsContract.Contacts.DISPLAY_NAME + "= ?",
    new String [] {"Contact name"}, null);
    if (cursor.getCount() > 0) {
        cursor.moveToFirst();
        String xid = cursor.getString(cursor
            .getColumnIndex(ContactsContract.Contacts._ID));
        intent = new Intent(Intent.ACTION_VIEW, Uri
            .withAppendedPath(
                ContactsContract.Contacts.CONTENT_URI, xid));
        startActivity(intent);
    }
```

# Sign the release apk:
http://developer.android.com/tools/publishing/app-signing.html

# ICON
http://android-ui-utils.googlecode.com/hg/asset-studio/dist/icons-launcher.html#foreground.type=clipart&foreground.space.trim=1&foreground.space.pad=0.05&foreground.clipart=res%2Fclipart%2Ficons%2Fnavigation_cancel.svg&foreColor=33b5e5%2C0&crop=0&backgroundShape=bevel&backColor=ffffff%2C100

# Listen to the contacts changes:
http://saigeethamn.blogspot.in/2011/05/contacts-api-20-and-above-android.html

# Emulater send message

*open a console
*connect via telnet to the running emulator: telnet localhost 5554 (you can find the portnumber in the title of the emulator)
*type this: sms send senderPhoneNumber textmessage

# Android clear application data
```
adb -s emulator-5554 shell pm clear com.android.demo
```

# Android format string to URI
```
String queryUri = String.format(
                "http://www.google.com/complete/search?output=toolbar&q=%s",
                                Uri.encode(queryString));
```

# Custom title bar
http://www.edumobile.org/android/android-programming-tutorials/creating-a-custom-title-bar/

