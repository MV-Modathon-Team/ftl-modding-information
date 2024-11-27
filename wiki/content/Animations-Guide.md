## Standard Animations

With the exception of crew sprites, every animation in FTL is a horizontal strip of frames, each with the same dimensions, saved as a png image. Take this vanilla explosion animation for example:

[[/img/animations-guide/explosion_big3.png]]

Each frame is 64x64 pixels. Since there are 10 frames, the total width of the image is 704 pixels. Defining a standard animation takes two tags, the `animSheet` and the `anim`:

```xml
<animSheet name="explosion_big3" w="704" h="64" fw="64" fh="64">effects/explosion_big3.png</animSheet>
<anim name="explosion_big3">
    <sheet>explosion_big3</sheet>
    <desc length="11" x="0" y="0"/>
    <time>0.75</time>
</anim>
```

The `animSheet` defines the size of the image with the `w` and `h` attributes and the size of the frames with the `fw` and `fh` attributes. The value of the tag defines the location and filename. All animations are stored in a subfolder of `img`. This one is stored in `img/effects/explosion_big3.png`.

The `anim` defines how long the animation takes to complete a full cycle with the `time` child tag. The `length` attribute of the `desc` tag should be the number of frames in your animation, while the `x` and `y` attributes are unused for non-crew animations. the `sheet` tag should have the same value as the `name` attribute of your `animSheet` tag.

`animSheet` and `anim` tags usually have the same `name` attribute. The value of this attribute will be what you use to reference it in other files. For example, if you wanted a weapon blueprint to use this animation for the explosion when it hits a ship, you'd give its `explosion` tag the value `explosion_big3`.

## Weapon Animations

Weapon animations are more sophisticated. Take for example the Chain Ion animation:

[[/img/animations-guide/ion_chain.png]]

```xml
<animSheet name="ion_chaingun" w="280" h="58" fw="35" fh="58">weapons/ion_chain.png</animSheet>
<weaponAnim name="ion_chaingun">
    <sheet>ion_chaingun</sheet>
    <desc length="8" x="0" y="0"/>
    <chargedFrame>1</chargedFrame>
    <fireFrame>5</fireFrame>
    <firePoint  x="17" y="17"/>
    <mountPoint x="5" y="45"/>
    <!-- <delayChargeAnim>0.98</delayChargeAnim> -->
    <chargeImage>weapons/ion_chain_glow.png</chargeImage>
    <boost>ion_chaingun_charge</boost>
</weaponAnim>
```

The `animSheet` tag works the same as for standard animations. Instead of an `anim` tag, weapons use the `weaponAnim` tag. The `sheet` and `desc` child tags work the same as for the standard `anim` tag. The other tags work as follows:<br/>
`chargedFrame` - Which frame is displayed when the weapon is fully charged. Frames are counted from left to right starting at 0, so the value of 1 will display the second frame when the weapon is charged. While the weapon is charging, the weapon will display all the frames leading up to the `chargedFrame`. The minimum value of `chargedFrame` is 1, the first frame (frame 0) must be the one displayed while the weapon is at 0 charge.<br/>
`fireFrame` - Which frame the weapon fires it's projectile during. For this weapon, when fired, it will play every frame from the third (frame 2, the one frame after the `chargedFrame` of 1) to the sixth (frame 5), firing on the sixth, then playing the remaining frames before resetting to the first. The minimum value of `fireFrame` is 2.<br/>
`firePoint` - The location on the weapon sprite the projectile is created at when it fires.<br/>
`mountPoint` - The location on the weapon sprite that is anchored to the mount point on the ship.

[[/img/animations-guide/weapon-anim-coord-ref.png]]

`delayChargeAnim` (optional)  The percentage the weapon must be charged before displaying frames beyond the first. This is used by vanilla bomb weapon animations to prevent the animation of the bomb coming out of the launcher from playing until it's nearly charged. Value can be between 0 and 1.<br/>
`chargeImage` (optional) - The location of the charge image, which if defined, will gradually increase in opacity as the weapon charges. For example, the charge image used for the Chain Ion:

[[/img/animations-guide/ion_chain_glow.png]]

`boost` (optional) - The animation to use for the boost indicator glow if your weapon blueprint has a `boost` tag. For example, the boost animation used for the Chain Ion:

```xml
<animSheet name="ion_chaingun_charge" w="105" h="58" fw="35" fh="58">weapons/ion_chain_chargeglow.png</animSheet>
<anim name="ion_chaingun_charge">
    <sheet>ion_chaingun_charge</sheet>
    <desc length="3" x="0" y="0"/>
    <time>1.0</time>
</anim>
```

[[/img/animations-guide/ion_chain_chargeglow.png]]

The first frame of this animation is displayed on top of the weapon animation after the weapon has fired once, the second is displayed after the weapon has fired twice, etcetera.
