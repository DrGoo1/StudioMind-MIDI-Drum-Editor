# StudioMind MIDI Drum Editor 0.2.18

**User guide · macOS beta for Universal Audio LUNA**

StudioMind MIDI Drum Editor is a docked LUNA add-on for inspecting and editing drum MIDI. It shows each drum sound on its own row, with diamond-shaped hits and aligned Velocity, MIDI Control Change (CC), and Pitch Bend lanes. It works on MIDI already in a LUNA session; it does not supply a drum instrument or a kit.

## Install and open

1. Use **LUNA 3.1.2 or newer**. This beta was tested on an Apple-silicon Mac with LUNA 3.1.2, build 4693. Version 0.2.18 adds the Umbo Gumbo logo and retains the 0.2.17 editing behavior. Windows and other configurations are not qualified.
2. Open the **StudioMind MIDI Drum Editor 0.2.18.lunaaddon** file with LUNA. If it came in a ZIP, extract it first and open the individual `.lunaaddon` file. On a Mac’s first LUNA add-on install, LUNA may request administrator approval. If updating the regular StudioMind add-on, read the version and name in the **Replace** prompt before confirming.
3. In LUNA’s **Timeline**, select a MIDI clip on an instrument track. Open **Add Ons → Editors → StudioMind MIDI Drum Editor**. The panel docks at the bottom of the Timeline and its own header says **Drum Grid**.
4. Check the **Clip** menu and the clip/track name before editing. **Follow selection** tracks your LUNA selection; turn it off or choose a clip from **Clip** to work on a specific source. Try your first edits on a duplicate or disposable clip.

The panel starts in **READ ONLY**. Inspecting a point, changing the display, or scrolling does not change MIDI. Stop playback and recording before enabling an edit mode. Enable only the mode you need, then switch it off when finished.

## Find, inspect and hear hits

- **Click a diamond** to see the hit’s timing, MIDI note number, velocity and channel. Hover a hit or controller handle for details. Clicking empty space moves the editor’s inspection cursor; it does not move LUNA’s transport or insert MIDI in ordinary inspection mode.
- **Scroll vertically over the note grid** to move drum names and their diamonds together. Velocity and controller lanes remain separate. Scroll over the controller area to see more lanes without moving the note grid. For a short dock, drag the top edge of the whole dock upward in LUNA to reveal more.
- **Use the bottom horizontal scrollbar** to move the ruler, notes and controller lanes together. **Fit clip** fits the clip where the zoom range allows. Use the **Zoom** slider for finer work. The shared ruler uses LUNA’s bar and beat positions when available.
- **Channel** filters the displayed data. **Used sounds** hides unused articulation rows. Click a drum name to highlight its hits; click it again to clear the focus. This is a visual highlight, not a selection of all hits for editing.
- **Note color** can show **Articulation**, **Velocity**, **Pitch class**, or **Controller value**. With controller coloring, choose **Color CC**. A note is colored only when the editor can match one unambiguous point at the same tick and on the same channel. Missing and shared matches stay neutral.
- **Audition clicks** sends a short preview to the selected track’s compatible software instrument. It defaults to off and does not insert or record a note. If it is unavailable or silent, check the track’s instrument, patch, MIDI channel and routing. Muted or ineligible hits do not audition.

The built-in row names are **General MIDI candidates**. A Kontakt or custom kit can map pitches differently. Trust the displayed MIDI note number and your instrument’s map when a label or sound does not agree.

## Move an individual hit

1. Turn **Edit: On** and choose a single, unmuted hit.
2. Drag its diamond horizontally. The draft follows the pointer; releasing commits the guarded timing change. Press **Esc** during a drag to cancel before release.
3. **Snap: On** uses the chosen **Grid** for the move destination. Turn Snap off to place the hit freely. The **Grid** choices include **Bar**, **Beat (meter)** and **1/4** through **1/128**. **Off** hides grid lines; if Snap stays on, the last subdivision remains the snapping reference.

A timing move keeps pitch, channel, velocity and duration. The editor refuses unsafe clip-boundary crossings, ambiguous note pairs, and overlaps with another hit of the same pitch and channel.

### Nudge by an exact amount

With **Edit: On**, click one hit, choose a **Nudge step** from **1/128** through **1/4**, then click **←** for earlier or **→** for later. With focus in the note grid, the Left and Right arrow keys do the same. Nudge moves the hit by the chosen interval **from its current position**, regardless of Snap. For example, one **1/64** nudge on an off-grid hit preserves that hit’s off-grid phase. Holding an arrow does not repeat the nudge. If the keys reach LUNA instead, use the on-screen arrows.

## Quantize a selected group

