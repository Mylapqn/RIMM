# RIMMR MUSIC ADDON GUIDE

This guide should teach you how you can create custom music addon for RIMM.
Guide was written on Windows 11. Therefore if you are using different OS you might need to make some adjustments according to your OS.
Also this example will only demonstrate how to make cassette player addon, but same process can be applied to every other instrument.

**Just note that it's my first time making something like this in very limited time span, so if you're having any kind of issues, please open discussion thread [here](https://steamcommunity.com/sharedfiles/filedetails/discussions/2975211620) or [here](https://steamcommunity.com/sharedfiles/filedetails/discussions/2728646394). I will try my best to help you there. Thanks**

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

### Editing config
We are working inside **Submarines-duplicate.xml**

1. (Optional) Changing name
    - Locate `name="(Cassette) Submarine"` and replace **(Cassette) Submarine** with whatever you want
        - This is how item will be named 
2. (Optional) Item description
    - Locate `description="From: The Lumineers"` and replace **From: The Lumineers** with whatever you want
        - We are using this part to give original authors credits
3. Changing identifier - THIS MUST BE UNIQUE!!
    - Locate `identifier="EXAMPLE_ADDON-RIMM-cassette-player-Submarines"` and replace `EXAMPLE_ADDON-RIMM-cassette-player-Submarines` with unique ID
        - Higly recommended to use following template `PREFIX-RIMM-INSTRUMENT-NameOfSong`
            - PREFIX - your unique ID, can be your nickname, short name of your mod, etc..
            - RIMM - Refers to RIMM Reworked.
            - INSTRUMENT - [accordion, cassette-player, chorus-book, guitar, harmonica] or any other custom made instruments
            - NameOfSong - Recommended to use same as you already filled into name
        - **identifier MUST BE UNIQUE**. If not unique you will be facing mod conflict issues.
4. (Optional) Changing tags
    - Locate `Tags="smallitem,cassette-playernotes"` and change `cassette-playernotes` [accordionnotes, cassette-playernotes, chorus-booknotes, guitarnotes, harmonicanotes]
        - You can add tag `musicnotes` if you want your item storable inside our **Sheet folders**
5. (Optional) Changing spawn probability
    - Locate `PreferredContainer`. You can edit spawn chances there. Reffer to [Barotrauma modding guide](https://regalis11.github.io/BaroModDoc/ContentTypes/Item.html) for more info.
6. (Optional) Changing prices
    - Locate `Price` and change `baseprice`. For any additional info reffer to [Barotrauma modding guide](https://regalis11.github.io/BaroModDoc/ContentTypes/Item.html)
7. (Optional) Changing Inventory Icon & Sprite
    - locate `InventoryIcon texture="%ModDir:2728646394%/graphics/CassetteAtlas.png"`
        - If you don't want to use default mod texure replace `:2728646394%/graphics/CassetteAtlas.png` with path to your icon file.
            - file should be png
            - you will need to adjust `sourcerect=` and `origin=`
        - If you did any changes to `InventoryIcon` make sure to duplicate your changes to `Sprite` right bellow as well.
8. (Optional) Changing name of "Virtual" item
    - Locate `name="Song: Surbmarine"` and change it to whatever you want
        - We use `Song` as identifier that it's virtual item, but you don't have to.
        - Players will never really interact with this item directly so it doesn't matter what it's named
9. Changing identifier of virtual item
    - locate `identifier="example_addon-rimm-cassette-player-song-submarines"` and replace `example_addon-rimm-cassette-player-song-submariness` with unique ID
        - same rules apply as before
        - Higly recommended to use following template `PREFIX-RIMM-INSTRUMENT-SONG-NameOfSong`
            - SONG - we use it for identification that this is virtual item
    - Once have your uniquie ID locate `identifiers="example_addon-rimm-cassette-player-song-submarines"` and replace `example_addon-rimm-cassette-player-song-submarines` with your that ID.
10. Change audio path
    - Locate `file="%ModDir%/audio/cassette/Submarines.ogg"` and change `audio/cassette/Submarines.ogg` to your audio file.

## Finishing & Publishing
Now that you have your config files done. All we need is to tell the game where those configs can be found and publish mod.
1. Navigate to ../RIMMR Example Addon/
2. Find **files.xml** and open it
    - (Optional) Change Name - This reflects how your mod will be presented in-game
        - You can also change altnames
    - Inside `<contentpackage></contentpackage>` Write `<Item file="%ModDir%/PATHTOYOURFILE.xml" />`
        - Example: `<Item file="%ModDir%/config/cassette/Submarines.xml" />`
    - Delete Item paths to example configs.
        - If you don't do so then there is chance someone might not do that as well and then there will mod conflicts issues.
3. Delete all provided Example files and configs
    - If you don't do so then there is chance someone might not do that as well and then there will mod conflicts issues.
4. Open your game
    - You should see your mod in MODS loader. Load it.
    - Open Submarine editor
    - Load any sub
    - Place your items inside and test them if they are working correctly
5. Publish/Update - ingame
    - MAIN MENU -> MODS -> PUBLISH
        - Select your mod
        - Fill info you need, upload picture, etc...
        - (Optional) Change visibility to Private
            - First release, just to see if everything goes okay~ You can change visibility later on mod page.
        - Hit publish

