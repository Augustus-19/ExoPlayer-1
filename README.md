# Playing HLS Mosaic Video with 1 Video and 4 Audio channels #

Below link have video with 1 Video and 4 Audio channels
http://livelike-vod.s3.amazonaws.com/playlists/fifa-mosaic.m3u8

Single video channel will provide all 4 view for 4 different audio in same frame.

Next button will change the view and also changes the corresponding audio.

# How its done:
1. Use TextureView to scale and translate the video frame.
2. MediaCodecVideoRenderer has API to send video format change to playerView, just trigger this api and provide corresponding quadrant index
   in the video frame
   0:top-left 1:top-right 2:bottom-left 3:bottom-right
   Same index used to change the audio tracks too.
3. Changing audio track is done using TrackSelectionHelper


# Files changed:
1.  demos/main/src/main/AndroidManifest.xml
2.  demos/main/src/main/assets/media.exolist.json
3.  demos/main/src/main/java/com/google/android/exoplayer2/demo/PlayerActivity.java
4.  demos/main/src/main/java/com/google/android/exoplayer2/demo/TrackSelectionHelper.java
5.  demos/main/src/main/res/layout/player_activity.xml
6.  demos/main/src/main/res/values/strings.xml
7.  library/core/src/main/java/com/google/android/exoplayer2/C.java
8.  library/core/src/main/java/com/google/android/exoplayer2/SimpleExoPlayer.java
9.  library/core/src/main/java/com/google/android/exoplayer2/video/MediaCodecVideoRenderer.java
10. library/ui/src/main/java/com/google/android/exoplayer2/ui/PlayerView.java


# How to test:

Check video in below link to check how to test the application
[![IMAGE ALT TEXT HERE](https://github.com/Kirancd/ExoPlayer-1/blob/release-v2/youtubeVideo.png)](https://www.youtube.com/watch?v=0cpXvyRxskM&feature=youtu.be)

https://www.youtube.com/watch?v=0cpXvyRxskM&feature=youtu.be

# ExoPlayer #

ExoPlayer is an application level media player for Android. It provides an
alternative to Android’s MediaPlayer API for playing audio and video both
locally and over the Internet. ExoPlayer supports features not currently
supported by Android’s MediaPlayer API, including DASH and SmoothStreaming
adaptive playbacks. Unlike the MediaPlayer API, ExoPlayer is easy to customize
and extend, and can be updated through Play Store application updates.

## Documentation ##

* The [developer guide][] provides a wealth of information.
* The [class reference][] documents ExoPlayer classes.
* The [release notes][] document the major changes in each release.
* Follow our [developer blog][] to keep up to date with the latest ExoPlayer
  developments!

[developer guide]: https://google.github.io/ExoPlayer/guide.html
[class reference]: https://google.github.io/ExoPlayer/doc/reference
[release notes]: https://github.com/google/ExoPlayer/blob/release-v2/RELEASENOTES.md
[developer blog]: https://medium.com/google-exoplayer

## Using ExoPlayer ##

ExoPlayer modules can be obtained from JCenter. It's also possible to clone the
repository and depend on the modules locally.

### From JCenter ###

The easiest way to get started using ExoPlayer is to add it as a gradle
dependency. You need to make sure you have the JCenter and Google repositories
included in the `build.gradle` file in the root of your project:

```gradle
repositories {
    jcenter()
    google()
}
```

Next add a gradle compile dependency to the `build.gradle` file of your app
module. The following will add a dependency to the full library:

```gradle
implementation 'com.google.android.exoplayer:exoplayer:2.X.X'
```

where `2.X.X` is your preferred version. Alternatively, you can depend on only
the library modules that you actually need. For example the following will add
dependencies on the Core, DASH and UI library modules, as might be required for
an app that plays DASH content:

```gradle
implementation 'com.google.android.exoplayer:exoplayer-core:2.X.X'
implementation 'com.google.android.exoplayer:exoplayer-dash:2.X.X'
implementation 'com.google.android.exoplayer:exoplayer-ui:2.X.X'
```

The available library modules are listed below. Adding a dependency to the full
library is equivalent to adding dependencies on all of the library modules
individually.

* `exoplayer-core`: Core functionality (required).
* `exoplayer-dash`: Support for DASH content.
* `exoplayer-hls`: Support for HLS content.
* `exoplayer-smoothstreaming`: Support for SmoothStreaming content.
* `exoplayer-ui`: UI components and resources for use with ExoPlayer.

In addition to library modules, ExoPlayer has multiple extension modules that
depend on external libraries to provide additional functionality. Some
extensions are available from JCenter, whereas others must be built manually.
Browse the [extensions directory][] and their individual READMEs for details.

More information on the library and extension modules that are available from
JCenter can be found on [Bintray][].

[extensions directory]: https://github.com/google/ExoPlayer/tree/release-v2/extensions/
[Bintray]: https://bintray.com/google/exoplayer

### Locally ###

Cloning the repository and depending on the modules locally is required when
using some ExoPlayer extension modules. It's also a suitable approach if you
want to make local changes to ExoPlayer, or if you want to use a development
branch.

First, clone the repository into a local directory and checkout the desired
branch:

```sh
git clone https://github.com/google/ExoPlayer.git
git checkout release-v2
```

Next, add the following to your project's `settings.gradle` file, replacing
`path/to/exoplayer` with the path to your local copy:

```gradle
gradle.ext.exoplayerRoot = 'path/to/exoplayer'
gradle.ext.exoplayerModulePrefix = 'exoplayer-'
apply from: new File(gradle.ext.exoplayerRoot, 'core_settings.gradle')
```

You should now see the ExoPlayer modules appear as part of your project. You can
depend on them as you would on any other local module, for example:

```gradle
implementation project(':exoplayer-library-core')
implementation project(':exoplayer-library-dash')
implementation project(':exoplayer-library-ui')
```

## Developing ExoPlayer ##

#### Project branches ####

* Development work happens on the `dev-v2` branch. Pull requests should
  normally be made to this branch.
* The `release-v2` branch holds the most recent release.

#### Using Android Studio ####

To develop ExoPlayer using Android Studio, simply open the ExoPlayer project in
the root directory of the repository.
