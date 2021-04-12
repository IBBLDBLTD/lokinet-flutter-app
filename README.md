# Lokinet on the Go

An app to interact with Lokinet as a vpn tunnel for android

## building

build requirements:

* flutter 2.x
* lokinet android jni libs

first you need to get a build of the native libs for android lokinet

### native libs

you have 2 paths for this:

* get a ci build of the apk and extract the libs
* do it yourself (takes at least 30 minutes and a non windows build environment)

#### libs from ci

find the latest android ci build from [our ci server](https://oxen.rocks/oxen-io/loki-network/dev/?C=M&O=D)

* extract the tarball
* extract the apk
* copy libs/* to lokinet_lib/android/src/main/jniLibs/

#### DIY

get the lokinet repo source and set up your environment:

    $ git clone --recursive https://github.com/oxen-io/loki-network
    $ cd loki-network/android
    $ echo "# local.properites" > local.properties
    $ echo "sdk.dir=/path/to/android/sdk" >> local.properties
    $ echo "ndk.dir=/path/to/android/ndk" >> local.properties

build it and wait for a bit:

    $ gradle assembleDebug
    
copy the libs over:

    $ cp -av build/intermediates/cmake/debug/obj/* /path/to/lokinet-mobile/lokinet_lib/android/src/main/jniLibs/


### build with flutter

now build the project with flutter:

    $ flutter build apk --debug
    
if succesful it will produce an apk at `build/app/outputs/flutter-apk/app-debug.apk` which you can run
