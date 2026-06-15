# Face Tracker Hardware Design 

An open-source hardware project for building compact face tracker based on [Babble Project](https://babble.diy/).


## 🔧 Overview

Electronics design made with Altium Designer, including schematics, layout, and manufacturing files (Gerbers, CPL, BOM). Mechanical parts designed in SolidWorks.

## 📦 Features

- Modular and compact design
- Increased power efficiency
- Could be used both in wireless and USB mode

## 🖼️ Gallery

![PCB Back](Images/pcb_back.png)
![Assembled Unit](Images/tracker_front_camera.png)
![Tracker on Quest 3](Images/tracker_on_quest3.png)

# BabbleVR_NVer Assembly Guide

## 1. Manufacturing assumption

This guide assumes the PCB has already been ordered through JLCPCB using:

* Gerber ZIP
* BOM CSV
* CPL / Pick-and-place CSV
* Double-sided SMT assembly
* 4-layer PCB
* ENIG finish recommended
* JLCPCB-assembled SMT parts

Do not treat the first batch as production-ready. Build and test the first units as prototypes.

## 2. Parts and tools needed after JLCPCB assembly

### Printed / mechanical parts

Use the mechanical files from the repository:

* `CaseTop_01.STL`
* `CaseBottom_01.STL`
* `ButtonCover_01.STL`
* `Quest3_MountScobe_01.STL`
* optional hinge/mount parts from the mechanical design folder

Print the case in a material that handles repeated flexing and heat better than brittle PLA. PETG, ASA, or nylon are better choices.

### Non-JLCPCB parts

You still need:

* 90-degree or near-90-degree OV2640/compatible face camera module
* 24-pin, 0.5mm-pitch FPC camera tail, matching the board connector
* 1S LiPo battery that physically fits the case
* 2-pin battery connector matching the board footprint
* M2 self-tapping screws
* USB-C cable
* Kapton tape or thin double-sided electronics tape
* Optional thin foam pad for camera strain relief

### Tools

* ESD-safe tweezers
* Magnifier or microscope
* Multimeter
* USB current meter or current-limited bench supply
* Plastic spudger
* Small screwdriver
* Flush cutters or hobby knife for cleaning printed parts

## 3. Inspect the JLCPCB-assembled board

Before powering anything:

1. Inspect USB-C connector X2.
2. Inspect FFC camera connector X1.
3. Inspect battery connector X3.
4. Inspect ESP32-S3 module D1.
5. Inspect charger IC D5.
6. Inspect D6 1.2V LDO.
7. Inspect the IR LEDs and ESD protection parts.
8. Look for solder bridges, tombstoned passives, rotated LEDs, or lifted connector pins.

Do not plug in the battery yet.

## 4. First power-up without battery

1. Connect USB-C only.
2. Use a USB current meter if available.
3. Check that the board does not immediately overheat.
4. Measure major rails:

   * 3.3V rail
   * 2.8V rail if present
   * 1.2V rail from D6
5. If any regulator gets hot quickly, unplug immediately.
6. If the current draw is excessive or unstable, do not insert the battery.

Only continue if USB power is stable.

## 5. Battery check

Before plugging in the LiPo:

1. Verify battery connector polarity with a multimeter.
2. Verify the PCB battery connector polarity.
3. Confirm the LiPo is a single-cell 3.7V nominal pack.
4. Confirm it physically fits without crushing the pouch cell.
5. Plug in the battery only after USB-only power-up passes.

Never force the battery into the shell. Do not fold or pinch the LiPo.

## 6. Camera selection

The camera should be a small OV2640-style DVP camera module with:

* 24-pin FPC tail
* 0.5mm pitch
* 3.3V logic
* FOV around 90 degrees if possible
* 75mm cable preferred if the camera must route around the enclosure
* No bulky board behind the lens
* Lens positioned so it can aim at the lower face from the headset

A true 90-degree version may need to be sourced from an OEM/supplier listing. If an exact 90-degree camera is not available, use a nearby FOV such as 100 or 120 degrees and compensate with crop settings in software.

Avoid ultra-wide 160-degree fisheye unless the case and software crop are tested, because the image can distort the mouth and jaw.

## 7. Camera installation

1. Open the FFC latch carefully.
2. Insert the camera ribbon straight into X1.
3. Make sure the exposed contacts face the correct side of the connector.
4. Close the latch gently.
5. Do not crease the FPC cable sharply.
6. Route the cable so the case does not pinch it.
7. Mount the camera in the front camera opening.
8. Temporarily tape the camera in place before final enclosure closure.
9. Power the board and check the camera feed before closing the case.

If the image is upside down or mirrored, fix it in software first before rotating hardware.

## 8. Case assembly

1. Test-fit the PCB in the bottom shell.
2. Confirm USB-C lines up with the shell opening.
3. Confirm the switch/buttons move freely.
4. Install the button cover.
5. Route the camera FPC.
6. Seat the camera in the front opening.
7. Add a small piece of Kapton or foam to reduce FPC strain.
8. Place the battery where it cannot press into sharp pins or solder joints.
9. Close the top shell.
10. Install M2 self-tapping screws.
11. Do not overtighten; stop when the shell is snug.

## 9. Mounting to headset

For Quest 3:

1. Attach the Quest 3 mount.
2. Mount the tracker below the headset front.
3. Aim the camera upward toward the lower face.
4. The feed should include:

   * lower face
   * mouth
   * jaw
   * tip of nose / nostrils
   * cheek movement area
5. Reposition the tracker until the mouth stays visible while talking.

## 10. Firmware and software setup

1. Connect the tracker over USB.
2. Put the device into configuration mode if required by the firmware.
3. Use Baballonia / Babble software to configure wired or wireless mode.
4. For wireless mode, use 2.4GHz Wi-Fi, not 5GHz.
5. Reboot the tracker.
6. In wired mode, the device should appear as a USB camera.
7. In wireless mode, connect to the tracker over the local network.
8. Open the camera feed.
9. Set crop mode.
10. Crop to the lower-face region.
11. Switch back to tracking mode.
12. Verify stable tracking before using it in VRChat.

## 11. Final test checklist

Before calling the unit finished:

* USB-C works
* battery charges
* battery powers the unit
* no regulator overheats
* camera feed is visible
* image is not black
* image is not badly overexposed
* IR LEDs work
* buttons work
* case closes without crushing the FPC
* mount holds the tracker securely
* mouth and jaw stay in frame
* Babble software can connect
* VRChat / VRCFaceTracking receives tracking data

## 12. Notes for revision 2

Track these problems from the first build:

* Camera FPC too short or too long
* Camera angle wrong
* USB-C hard to access
* battery connector polarity confusion
* case pinching the cable
* LEDs too dim or too bright
* board gets warm
* weak mount
* mouth not centered in feed
* bad crop caused by too-wide or too-narrow lens


