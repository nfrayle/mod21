# 1.12 Minecraft Modding in IntelliJ

Video: [Forge MDK Setup in IntelliJ 2017](https://www.youtube.com/watch?v=G2aPT36kf60)git

## One Time Setup

### Copy MDK from minecraftforge

The MDK serves as the starting point for a new mod.

* copy base files from http://files.minecraftforge.0net/
  * download MDK to serve as starting point files
  * download Recommended instead of Latest
  * for easy access, stored in ~/Documents/__DEVELOPMENT__/1.12-DO_NOT_TOUCH-MineCraft_1.12_Base_for_Mods/forge-1.12.2-14.23.4.2705-mdk

## For every new mod

### Copy MDK as the starting point of the mod

NOTE: Everywhere you see modname, change to the actual name of the new mod (e.g. mod21)

#### copy forge-1.12.2-14.23.4.2705-mdk

* FROM: ~/Documents/__DEVELOPMENT__/1.12-DO_NOT_TOUCH-MineCraft_1.12_Base_for_Mods/forge-1.12.2-14.23.4.2705-mdk
* TO:   ~/Documents/__DEVELOPMENT__/nfr/minecraft/1.12/modname

#### open IntelliJ and import

File -> Open... navigate to mod_name dir
* OFF auto-import
* ON create dirs for empty content
* OFF create seperate module per source set
* ON use default gradle wrapper (recommended)
* empty - Gradle Home (wasn't empty in the video, so not sure this is correct)
* 1.8 - Gradle JVM
* .idea - Project Format
* Save and Open in New Window

#### configure gradle

Open gradle config
* View -> Window Tools -> Gradle
* (may need to refresh to see new modname listed)
* Rt-click modname -> Open Gradle config

Make changes
* group = FROM: "com.yourname.modid" TO: "com.nfr.modname"
* archivesBaseName = FROM: "modid" TO: "modname"
* sourceCompatibility = targetCompatibility should be '1.8'

NOTE: This either didn't get saved or got reset.  I had to change again when first testing running Minecraft.

#### update gradle

Open terminal in IntelliJ
* run command: ./gradlew wrapper --gradle-version 3.3

#### import gradle project

There is a popup type window in the lower left.  Once gradle is updated in the previous step, you can click Import Changes in that box.

Watch status of gradle build in the status bar at the bottom of the window.

#### configure setupDecompWorkspace task

* View -> Window Tools -> Gradle (or click Gradle in right side doc)
* click Refresh icon
* modname -> Tasks -> forgegradle
  * Rt Click setupDecompWorkspace -> Create
  * VM Options:  -Xmx4g -Xms4g  (increases memory for this task)
  * check Single Instance Only (at top of dialog)
* Run
  * Rt Click setupDecompWorkspace -> Run (may take a few minutes to complete; decompiles minecraft)
* click Refresh icon
  * expand Dependency dir to see dependencies are filled in

#### create run shortcuts

* View -> Window Tools -> Gradle (or click Gradle in right side doc)
* modname -> Tasks -> forgegradle
  * Rt Click genIntelliJRuns -> Run (pretty quick)

### Run Minecraft

* At top right, select Minecraft Client from select list and click Run arrow >
* First time, may need to set some configurations...
    * VM Options:  -Xmx4g -Xms4g  (increases memory for this task)
    * Use classpath of module: select modname
    * Run
* Once Minecraft loads, click Mods and go to the end of the list and see Example Mod.


By default, the mod will show up as Example Mod.  This can be changed by...
* edit src/main/resources/mcmod.info
  * modid - FROM: 'examplemod' TO: 'modname'  (leave as examplemod until more updates are made in src/main/java/com/example/examplemod/ExampleMod.java)
  * name - FROM: 'Example Mod' TO: 'Mod Name'
  * description - FROM: 'Example placeholder mod.' TO: "My first mod in IntelliJ."
  * authorList - FROM: ["ExampleDude"] TO: ["Mom", "Nathan"]
  * credits: FROM: "The Forge and FML guys, for making this example"  TO: "The Forge and FML devs, for making this example"




NEED TO TEST forking this from github as a starting point.





## REMAINING IS README FROM FORGE

-------------------------------------------
Source installation information for modders
-------------------------------------------
This code follows the Minecraft Forge installation methodology. It will apply
some small patches to the vanilla MCP source code, giving you and it access 
to some of the data and functions you need to build a successful mod.

Note also that the patches are built against "unrenamed" MCP source code (aka
srgnames) - this means that you will not be able to read them directly against
normal code.

Source pack installation information:

Standalone source installation
==============================

See the Forge Documentation online for more detailed instructions:
http://mcforge.readthedocs.io/en/latest/gettingstarted/

Step 1: Open your command-line and browse to the folder where you extracted the zip file.

Step 2: Once you have a command window up in the folder that the downloaded material was placed, type:

Windows: "gradlew setupDecompWorkspace"
Linux/Mac OS: "./gradlew setupDecompWorkspace"

Step 3: After all that finished, you're left with a choice.
For eclipse, run "gradlew eclipse" (./gradlew eclipse if you are on Mac/Linux)

If you prefer to use IntelliJ, steps are a little different.
1. Open IDEA, and import project.
2. Select your build.gradle file and have it import.
3. Once it's finished you must close IntelliJ and run the following command:

"gradlew genIntellijRuns" (./gradlew genIntellijRuns if you are on Mac/Linux)

Step 4: The final step is to open Eclipse and switch your workspace to /eclipse/ (if you use IDEA, it should automatically start on your project)

If at any point you are missing libraries in your IDE, or you've run into problems you can run "gradlew --refresh-dependencies" to refresh the local cache. "gradlew clean" to reset everything {this does not affect your code} and then start the processs again.

Should it still not work, 
Refer to #ForgeGradle on EsperNet for more information about the gradle environment.

Tip:
If you do not care about seeing Minecraft's source code you can replace "setupDecompWorkspace" with one of the following:
"setupDevWorkspace": Will patch, deobfuscate, and gather required assets to run minecraft, but will not generate human readable source code.
"setupCIWorkspace": Same as Dev but will not download any assets. This is useful in build servers as it is the fastest because it does the least work.

Tip:
When using Decomp workspace, the Minecraft source code is NOT added to your workspace in a editable way. Minecraft is treated like a normal Library. Sources are there for documentation and research purposes and usually can be accessed under the 'referenced libraries' section of your IDE.

Forge source installation
=========================
MinecraftForge ships with this code and installs it as part of the forge
installation process, no further action is required on your part.

LexManos' Install Video
=======================
https://www.youtube.com/watch?v=8VEdtQLuLO0&feature=youtu.be

For more details update more often refer to the Forge Forums:
http://www.minecraftforge.net/forum/index.php/topic,14048.0.html
