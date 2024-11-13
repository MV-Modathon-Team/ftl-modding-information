If you're new to Superluminal, I recommend watching and following along with the video tutorial for using it to create player ships for Hyperspace and Multiverse.

## FTL HS/MV Player Ship Tutorial
[![FTL HS/MV Player Ship Tutorial](https://img.youtube.com/vi/3PSGVwlA95o/maxresdefault.jpg)](https://www.youtube.com/watch?v=3PSGVwlA95o)

There are a few things I missed when making this tutorial. Under Ship Loadout and Properties, your Layout Filename and Image Namespace should also use a unique prefix like the one for the Blueprint Name.

[[/img/ship-creation-guide/layout-name.png]]

Instead of setting the system maximums for shields and drones directly in the XML, you can do it in Superluminal by ticking the Enable Max Level box.

[[/img/ship-creation-guide/system-max.png]]

You can also link weapon mounts to gibs so that weapons in those slots will follow the linked gib when the ship explodes. First, hide everything except the gibs using either the number keys or by going to View > Ship Components/Images. Select the weapon mount you want to link and click the button under Linked Gib, then click the gib that you want to link it to.

[[/img/ship-creation-guide/linked-gib.png]]

## Miniships

If you're making a ship for Multiverse, you'll need to add some icons to the miniship. All the existing miniship icons are in the [assets/miniship icons](../blob/master/assets/miniship%20icons) folder of this repository, and there's more info about how to use them in the [About the Icons](../blob/master/assets/miniship%20icons/About-the-Icons.md) file in that folder.

You should save a copy of your miniship without the icons for a couple reasons. The first is that you may change the loadout of your ship later and it'll be much easier to update the icons accordingly with the original miniship. The second is that you can add it to your mod to remove the icon box from the silhouette of the ship while its locked. To do this, place it in `img/customizeUI`, the same folder that the main miniship is stored in. Make sure it's name is the same as the main miniship, but with `_base` added to the end before the file extension. For example, if the main miniship is named `miniship_mup_cvx_testrel_a.png`, call the miniship without the icons `miniship_mup_cvx_testrel_a_base.png`.

## Thruster Animations

If you want to add custom thruster animations to your ship like the ones the vanilla Kestrel and Federation Cruiser have, first use the [Animations Guide](Animations-Guide) to add them to to your mod's `animations.xml`. After that you'll need to determine the coordinates they should be placed at relative to your ship's hull image. To do this in GIMP, you can place a frame of the thruster animation on top of the hull where they should appear in-game, then place the cursor over the top-left corner of that thruster frame. The coordinates of the cursor appear in the bottom-left corner of the GIMP application window.

[[/img/ship-creation-guide/thruster-coords.png]]

Once you know the coordinates, you can add the thrusters to your ship's layout file. Find the `.xml` file in the `data` folder with the same name you used in the Layout Filename field when you created the ship in Superluminal. Open it in your editor of choice and add the following XML:

```xml
<thrusters sync="true">
    <thruster x="49" y="15">your_thruster_animation_name</thruster>
    <thruster x="49" y="283">your_thruster_animation_name</thruster>
</thrusters>
```

Replace `your_thruster_animation_name` with the name you gave your thruster animation in `animations.xml`, and replace the coordinates with the coordinates of your thrusters. Add as many `thruster` tags as are necessary. If you set the `sync` attribute in the `thrusters` tag to `false`, Then the frame each animation starts on will be randomized. If set to `true` they will all start on the same frame.

## Generating Custom Shield Images

UNDER CONSTRUCTION

## Unlock Conditions and Icons

UNDER CONSTRUCTION

## Combining Mods

UNDER CONSTRUCTION
