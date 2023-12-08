This project is used to compile opencv into a aar module that can then be directly used in projects. Steps to create a similar project:

Ref: [Android Library Doc](https://developer.android.com/studio/projects/android-library)
1. Click File > New > New Module
2. Click Android Library; enter the details and press Finish
3. Now go to Build > Build Bundle(s)/APK(s) . This will generate the AAR

(OR)

For OpenCV, since the SDK already existed,
1. Create a dummy Android project. Use Groovy builds as KTS builds do not build OpenCV properly
2. Add OpenCV by Importing the module and adding it as a dependency to the app.
3. Go to Project's `build.gradle` file and add `id 'com.android.library' version '8.1.4' apply false` since we are going to compile a library and not an application. Also add `id 'org.jetbrains.kotlin.android' version '1.9.10' apply false` since OpenCV requires this.
4. Now when we try to build, it should build `OpenCV` also. But we do not need the app part since we are just going to compile the AAR
5. In the app's build.gradle file, remove the `include (:app)` line this will ensure that the app is no longer built. You can also remove the  `id 'com.android.application' version '8.1.4' apply false` from Project's `build.gradle` as we are no longer building the app
6. Open a terminal and type the below commands:
    - `set _JAVA_OPTIONS=-Xmx512M`
    - `set JAVA_HOME=%HOME%\.jdks\corretto-17.0.9`
    - `gradlew opencv:assembleRelease`
- The above will get the aar built. It will be located in `opencv\build\outputs\aar` folder.

TODO: Ref https://medium.com/@rodrigo.vianna.oliveira/creating-an-android-library-aar-using-modularization-8607f21c589f

Warning: This is a student project and is not production ready. Use at your own risk.