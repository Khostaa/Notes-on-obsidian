![[File Structure.png]]
# Project
## Photos
## Videos
## Temp
## Project Files
### Sound and Music
save the sounds, SFX and Music required for particular project into this folder.
### Davinci
save the project library location in this folder **Project/Project Files/Davinci**
#### Working Folders
##### Proxies
save the proxies of a project into this folder
##### cache
save the render cache of a project into this folder
##### gallery stills
save the gallery still of a project into this folder.

### After Effects
save the project files of after effects files into this folder.

# Project Library
creates as required. 
- generally used to distinguish between working environments of each project type and group them accordingly.
# Exporting Project
## Exporting Project (.drp file)
if the already as all the project files then the file with this extension can be exported and shared with them.

## Exporting Project Archive (.dra file)
this file takes up more space and exports all the things to get started with project right away if shared without dependency of project files with new user or not.

# Project Backups
## To save a project backup
DaVinci Resolve > Preferences > User and open the Project Save and Load Panel.

## To open a project backup
 - open project manager.
 - right click > Project Backups > select required version of Project

# Project Notes
- To keep track of text notes associated with each project.
- can be accessed using File > Project Notes

# Dynamic Project Switching
- to use it, it must be enable by right clicking on Project Manager. it will remain enabled until you turn it off.
- Open any project, reopen Project Manager and open any other project. now can be switched between multiple projects from top bar section of Davinci interface.

# Edit page
| Shortcuts      | Functions                               |
| -------------- | --------------------------------------- |
| J              | Play backward                           |
| K              | stop playback                           |
| L              | Play forward                            |
| Hold J/L       | Start Playback fast in either direction |
| Release J/L    | Stop playback                           |
| Shift + J      | Play fast backward                      |
| Shift + L      | play fast forward                       |
| Shift + K      | Play slow forward                       |
| Hold K + J     | Play slow backward                      |
| Hold K + L     | Play slow forward                       |
| Hold K + Tap J | move playhead back 1 frame              |
| Hold K + Tap L | move playhead forward 1 frame           |
| Shift + S      | Change Clip Speed Menu of timeline      |
## Using Time code entry
-  pressing **=** key focuses on *timecode*
	- then press numbers without **:(colon)** to move to that point in timeline
	- **+** followed by numbers on keyboard add the time to existing timecode of current playhead position.
	- *-* followed by numbers on keyboard gets the playhead back to previous frames for current playhead position.
	- **.(dot)** adding dot after no. automatically fills in '00' to the timecode
- with a edit point selected of clip **+** or **-** deletes/add frames based on the entry numbers.

## Nudge commands
- path to make changes in no. of frames nudged
DaVinci Resolve -> preferences -> user -> editing -> Default fast nudge length

- Select the clip then
	- *comma ,* - to move edit/clip left a frame
	- *period .* - to move edit/clip right a frame

	- Shift + comma = move edit/clip left *5* frames
	- Shift + Period = move edit/clip right *5* frames
		- *5* frames is by default. can be change in path mentioned above.

- Shorten/ elongate clips
	-  Select beginning/end of clip then *.* or *,*
	- or, Shift + . or shift + , - to extend/reduce 5 frames at a time
	- if at intersection of two clips, it extends one and trims the other.

## Viewer Overlay 
This includes - transform, fusion overlay, zoom, etc menu at left bottom part of viewer

| Shortcuts         | Functions                                                                                                                                                                                                       |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Shift + Q         | Crop                                                                                                                                                                                                            |
| Shift + N         | Dynamic Zoom                                                                                                                                                                                                    |
| Shift + F         | Fusion overlay                                                                                                                                                                                                  |
| Shift + Tab       | Transform                                                                                                                                                                                                       |
| Shift + ~         | Toggle on/off                                                                                                                                                                                                   |
| / - Forward Slash | To play around selection - pre/post roll up can be adjusted from path above in Nudge commands - Playhead rests are current postion after playback. with a clip selected, Playhead moves to the end of that clip |
|                   |                                                                                                                                                                                                                 |



