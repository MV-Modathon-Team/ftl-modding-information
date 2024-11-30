## Understanding XML

The core of FTL modding is XML, which stands for Extensible Markup Language. A programming language has data as well as logic, whereas a markup language only has data, making it much more accessible. In other words, you don't need a degree in computer science to mod FTL.

XML is made up of tags, attributes and values. Every tag can have any number of attributes and any number of children. A tag can also contain a value instead of children.

```xml
<parent-tag>
    <tag1>Pew!</tag1>
    <tag2 attribute1="Boom!" attribute2="Pow!"/>
    <tag3/>
</parent-tag>
```

In this example, `parent-tag` has three children, `tag1`, `tag2` and `tag3`. `tag1` has the value `Pew!`. `tag2` has no value and two attributes, the first with the value `Boom!` and the second with the value `Pow!`. `tag3` has no attributes, value or children.

Note that tags with children or a value are closed differently than tags without them. `parent-tag` and `tag1` are closed by a copy of the opening tag with a forward slash added before the tag name. `tag2` and `tag3` are closed by adding a forward slash to the end of the tag, after the name and attributes.

You can also add comments to your XML by using `<!--` to open them and `-->` to close them. They can take up one or multiple lines. Comments are not read by the game, and are used only to make notes in the XML for future reference. For example, if you wanted to mark a section of your XML file that defines all your weapons, you might write something like this:

```xml
<!--=============
==== WEAPONS ====
==============-->
```

If you want to make a note for a particular tag, you might write something like this:

```xml
<parent-tag>
    <tag1>Pew!</tag1> <!-- That sound it make when you shoot -->
    <tag2 attribute1="Boom!" attribute2="Pow!"/> <!-- Dead -->
    <tag3/> <!-- No sound :( -->
</parent-tag>
```

## Using XML

The plan is to eventually have a guide on this wiki for every application for XML in FTL modding. For now, you can use [Kix's old modding guide](<https://docs.google.com/document/d/1MZ-LbQdQ9qG2eNDbAVk6rfabbKJi4_fAV-ARA6IHw2M>).
