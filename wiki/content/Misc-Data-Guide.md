## Text Data

The purpose of defining FTL's text in files separate from where they're used is to allow for localization to other languages. The English texts are stored in several files:

- `text_achievements.xml`
- `text_blueprints.xml`
- `text_events.xml`
- `text_misc.xml`
- `text_sectorname.xml`
- `text_tooltips.xml`
- `text_tutorial.xml`

The file names describe which texts are contained in each file. For example, `text_blueprints.xml` contains all the texts used in `blueprints.xml`. `text_misc.xml` stores all texts which do not fit any of the other categories. All non-English texts are defined in the XML text file with the corresponding two-letter language code. For example, all the French text is stored in `text-fr.xml`.

To define a new text string in one of these files for a mod, first create a corresponding `append` file. If you want to add a text string to `text_misc.xml`, for example, you would create a file called `text_misc.xml.append`.

The format of a text string tag is as follows:

```xml
<text name="continue" language="fr">Continuer...</text>
```

The `name` attribute is used to retrieve it in other XML files. If you wanted to use this example as the text for an event choice, you'd do so with `<text id="continue"/>`. The `language` attribute is used only for non-English texts, and should be given a value that is the same two-letter language code as the file which contains it. The value of the `text` tag is the text string itself which will be displayed in-game.