1. Open **Advanced Quantize…** and turn **Edit: On**.
2. Click one diamond, then **Shift-click** other hits to add or remove them. Check the selection count. **Clear selection** resets the group. You can select up to 64 eligible hits in the current clip.
3. Pick the dialog’s own **Grid** (**1/4** through **1/64**), **Strength** and **Swing**. These are independent of the main Snap and Grid controls.
4. Click **Apply to selected hits**. Read the status message before making another edit.

**Strength** is how far a hit moves toward its target: 100% moves all the way, 50% halfway, and 0% leaves timing unchanged. **Swing** delays alternate subdivisions on that grid; 0% gives straight timing. Start with a modest amount, listen, then adjust. Swing changes where the targets lie; Strength controls how far the selected hits move toward them.

Quantize changes timing only. It does not shorten hits, change velocities, quantize controllers, or move unselected notes. It needs an available LUNA bar/meter grid. LUNA’s own Quantize window (**⌘⇧U**) is separate and has additional options.

## Velocity, CC and Pitch Bend

| Task | What to do |
| --- | --- |
| **Change a hit’s velocity** | Turn on **Velocity Edit** and drag that hit’s velocity bar or round handle vertically. Up increases attack velocity; down decreases it. Release to commit. This does not alter timing. |
| **Show a CC lane** | Choose its number in **+ Show CC**. Use the lane’s **×** to hide it; hiding does not delete any MIDI. |
| **Change an existing CC value** | Turn on **CC Value Edit** and drag the existing round point vertically. Release to commit. Its time and channel stay the same. CC values range from 0 to 127. |
| **Insert a CC point** | Show the lane, turn on **CC Draw**, choose **Draw ch**, then click empty space in the lane. Horizontal position sets time and uses Snap when enabled; height sets value. This does not replace an existing point at the same controller, tick and channel. |
| **View or insert Pitch Bend** | Check **Pitch Bend** to show the bipolar lane. Turn on **Bend Draw**, choose **Draw ch**, then click empty space. The line at zero is the center; the displayed range is −8192 to +8191. This beta can insert bend points but does not offer dragging existing bend values or drawing a curve. |

**Draw ch → Auto** uses the clip’s channel only when there is exactly one. Choose the intended channel explicitly when more than one is in use, and make sure it matches any active channel filter. Controller and pitch bend messages affect their MIDI channel; they are not attached to individual drum hits. The stepped CC connector lines illustrate the last transmitted value until the next point on that channel. The handles are the actual events; the lines do not add events or create smooth ramps.

**Resize a lane:** drag the small grip at the **top** of the Velocity or controller lane. Drag **up to expand** and **down to shrink**. With a grip focused, Up and Down adjust height, Shift makes a larger step, and Home/End set the minimum/maximum. Resizing is a view change, not a MIDI edit.

## Undo and shortcuts

| Control | Action |
| --- | --- |
| **LUNA Edit → Undo**, or **⌘Z** | Undo the last committed LUNA edit. One successful Nudge or Quantize Apply is one Undo. Verify the intended hit or values returned before continuing. |
| **Esc** | Cancel an in-progress pointer edit or lane resize before release. |
| **← / →** in the note grid | Nudge one selected hit by the chosen step when Edit is armed. On-screen arrows are also available. |
| **R / T** or **⌘[ / ⌘]** | Zoom out / in when focus is not in a field or control. Use the Zoom slider if a shortcut is routed elsewhere. |
| **⌘⇧U** | Open LUNA’s native Quantize window, separate from the add-on. |

## Troubleshooting and beta limits

- **The add-on is missing:** Check the LUNA version, that you opened the extracted add-on file, and that you are on the **Timeline**. Look under **Add Ons → Editors**, not plug-in inserts. If the panel prompts you to connect, use **Connect local LUNA**, then reselect a MIDI clip.
- **No hits or unexpected clip contents:** Select the actual MIDI clip, not a rendered audio track. Check **Clip**, **Follow selection**, **Channel** and **Used sounds**. In overlaps the panel can show source events rather than comp playback; editing an overlapping or ambiguous source is restricted.
- **An edit is disabled or refused:** Stop the transport, disarm recording, and check that the source is visible, unmuted and editable. Select an eligible hit or a valid explicit group, and arm only the required mode. Read the on-screen message before retrying. If it says an edit might have landed, inspect LUNA first instead of applying twice.
- **Can’t see all the lanes:** Scroll separately over the notes and controllers, or make the native dock taller. **Fit clip** helps if the time range is off screen. **×** hides a controller lane without affecting the source.
- **Compatibility:** This is a beta, not a replacement for LUNA’s complete MIDI editor. Kit-specific articulation mapping, controller curves, existing Pitch Bend value editing, Windows compatibility and every third-party instrument/routing combination are outside the verified scope. On LUNA 3.1.2 for macOS, the native tests covered single-hit Nudge, selected-note Quantize at straight timing and one Undo for each. Non-default Strength/Swing and the separate scroll and controller-grip interactions also have automated checks, but were not all exercised in native LUNA.
