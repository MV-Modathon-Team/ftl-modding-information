If you're new to Superluminal, I recommend watching and following along with the video tutorial for using it to create player ships for [Hyperspace](https://subsetgames.com/forum/viewtopic.php?t=35095) and [Multiverse](https://subsetgames.com/forum/viewtopic.php?t=35332).

## Using Superluminal

To learn how to use Superluminal you can watch this tutorial.

### [FTL HS/MV Player Ship Tutorial](https://www.youtube.com/watch?v=3PSGVwlA95o)
[![FTL HS/MV Player Ship Tutorial](https://img.youtube.com/vi/3PSGVwlA95o/maxresdefault.jpg)](https://www.youtube.com/watch?v=3PSGVwlA95o)

There are a few things I missed when making this. Under Ship Loadout and Properties, your Layout Filename and Image Namespace should also use a unique prefix like the one for the Blueprint Name.

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

## Creating Custom Shield Images

### Manual Method

First, download [assets/Shield_Template.xcf](../blob/master/assets/Shield_Template.xcf) from this repository and open it in GIMP. Select the Shield layer, go to Layer > Scale Layer, and click the chain icon to the left of the dimensions to unlink them. Enter the dimensions you want and click the Scale button.

When the shield is the size you want, use the Select by Color Tool to select all of the blue pixels on the Honeycomb layer. With the selection active, go back to the Shield layer, then go to Colors > Hue-Saturation. Make the following adjustments:<br/>
Hue: -2<br/>
Lightness: +38<br/>
Saturation: +7<br/>

Press the OK button, then click the eye icon next to the Honeycomb layer. Press Shift+Ctrl+A to deselect the honeycomb pattern. If you've done everything correctly, the pattern should now appear on the shield. To finish, go to Image > Crop to Content, then go to File > Export As. Save the image with the appropriate name and place it in the `img/ship` folder of your mod.

### Script Method

If you have Python and Pillow installed as shown in the [Cloak Image Tutorial](https://youtu.be/08GqtK9hUjE), you can use the script included with Multiverse to generate a shield image automatically. Open the latest Multiverse assets `.zip` archive and extract `shield_base_bubble.png`, `shield_base_hex.png` and `shield-updater.py` from the `img/ship` directory. Place them in the same directory as your shield image and resize your shield image to whatever dimensions you want, then run `shield-updater.py`. When you're done, you can remove the three files extracted from Multiverse.

## Unlock Icons and Conditions

### Icons

Achievement Icons can be made using this palette.

[[/img/ship-creation-guide/pallete-achievement.png]]

To make an icon from your ship's hull image, you can follow AgentTHeKat's tutorial.

### [Icon Creation Turorial](https://www.youtube.com/watch?v=HNQs6TZ3xVw)

[![cheivements](https://img.youtube.com/vi/HNQs6TZ3xVw/maxresdefault.jpg)](https://www.youtube.com/watch?v=HNQs6TZ3xVw)

### Conditions

Once you've made the icon, give it the same name as the Layout Filename, with `_1` added to the end before the file extension. For example, if the layout is named `mup_cvx_testrel_a`, call the achievement icon `mup_cvx_testrel_a_1.png`. Put it in the `img/achievements` folder of your mod.

To define unlock conditions for your ship, open the `hyperspace.xml.append` file generated by Superluminal in the editor of your choice. You should find something similar to this:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="true" b="false" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_TESTREL">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
</mod:findLike>
```

To add unlock conditions, create a closing tag for the `ship` append and add an `unlock` child tag:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="true" b="false" c="false" secret="false">
        <unlock variant="a" silent="false">
            <type>1</type> <!-- A value between 0 and 5 -->
            <shipReq>PLAYER_SHIP_NAME</shipReq>
            <value>8</value> <!-- Used only for type 1 -->
            <otherUnlocks> <!-- Used only for type 3 -->
                <ship>PLAYER_SHIP_NAME_1</ship>
                <ship>PLAYER_SHIP_NAME_2</ship>
            </otherUnlocks>
            <victories> <!-- Used only for type 5 -->
                <victory>PLAYER_SHIP_NAME_1</victory>
                <victory>PLAYER_SHIP_NAME_2</victory>
            </victories>
        </unlock>
    </mod-append:ship>
    <!-- Etc... -->
</mod:findLike>
```

The `secret` attribute added to the `ship` tag determines whether its name is hidden while locked. If `true`, the ship will appear as "Unidentified Cruiser" when hovering over it in the ship selection screen.

The `variant` attribute determines which ship variant the unlock is for. If you have multiple variants, you can add an `unlock` tag for each. The `silent` attribute determines whether the unlock achievement appears in the top-right of the screen if you unlock the ship during a run.

The value of the `type` tag determines the method required to unlock it. There are six methods to choose from:<br/>
`0` - Ship is unlocked when the Flagship is defeated.<br/>
`1` - Ship is unlocked when you reach the sector defined by the `value` tag.<br/>
`2` - Ship is unlocked when you win the run (win conditions besides defeating the Flagship can be defined).<br/>
`3` - Ship is unlocked when all the other ships defined by `otherUnlocks` have been unlocked.<br/>
`4` - Ship is unlocked when some other condition is met, either by an `unlockCustomShip` tag in an event or a call of `AchievementTracker::UnlockShip` in a Lua script.<br/>
`5` - Ship is unlocked when you've won the game with all other ships under `victories`.

The value of `shipReq` determines which ship you have to be playing with to unlock the ship. This is typically used for unlocking different variants of the same class, or unlocking the next ship in order on the same page.

If you want to define multiple ways to unlock a single ship, you can add as many `unlock` tags for it as you want.

### Arrows

In vanilla, you can unlock new ship classes without completing their questlines by getting to sector 5 with the previous ship in the order. This is shown by an arrow between the ships with a tooltip when you hover your cursor over it.

[[/img/ship-creation-guide/unlock-arrow.png]]

These arrows can also be defined for your ships by adding the `arrow` tag as a child of the `ship` tag:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="true" b="false" c="false" secret="false">
        <arrow variant="a" tooltip="ship_unlock_arrow_tooltip" tooltipText="Tooltip text for hovering arrow with cursor" image="arrow_image.png" lockedImage="arrow_image_locked.png" unlockedImage="arrow_image_unlocked.png" direction="up/left/down/right" x="0" y="0" mirrorX="false" mirrorY="false">PLAYER_SHIP_NAME</arrow>
        <!-- Etc... -->
    </mod-append:ship>
    <!-- Etc... -->
</mod:findLike>
```
The value of the `arrow` tag determines what the target ship is. The arrow will be drawn going to the target ship from the ship that the `arrow` tag belongs to. In this example, the arrow would be drawn from `PLAYER_SHIP_CVX_TESTREL` to `PLAYER_SHIP_NAME`.

The attributes of the `arrow` tag function as follows:<br/>
`variant` - Value can be `a`, `b`, `c` or `all`. Determines which variant the arrow is drawn for. The source and target ship must be the same variant. If the value is set to `all` or the `variant` attribute is omitted, then the arrow appears on every page (but the target ship is always the specific variant).<br/>
`tooltip` - The ID of the text as defined in `text_misc.xml` to use for the hover tooltip. For defining text strings, see the [Misc Data Guide](Misc-Data-Guide#text-data).<br/>
`tooltipText` - Literal text to use for hover tooltip. Use instead of the `tooltip` attribute if you want to define the text directly instead of in `text_misc.xml`.<br/>
`image` - Full image name of the arrow asset. Arrow images must be in the `img\customizeUI` folder of your mod. Uses the default victory arrow asset in the corresponding direction if omitted.<br/>
`lockedImage` - Full image name of the arrow asset when source ship is locked. Uses the default locked arrow asset in the corresponding direction if omitted.<br/>
`unlockedImage` - Full image name of the arrow asset when the target ship is unlocked. No default, if unspecified then no arrow is rendered when the target ship is unlocked.<br/>
`direction` - Value can be `up`, `down`, `left` or `right`. Determines the direction which the arrow points, and is used to place the image relative to the button. Omit for default (0, 0) offset.<br/>
`x` and `y` - Offset coordinates for arrow after applying the automatic offset from the `direction` attribute.<br/>
`mirrorX` and `mirrorY` - Mirrors the arrow asset over the X and Y axes respectively.

## Combining Ship Mods

If you have multiple ship mods that you want to combine into a single patchable archive, first pick which one you want to move all the content to. We'll treat this as the primary mod. Move everything from the `img` folder of the secondary mod into the `img` folder of the primary one. Don't do the same for everything in the `data` folder, as that would override the data of one of the mods. In order to combine those files, you'll have to edit some of them directly. If you haven't already, I recommend reading the [XML Guide](XML-Guide) before continuing.

For both the `.xml` and `.txt` layout files, simply move all the ones from the secondary mod into the `data` folder of the primary. For the `blueprints.xml.append` file, open the one from the secondary mod in the editor of your choice. Copy the entirety of the `shipBlueprint`, then paste it into the `blueprints.xml.append` of the primary mod.

`hyperspace.xml.append` is a bit more involved, and the method you use to combine it will depend on whether you're adding a different variant for the same ship class or a different ship entirely.

For adding a different variant, suppose the `hyperspace.xml.append` of your primary mod looks like this:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="true" b="false" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_TESTREL">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
</mod:findLike>
```

And the `hyperspace.xml.append` of your secondary mod looks like this:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="false" b="true" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_TESTREL_2">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
</mod:findLike>
```

In order to combine them, you would modify your primary `hyperspace.xml.append` so that it looks like this:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="true" b="true" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_TESTREL">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
    <mod-append:customShip name="PLAYER_SHIP_CVX_TESTREL_2">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
</mod:findLike>
```

Note that the new `customShip` tag was copied in, but the new `ship` tag wasn't. Instead, since a B variant for the same ship class was added, we simply changed the value of the `ship` tag's `b` attribute from `false` to `true`.

Now suppose instead that you wanted to add an entirely new ship to the primary mod with a `hyperspace.xml.append` which looks like this:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_BESTREL" a="true" b="false" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_BESTREL">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
</mod:findLike>
```

In order to combine them, you would modify your primary `hyperspace.xml.append` so that it looks like this:

```xml
<mod:findLike type="ships" limit="1">
    <mod-append:ship name="PLAYER_SHIP_CVX_TESTREL" a="true" b="false" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_TESTREL">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
    <mod-append:ship name="PLAYER_SHIP_CVX_BESTREL" a="true" b="false" c="false" />
    <mod-append:customShip name="PLAYER_SHIP_CVX_BESTREL">
        <hiddenAug>SHIP_KESTREL</hiddenAug>
        <hiddenAug>FOR_MULTIVERSE</hiddenAug>
        <crewLimit>11</crewLimit>
    </mod-append:customShip>
</mod:findLike>
```

Note that both the `ship` tag and the `customShip` tag were copied in with no modifications.
