# RIMMR MUSIC ADDON GUIDE

This guide should teach you how you can create custom music addon for RIMM.
Guide was written on Windows 11. Therefore if you are using different OS you might need to make some adjustments according to your OS.
Also this example will only demonstrate how to make cassette player addon, but same process can be applied to every other instrument.

## Preparations:
Here is list of things you should do before you start working:
* Install [Barotrauma](https://store.steampowered.com/app/602960/Barotrauma/)
* Subscribe to [RIMM Reworked on steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2728646394)
* Download [ffmpeg](https://ffmpeg.org/)
* Have your audio files ready (Needs to be **.ogg**).
    - If your audio file isn't **.ogg** follow [(Optional) Conversion/Compressing audio files](https://github.com/Mylapqn/RIMM/tree/main/RIMMR%20Example%20Addon#cloning-repository) which can also convert to .ogg

Optional:
* Install [notepad++](https://notepad-plus-plus.org/) or something similar (VisualStudio Code, Atom, etc..)

## Cloning Repository
1. Head to [RIMM GITHUB](https://github.com/Mylapqn/RIMM/tree/main)
2. Click green **\<Code\>** and click **Download ZIP**
3. Navigate to home directory of Barotrauma. Default: _C:\Program Files (x86)\Steam\steamapps\common\Barotrauma_
4. Extract downloaded .zip file into **LocalMods**
    - Now you should have 2 new folders in folder **LocalMods**
        * RIMM Reworked
        * RIMMR Example Addon
5. Delete **RIMM Reworked** folder
6. (Optional) Rename **RIMMR Example Addon** to whatever you like. Just note that I will still be reffering to that folder as it is now.

## (Optional) Conversion/Compressing audio files.
Barotrauma doesn't like "big" audio files. Especially if you're playing in multiplayer. Using big audio files can cause lags, and players loosing connection. That's why we decided to use compression to make files smaller and keep the audio levels acceptable.
1. Locate to folder where **ffmpeg.exe** is located
2. (Optional) Put the audio files in the same folder as **ffmpeg.exe** is
3. Right click inside folder and select **Open Terminal**
4. Windows PowerSheel should open
5. Write `./ffmpeg.exe -y -i input.ogg -af "pan=stereo|c0<c0+c1|c1<c0+c1" -c:a libvorbis -ab 32k -ar 22050 out.ogg`
    - replace **input.ogg** with name of your audio file
        - if your audio is for example **.mp3** this command will convert your audio to .ogg along with compresion
            - if you want only to convert to .ogg write `./ffmpeg.exe -i input.mp3 out.ogg`
                - Replace **input.mp3** with your file name.
6. Inside folder you should now have new file **out.ogg**
7. (Optional) For cassette player music run another command
    - `./ffmpeg.exe -y -i out.ogg -c:a libvorbis -ab 32k -ar 11025 radio-out.ogg`
        - It will generate new **radio-out.ogg**, use that instead of **out.ogg**

## Making mod
1. Place your audio files into **RIMMR Example Addon**. It's highly recommended to use our current mod structure as it should be quite easy to navigate.
    - Example: I have audio file for cassette player **Submarines.ogg**. So I place it inside of `../LocalMods/RIMMR Example Addon/audio/cassette/`
2. Navigate to `../RIMMR Example Addon/config/cassette/`
3. Duplicate **Submarines.xml** file
4. Rename duplicate to whatever you want (I will be reffering to this file as **Submarines-duplicate.xml**). It's recommended to use same name as you use on your audio file.
    - After renaming it still **NEEDS TO BE .xml** file
5. Open **Submarines-duplicate.xml** in your preffered text editor
