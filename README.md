![Unity Audio Manager](https://github.com/MathewHDYT/Unity-Audio-Manager-UAM/blob/main/logo.png/)

[![MIT license](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://lbesson.mit-license.org/)
[![Unity](https://img.shields.io/badge/Unity-5.2%2B-green.svg?style=flat-square)](https://docs.unity3d.com/520/Documentation/Manual/index.html/)
[![GitHub release](https://img.shields.io/github/release/MathewHDYT/Unity-Audio-Manager-UAM/all.svg?style=flat-square)](https://github.com/MathewHDYT/Unity-Audio-Manager-UAM/releases/)
[![GitHub downloads](https://img.shields.io/github/downloads/MathewHDYT/Unity-Audio-Manager-UAM/all.svg?style=flat-square)](https://github.com/MathewHDYT/Unity-Audio-Manager-UAM/releases/)

# Unity Audio Manager (UAM)
Used to play/change/stop/mute/... sounds at certain circumstances or events in 2D and 3D simply via. code.

## Contents
- [Unity Audio Manager (UAM)](#unity-audio-manager-uam)
  - [Contents](#contents)
  - [Introduction](#introduction)
  - [Installation](#installation)
- [Documentation](#documentation)
  - [Reference to Audio Manager Script](#reference-to-audiomanager-script)
  - [Adding a new sound](#adding-a-new-sound)
  - [Public accesible methods](#public-accesible-methods)
    - [Play method](#play-method)
	- [Play At Time Stamp method](#play-at-time-stamp-method)
	- [Get Playback Position method](#get-playback-position-method)
	- [Play At 3D Position method](#play-at-3d-position-method)
	- [Play Attached To GameObject method](#play-attached-to-gameobject-method)
	- [Play Delayed method](#play-delayed-method)
	- [Play OneShot method](#play-oneshot-method)
	- [Play Scheduled method](#play-scheduled-method)
	- [Stop method](#stop-method)
	- [Toggle Mute method](#toggle-mute-method)
	- [Progress method](#progress-method)
	- [Get Source method](#get-source-method)
	- [Change Pitch method](#change-pitch-method)
	- [Change Volume method](#change-volume-method)

## Introduction
Nearly all games need music and soundeffects and this small and easily integrated Audio Manager can help integrate and play music in Unity for your game quick and easily.

**Unity Audio Manager implements the following methods:**
- A way to simply play a sound (see [Play method](#play-method))
- A way to play a sound at a given time in the song (see [Play At Time Stamp method](#play-at-time-stamp-method))
- A way to get the amount of time a sound has been played (see [Get Playback Position method](#get-playback-position-method))
- A way to play a sound at a 3D position (see [Play At 3D Position method](#play-at-3d-position-method))
- A way to play a sound attached to a gameobject (see [Play Attached To GameObject method](#play-attached-to-gameobject-method))
- A way to play a sound after a certain delay time (see [Play Delayed method](#play-delayed-method))
- A way to play a sound once (see [Play OneShot method](#play-oneshot-method))
- A way to play a sound at a given time in the time line (see [Play Scheduled method](#play-scheduled-method))
- A way to stop a sound (see [Stop method](#stop-method))
- A way to mute or unmute a sound (see [Toggle Mute method](#toggle-mute-method))
- A way to get the source of a sound (see [Get Source method](#get-source-method))
- A way to change the pitch of a sound (see [Change Pitch method](#change-pitch-method))
- A way to change the volume of a sound (see [Change Volume method](#change-volume-method))

For each method there is a description on how to call it and how to use it correctly for your game in the given section.

## Installation
**Required Software:**
- [Unity](https://unity3d.com/get-unity/download) Ver. 2020.3.17f1

The Audio Manager itself is version independent, as long as the AudioSource object exists. Additionally the example project can be upgraded to a newer version if needed. It is recommended to use the Version the project was originally created in, to ensure that everything works as expected.
After installing Unity you can simply download the project and open it in Unity (see [Opening a Project in Unity](https://docs.unity3d.com/2021.2/Documentation/Manual/GettingStartedOpeningProjects.html)) and start the game with the Play Button to test the Audio Managers methodality.

To simply use the Audio Manager in your own project simply get the two files in the *Example Project/Assets/Scritps* called *AudioManager* and *Sound* and use them like shown in [Adding a new sound](#adding-a-new-sound).

# Documentation
This documentation strives to explain how to start using the Audio Manager in your project and explains how to call and how to use it's publicly accesible methods correctly.

## Reference to Audio Manager Script
To use the Audio Manager to start playing audio outside of itself you need to reference it. As the Audio Manager is a [Singelton](https://stackoverflow.com/questions/2155688/what-is-a-singleton-in-c) this can be done easily when we get the instance and save it as a global private variable in the script that uses the Audio Manager.

```csharp
private AudioManager am;

void Start() {
    am = AudioManager.instance;
    // Calling method in AudioManager
    am.Play("SoundName");
}
```

Alternatively you can directly call the methods this is not advised tough, if it is executed multiple times or you're going to need the instance multiple times in the same file.

```csharp
void Start() {
    AudioManager.Play("SoundName");
}
```

## Adding a new sound
**To add a new sound you simply have to create a new element in the Sounds array with the properties:**
- Name (This is used to reference the sound in the Audio Manager so ensure it's unique)
- Clip (Simply add a sound file that is saved in your Unity Project)
- Volume (How loud the sound is)
- Pitch (Distortion of the sound effect, set it to 1 if you wan't to ensure that the soundeffect sounds like intended)
- Loop (Determines if the sound should be repeated automatically after finishing --> Usefull for a theme sound)

![Image of AudioManager Script](https://image.prntscr.com/image/hty8-QfaT9aya-SAmJ-dMA.png)

## Public accesible methods
This section exaplins all public accesible methods, especially how to call them and for what they are used. We always assume AudioManager instance has been already referenced in the script you want to use it for see [Reference to Audio Manager Script](#reference-to-audiomanager-script) if you haven't done that already.

### Play method
**What it does:**
Starts playing the choosen sound.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play.

```csharp
am.Play("SoundName");
```

**When to use it:**
Use the play method when you want to play a sound directly without changing it's initally properties. So if you enabled looping for the sound (see [Adding a new sound](#adding-a-new-sound)) then it will loop.

See [AudioSource.Play](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/AudioSource.Play.html) for more details on what play does.

### Play At Time Stamp method
**What it does:**
Start playing the choosen sound at the given timestamp.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play and startTime is the moment we want to play the sound at so instead of starting at 0 seconds we start at 10 seconds. 

```csharp
float startTime = 10f;
am.PlayAtTimeStamp("SoundName", startTime);
```

**When to use it:**
Use the play at time stamp method when you want to play a sound but skip a portion at the start. Could be used if only the second part of your sound is high intesity and normally you want to build up the intensity, but not when the game is in a special state.

### Get Playback Position method
**What it does:**
Returns the current playback position of the given sound in seconds.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to get the playback position of.

```csharp
float timeStamp = am.GetPlaybackPosition("SoundName");
Debug.Log("Current time in the song: " + timeStamp);
```

**When to use it:**
Use the get playback position to get the time the current sound has been playing.

### Play At 3D Position method
**What it does:**
Starts playing the choosen sound in a given 3D position.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play and worldPosition is the 3D position in world space is the place the sound is emitting from.
The minDistance is the distance the sound will not get louder at, the maxDistance is the distance the sound will still be hearable at, spread is the angle of the sound in degrees, spatialBlend defines how much the sound is affected by 3D (0f = 2D, 1f = 3D).
The dopplerLevel defines the doppler scale for our sound and the rolloffMode defines how the sound should decline in volume between the min and max distance.

```csharp
Vector3 worldPosition = new Vector3(10f, 10f, 0f);
float minDistance = 5f;
float maxDistance = 15f;
float spread = 0f;
float spatialBlend = 1f;
float dopplerLevel = 1f;
AudioRolloffMode rolloffMode = AudioRolloffMode.Linear;
am.PlayAt3DPosition("SoundName", worldPosition, minDistance, maxDistance, spread, spatialBlend, dopplerLevel, rolloffMode);
```

Alternatively you can call the methods with less paramters as some of them have default arguments.

```csharp
Vector3 worldPosition = new Vector3(10f, 10f, 0f);
float minDistance = 5f;
float maxDistance = 15f;
am.PlayAt3DPosition("SoundName", worldPosition, minDistance, maxDistance);
```

**When to use it:**
Use the play at 3d position method when you want to play a sound directly from a 3D position and make the volume be influenced by the distance the player has from that position.

### Play Attached To GameObject method
**What it does:**
Starts playing the choosen sound attached to a GameObject.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play and the gameObject is the object the sound is emitting from.
The minDistance is the distance the sound will not get louder at, the maxDistance is the distance the sound will still be hearable at, spread is the angle of the sound in degrees, spatialBlend defines how much the sound is affected by 3D (0f = 2D, 1f = 3D).
The dopplerLevel defines the doppler scale for our sound and the rolloffMode defines how the sound should decline in volume between the min and max distance.

```csharp
float minDistance = 5f;
float maxDistance = 15f;
float spread = 0f;
float spatialBlend = 1f;
float dopplerLevel = 1f;
AudioRolloffMode rolloffMode = AudioRolloffMode.Linear;
am.PlayAttachedToGameObject("SoundName", this.gameObject, minDistance, maxDistance, spread, spatialBlend, dopplerLevel, rolloffMode);
```

Alternatively you can call the methods with less paramters as some of them have default arguments.

```csharp
float minDistance = 5f;
float maxDistance = 15f;
am.PlayAttachedToGameObject("SoundName", this.gameObject, minDistance, maxDistance);
```

**When to use it:**
Use the play attached to gameObject method when you want to play a sound directly from a object and make the volume be influenced by the distance the player has from that object.

### Play Delayed method
**What it does:**
Starts playing the choosen sound after the given delay time.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play after the given amount of time which would be the 5 seconds we've defined.

```csharp
float delay = 5f;
am.PlayDelayed("SoundName", delay);
```

**When to use it:**
Use the play delayed method when you want to play a sound after a given delay time instead of directly when the method is called.

See [AudioSource.PlayDelayed](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/AudioSource.PlayDelayed.html) for more details on what play delayed does.

### Play OneShot method
**What it does:**
Starts playing the choosen sound once.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play once.

```csharp
am.PlayOneShot("SoundName");
```

**When to use it:**
Use the play oneshot method when you want to play a sound once.

See [AudioSource.PlayOneShot](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/AudioSource.PlayOneShot.html) for more details on what play oneshot does.

### Play Scheduled method
**What it does:**
Starts playing the sound after the given amount of time with additional buffer time to fetch the data from media.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to play after the given amount of time which would be the 10 seconds we've defined.

```csharp
double time = 10d;
am.PlayScheduled("SoundName", time);
```

**When to use it:**
Use to switch smoothly between sounds because it is independent of the frame rate and gives the audio system enough time to prepare the playback of the sound to fetch it from media where the opening and buffering takes a lot of time (streams) without causing sudden CPU spikes.

See [AudioSource.PlayScheduled](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/AudioSource.PlayScheduled.html) for more details on what Play Scheduled does.

### Stop method
**What it does:**
Stops the sound if it is currently playing.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to stop.

```csharp
am.Stop("SoundName");
```

**When to use it:**
Use to stop the given sound, if you restart it later the sound will start a new so to really stop it a workaround with the [Get Playback Position method](#get-playback-position-method) would be needed to start but at the given start time with the [Play At Time Stamp method](#play-at-time-stamp-method).

See [AudioSource.Stop](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/AudioSource.Stop.html) for more details on what stop does.

### Toggle Mute method
**What it does:**
Sets the volume of the sound to 0 and resets it to it's initally value if toggled again.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to toggle mute on / off.

```csharp
am.ToggleMute("SoundName");
```

**When to use it:**
Use to completly silence a sound and still keep it playing in the background. For example if you have a radio channel with a mute button.

### Progress method
**What it does:**
Returns the progress of the given sound, which is a float from 0 to 1.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to get the progress from.

```csharp
float progress = am.Progress("SoundName");
Debug.Log("Current progress in the song: " + progress);
```

**When to use it:**
Use to get the progress of a song for an animation or to track once it's finished to start a new song.

### Get Source method
**What it does:**
Returns the source of the given sound.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to get the source from.

```csharp
AudioSource source = am.GetSource("SoundName");
source.pitch = 0.8f;
source.volume = 0.5f;
```

**When to use it:**
Use to directly change the values of the given song yourself and affect it while it's playing.

### Change Pitch method
**What it does:**
Changes the pitch of a sound over a given amount of time.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to change the pitch from.
The endValue (0.1 - 3) is the value the pitch should have at the end.
The waitTime defines the total amount of time needed to achieve the given endValue.
The granularity is the amount of steps in which we decrease the volume to the endValue.

```csharp
float endValue = 0.8f;
float waitTime = 1f;
float granularity = 2f;
am.ChangePitch("SoundName", endValue, waitTime, granularity);
```

Alternatively you can call the methods with less paramters as some of them have default arguments.

```csharp
float endValue = 0.8f;
am.ChangePitch("SoundName", endValue);
```

**When to use it:**
Use if you want to decrease the pitch over a given amount of time.

### Change Volume method
**What it does:**
Changes the volume of a given sound over a given amount of time.

**How to call it:**
SoundName in this case is the Name we have given the sound we want to change the volume from.
The endValue (0 - 1) is the value the volume should have at the end.
The waitTime defines the total amount of time needed to achieve the given endValue.
The granularity is the amount of steps in which we decrease the volume to the endValue.

```csharp
float endValue = 0.8f;
float waitTime = 1f;
float granularity = 2f;
am.ChangeVolume("SoundName", endValue, waitTime, granularity);
```

Alternatively you can call the methods with less paramters as some of them have default arguments.

```csharp
float endValue = 0.8f;
am.ChangeVolume("SoundName", endValue);
```

**When to use it:**
Use if you want to decrease the volume over a given amount of time.
