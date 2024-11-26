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

The `animSheet` defines the size of the image and the frames as well as the location. All animations are stored in a subfolder of `img`. This one is stored in `img/effects/explosion_big3.png`.

The `anim` defines how long the animation takes to complete a full cycle with the `time` child tag. The `length` attribute of the `desc` tag should be the number of frames in your animation, while the `x` and `y` attributes are unused for non-crew animations. the `sheet` tag should have the same value as the `name` attribute of your `animSheet` tag.

`animSheet` and `anim` tags usually have the same `name` attribute. The value of this attribute will be what you use to reference it in other files. For example, if you wanted a weapon blueprint to use this animation for the explosion when it hits a ship, you'd give its `explosion` tag the value `explosion_big3`.
