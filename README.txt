///////////////////////////////////////
// skeinforge-tools
///////////////////////////////////////

Tools for the skeinforge toolchain developed by members of the MakerBot community.

This repo started with the Raftless tool developed by Eberhard Rensch "Zaggo", and currently maintained by Miles Lightwood "TeamTeamUSA". Raftless has been tested with skeinforge 2010-02-05.

CURRENT TOOLS
* Raftless for skeinforge bundled with ReplicatorG 0017
* Raftless

///////////////////////////////////////
// Raftless for skeinforge bundled with ReplicatorG 0017
///////////////////////////////////////

Installation
------------
1. Download ReplicatorG 0017 from http://code.google.com/p/replicatorg/downloads/list
2. Download replicatorg-0017/raftless-RepG0017.zip.
3. Uncompress raftless-RepG0017.zip
4. Move skeinforge.py to the skeinforge folder. Overwrite existing file.
5. Move export.py and raftless.py to the skeinforge/skeinforge_tools folder. Overwrite existing files.

Usage
-----
I have not been able to get raftless to work from within ReplicatorG. I have been able to get it to work via launching skeinforge and skeining a file using it.

1. Launch skeinforge
2. Open the Raftless tool. Select 'Activate Raftless'. Click Save Preferences. This will create the raftless preferences file.
3. Open the Raft tool. Unselect 'Activate Raft'. Click Save Preferences. This will create the raft preferences file that works with raftless.
4. Click 'Skeinforge' and select file to skein.

///////////////////////////////////////
// Raftless - http://pleasantsoftware.com/developer/3d/2009/12/05/raftless/
///////////////////////////////////////

Installation
------------
1. Download reprap_python_beanshell_2010-02-05.zip at github. This collection of python scripts is what is commonly known as skeinforge.
2. Uncompress reprap_python_beanshell_2010-02-05.zip
3. Move raftless.py to the skeinforge_tools/craft_plugins folder.
4. Edit skeinforge_tools/profile_plugins/extrusion.py and add Raftless to the tool chain sequence by inserting ‘raftless’ into the tool sequence in getCraftSequence(). The best place is at the end of the sequence, right before ‘export’.

Usage
-----
As reported previously, printing on a heated build surface not only permits (almost) warp-free printing, but also eliminates the need for rafts for simple shaped objects (simple as in rectangular footprint).

As soon as the base shape of an object becomes more complex, things go likely wrong: Most of the time, the more complex perimeter lines don’t stick and ripped off the build surface by the passing nozzle.

To solve this problem, I played around with several parameters of the gcode files, like feed rate and flow rate.

It turns out that, if extruded “slow enough”, also complex shapes are easily printable without a raft.

IMG_4709 After testing this for a while by post-processing gcode files manually (i.e. editing the gcode files in a text editor), I started to write a new tool for the skeinforge tool chain.

By integrating a ‘Raftless’ tool into skeinforge, I not only save a lot of time (it’s rather time consuming to edit gcode files each time before printing), but I’ve also much more (and easy!) control over what to slow down. Although it’s possible to change each single line of gcode in a text editor, it’s quite a challenge to navigate through thousands of ‘G1 X Y Z F’ lines without getting lost or insane.

Anyway, I just finished a new tool for the skeinforge tool chain:
“Raftless”

Raftless is a script to prepare a gcode file for raftless printing.

Raftless Settings

The default ‘Activate Raftless’ checkbox is off, since the mutual exclusive ‘Raft’ script is activated by default. In order to use the Raftless script, you want to desactivate the Raft script first. If both scripts, Raft and Raftless, are activated, the Raftless script (which runs after the Raft script) automatically detects the already created raft. In this case, the Raftless script is skipped and a warning message is printed to the console.

The “1st Perimeter Feed Rate over Feed Rate” preference defines the feed rate during the extrusion of the 1st layer’s perimeter lines. The preference is a ratio of the normal extrusion feed rate as configured in the ‘Speed’ script. The default value is .5, which means half the normal feed rate.

The “1st Perimeter Flow Rate over Flow Rate” preference is the ratio of the filament feedrate during the extrusion of the 1st layer’s perimeter lines. Since the feed rate is slower than normal, you might want to reduce also the flow rate in this case. This preference is a ratio of the normal flow rate (as configured in the ‘Speed’ script). The default is 1. (same flow rate as normal).

If “Add Extrusion Intro” is on, an additional straight extrusion line is added to the start of the first perimeter. This line starts at the coordinates ‘Extrusion Intro Max X Absolute’/'Extrusion Intro Max Y Absolute’. These both values are absolute (positive) values. The script automatically negates one or both of these values, according to the location of the first regular extrusion.

Please note, that Add Extrusion Intro doesn’t check for collisions with the perimeter lines. If necessary, you want to change the max X/Y values manually.

If you’re interested in raft-less printing, you should definitely give the ‘Raftless’ tool a try.

I wrote the Raftless script based on the most recent version of skeinforge (“created at 2009-11-06″) as included in the not-released-yet newest Replicator G version. In the meantime, you can download this version of skeinforge from the public Makerbot GITHub repository. Please note, that all unreleased software in this repository is per definition ”beta”. So: no guarantees.

Any feedback is highly appreciated!



