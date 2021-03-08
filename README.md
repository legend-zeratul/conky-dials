# conky-dials - Minimal dials config

MIT License. Legend Zeratul.

A simple, minimal system monitor like the one shown in the screenshots below:

[TBD: Screenshots]

The desktop shown in the above screenshot is standard XFCE - with Conky providing both the workspace indicator and the system monitor dials. The workspace indicator is read only (you cannot click on the indicator to switch workspaces - conky cannot handle clicks).

Pls note that this is work in progress - I only have a single line dial today - I will be updating the script to show both RAM/SWAP, other drives, etc. as well.

There are two parts to the files here:
- 1. The system monitor (dials) - conkyrc-dials.conf - and -
- 2. The workspace indicator - conkyrc-workspaces.conf

For the purpose of this readme, I'm going to assume that you are interested in the system monitor more than the workspaces, so the instructions for the system monitor part is given first.

## 1. Installation - System Monitor (Dials) ##

### 1.1. Conky Setup/Installation ###
The dials are written in Lua, rendered through Cairo - so first thing we need is Conky installed with both Lua/Cairo support:

#### For Arch/EndeavourOS/Manjaro users ####
- Using your package manager (yay, pamac, pacman, etc), install 'lua 5.4.2-1' first
- Install the 'conky-cairo' package (1.11.3-1 as of the time of this script) 
- Find/install the 'Inter' font (freely available online, package 'inter-font')
- Run 'conky -v' from a Terminal - to check that conky/lua bindings have been installed correctly. If you see the following output, we're good:

~~~
Lua bindings:
  * Cairo
  * Imlib2
  * RSVG
~~~

#### For Ubuntu/Debian users ####
(These instructions havent been tested yet - I'm working on it - will post an update shortly.)

- Install the 'conky-all' package (```sudo apt install conky-all```)
- Install 'fonts-inter' (```sudo apt install fonts-inter```)

### 1.2. Install/Run the dials script ###
- Copy/save/extract the conkyrc-dials.conf and the conky-dials.lua files to some folder (lets assume both scripts are in ```~/.conky/```)
- If you have saved the files to a different folder, then pls open/update the path to the lua file in conkyrc-dials.conf (you can ignore this if you've saved the files to .conky under your home folder)
- The script refreshes every 10 seconds (battery life saving) - you can edit this setting (update_interval) in the conkyrc-dials.conf file 
- Run conky with ```conky -c ~/.conky/conkyrc-dials.conf```

**Customization**
- The script support two themes - the colored dials are named 'nord' and the white dials are named 'snow'
- For some wallpapers, the white dials work better, for some the colored dials work better, the default theme is snow
- If you want to change the selected theme, find the line in the lua script that selects the theme (curr_theme=themes.snow) and change it to themes.nord (changes to the Lua script needs a restart of conky)
- Create a conky.desktop file under the .config/autostart directory to start the script upon login

**Troubleshooting**
- Only clock shows up: either the path to the lua script is incorrect, or the Lua/Cairo bindings are not enabled - you might have to uninstall existing conky and repeat the installation instructions above (or post an issues log)

## 2. Installation - Workspace indicator ##

### 2.1 Installation/Setup ###
- This script does not need Cairo/Lua, can work with a default conky installation, however it requires font-awesome to be installed (the indicator circles are font-awesome glyphs) - install both Conky and font-awesome through your normal package manager

### 2.2. Install/run the workspaces script ###
- Copy/save/extract conkyrc-workspaces.conf to some folder (lets assume ```~/.conky/```)
- Run conky with ```conky -c ~/.conky/conkyrc-workspaces.conf```

**Known Issues**
- The indicator is read only - you cannot click the dials to switch (conky doesnt accept clicks - I know what command to execute if I had a mechanism to handle clicks - so if you know how to do this, pls do message)
- As a tradeoff between performance and response time, this script is set to refresh every second - this might mean that there can be a small pause between your desktop actually switching to a workspace vs when the indicator refreshes


