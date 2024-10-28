The core of FTL modding is XML, which stands for Extensible Markup Language. A programming language has data as well as logic, whereas a markup language only has data, making it much more accessible. In other words, you don't need a degree in computer science to mod FTL.

XML is made up of tags, attributes and values. Every tag can have any number of attributes and any number of children. A tag can also contain a value instead of children.

```xml
<parent-tag>
    <tag1>Pew!</tag1>
    <tag2 attribute1="Boom!" attribute2="Pow!"/>
    <tag3/>
</parent-tag>
```

In this example, `parent-tag` has three children, `tag1`, `tag2` and `tag3`. `tag1` has the value `Pew!`. `tag2` has two attributes, the first with the value `Boom!` and the second with the value `Pow!`. `tag3` has no attributes, value or children.

Note that tags with children or a value are closed differently than tags without them. `parent-tag` and `tag1` are closed by a copy of the opening tag with a forward slash added before the tag name. `tag2` and `tag3` are closed by adding a forward slash to the end of the tag, after the name and attributes.
