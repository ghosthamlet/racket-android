racket-android - deploying Racket on Android

This project was funded by Black Swan Learning LLC.

# DEPENDENCIES

- OS X development machine (This is not an intrinsic requirement, but
  a happenstance of how we made it.)

- A Java JRE/JDK of the 1.8.0-era. (We test with 1.8.0_92.)

- Android SDK 23 with 23.0.2 build tools installed in
  `~/Library/Android/sdk` (the default location that Android Studio
  puts it in.)
  
- Android NDK for version 23, compiler version 4.9 installed in
  `~/Library/Android/sdk/ndk-bundle` (default location) (Perhaps we
  can generalize the build process to use a different one, but it is
  tested with this one)
  
- An Android device that supports version 23, uses armeabi, and
  support OpenGL ES 3. We test with the Google Pixel C.
  
- A Racket version that supports `--enable-ffipoll` (6.6 and later)

- The Racket packages, `lux`, `opengl`, and `mode-lambda`.

# USAGE

Put the program that you want to run in `rkt/app.rkt`. It will use
`rkt/app-csd.rkt` for the compiled sprite database.

Run `make build_all` in the main directory. This will download the
current Racket master repository and build a cross-compiled version of
it for use on Android. It is essential that this version and the
version that `racket` runs are the same version, because they will
share compiled bytecode, so you may want to build this version as
second time and put it in your `$PATH` when working with
`racket-android`.

It will place the appropriate C code into the `project` directory for
use by the Android app. If you run `make app`, then it will build the
Android app and install it to the attached device.

The Android app can be customized in the usual ways by, for instance,
modifying `project/app/src/main/AndroidManifest.xml` (for name and
permissions) or `project/app/src/main/res` (for icons.)

# EXAMPLES

Look at `rkt/basic.rkt` for an example application.

The simulator provides an interface compatible with the tablet and can
be run locally directly from DrRacket/etc. This requires a OpenGL
driver that supports most of the features of OpenGL ES 3. When you use
the simulator, you will have to manually recompile `rkt/app-csd.rkt`
to update the sprite database. (The tablet `Makefile` takes care of
this automatically.)

# TODO
- Make 'raco ctool' use gzip for the bytecode to decrease app size.
- Implement some sort of tree-shaking of bytecode to decrease app size.
