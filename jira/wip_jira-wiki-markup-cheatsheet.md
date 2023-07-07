# June 30, 2023 TIL - Jira Wiki Markup Cheatsheet

A Jira Wiki Markup helper cheatsheet.


## Headings

To create a header, place "hn. " at the start of the line (where n can be a number from 1-6).

| Notation               | Comment                   |
|------------------------|---------------------------|
| `h1. Biggest heading`  | `# Biggest heading`       |
| `h2. Bigger heading`   | `## Bigger heading`       |
| `h3. Big heading`      | `### Big heading`         |
| `h4. Normal heading`   | `#### Normal heading`     |
| `h5. Small heading`    | `##### Small heading`     |
| `h6. Smallest heading` | `###### Smallest heading` |


## Text Effects

Text effects are used to change the formatting of words and sentences.

| Notation        | Comment                  |
|-----------------|--------------------------|
| `*strong*`      | `**strong**`             |
| `_emphasis_`    | `_emphasis_`             |
| `??citation??`  | `-- citation`            |
| `-deleted-`     | `~~deleted~~`            |
| `+inserted+`    | `<ins>inserted</ins>`    |
| `^superscript^` | `<sup>superscript</sup>` |
| `~subscript~`   | `<sub>superscript</sub>` |


 | Makes text in <sub>subscript</sub>. |
| 

```
{{monospaced}}
```

 | Makes text as monospaced. |
| 

```
bq. Some block quoted text
```

 | 

To make an entire paragraph into a block quotation, place "bq. " before it.

Example:

> Some block quoted text

 |
| 

```
{quote}
    here is quotable content to be quoted
{quote}
```

 | 

Quote a block of text that's longer than one paragraph.

Example:

> here is quotable  
> content to be quoted

 |
| 

```
{color:red}
    look ma, red text!
{color}
```

 | 

Changes the color of a block of text.

Example:

look ma, red text!

 |

## Text Breaks

Most of the time, explicit paragraph breaks are not required - The wiki renderer will be able to paginate your paragraphs properly.

| Notation | Comment |
| --- | --- |
| 
```
(empty line)
```

 | Produces a new paragraph |
| 

```
\\
```

 | Creates a line break. Not often needed, most of the time the wiki renderer will guess new lines for you appropriately. |
| 

```
----
```

 | Creates a horizontal ruler. |
| 

```
---
```

 | Produces **—** symbol. |
| 

```
--
```

 | Produces **–** symbol. |

## Links

Learning how to create links quickly is important.

| Notation | Comment |
| --- | --- |
| 
```
[#anchor]
[^attachment.ext]
```

 | Creates an internal hyperlink to the specified anchor or attachment. Appending the '#' sign followed by an anchor name will lead into a specific bookmarked point of the desired page. Having the '^' followed by the name of an attachment will lead into a link to the attachment of the current issue. |
| 

```
[http://jira.atlassian.com]
[Atlassian|http://atlassian.com]
```

 | 

Creates a link to an external resource, special characters that come after the URL and are not part of it must be separated with a space.

The \[\] around external links are optional in the case you do not want to use any alias for the link.

Examples:

[http://jira.atlassian.com](http://jira.atlassian.com/)  
[Atlassian](http://atlassian.com/)

 |
| 

```
[mailto:legendaryservice@atlassian.com]
```

 | 

Creates a link to an email address, complete with mail icon.

Example:

![>>](https://jira.atlassian.com/images/icons/mail_small.gif)[legendaryservice@atlassian.com](https://jira.atlassian.com/secure/WikiRendererHelpAction.jspa?section=all#)

 |
| 

```
[file:///c:/temp/foo.txt]
[file:///z:/file/on/network/share.txt]
```

 | 

Creates a download link to a file on your computer or on a network share that you have mapped to a drive. To access the file, you must right click on the link and choose "Save Target As".

By default, this only works on Internet Explorer but can also be enabled in Firefox (see [docs](https://jira.atlassian.com/secure/$extLink)).

 |
| 

```
{anchor:anchorname}
```

 | Creates a bookmark anchor inside the page. You can then create links directly to that anchor. So the link \[My Page#here\] will link to wherever in "My Page" there is an {anchor:here} macro, and the link \[#there\] will link to wherever in the current page there is an {anchor:there} macro. |
| 

```
[~username]
```

 | Creates a link to the user profile page of a particular user, with a user icon and the user's full name. |

## Lists

Lists allow you to present information as a series of ordered items.

| Notation | Comment |
| --- | --- |
| 
```
* some
* bullet
** indented
** bullets
* points
```

 | 

A bulleted list (must be in first column). Use more (\*\*) for deeper indentations.

Example:

-   some
-   bullet
    -   indented
    -   bullets
-   points

 |
| 

```
- different
- bullet
- types
```

 | 

A list item (with -), several lines create a single list.

Example:

-   different
-   bullet
-   types

 |
| 

```
# a
# numbered
# list
```

 | 

A numbered list (must be in first column). Use more (##, ###) for deeper indentations.

Example:

1.  a
2.  numbered
3.  list

 |
| 

```
# a
# numbered
#* with
#* nested
#* bullet
# list
```

```
* a
* bulleted
*# with
*# nested
*# numbered
* list
```

 | 

You can even go with any kind of mixed nested lists

Example:

1.  a
2.  numbered
    -   with
    -   nested
    -   bullet
3.  list

Example:

-   a
-   bulleted
    1.  with
    2.  nested
    3.  numbered
-   list

 |

## Images

Images can be embedded into a wiki renderable field from attached files or remote sources.

| Notation | Comment |
| --- | --- |
| 
```
!http://www.host.com/image.gif!
or
!attached-image.gif!
```

 | 

Inserts an image into the page.

If a fully qualified URL is given the image will be displayed from the remote source, otherwise an attached image file is displayed.

 |
| 

```
!image.jpg|thumbnail!
```

 | 

Insert a thumbnail of the image into the page (only works with images that are attached to the page).

 |
| 

```
!image.gif|align=right, vspace=4!
```

 | 

For any image, you can also specify attributes of the image tag as a comma separated list of name=value pairs like so.

 |

## Attachments

Some attachments of a specific type can be embedded into a wiki renderable field from attached files.

| Notation | Comment |
| --- | --- |
| 
```
!quicktime.mov!
!spaceKey:pageTitle^attachment.mov!
!quicktime.mov|width=300,height=400!
!media.wmv|id=media!
```

 | 

Embeds an object in a page, taking in a comma-separated of properties.

Default supported formats:

-   Flash (.swf)
-   Quicktime movies (.mov)
-   Windows Media (.wma, .wmv)
-   Real Media (.rm, .ram)
-   MP3 files (.mp3)

Other types of files can be used, but may require the specification of the "classid", "codebase" and "pluginspage" properties in order to be recognised by web browsers.

Common properties are:

-   width - the width of the media file
-   height - the height of the media file
-   id - the ID assigned to the embedded object

Due to security issues, files located on remote servers are not permitted Styling  
By default, each embedded object is wrapped in a "div" tag. If you wish to style the div and its contents, override the "embeddedObject" CSS class. Specifying an ID as a property also allows you to style different embedded objects differently. CSS class names in the format "embeddedObject-ID" are used.

 |

## Tables

Tables allow you to organise content in a rows and columns, with a header row if required.

| Notation | Comment |
| --- | --- |
| 
```
||heading 1||heading 2||heading 3||
|col A1|col A2|col A3|
|col B1|col B2|col B3|
```

 | 

Makes a table. Use double bars for a table heading row.

The code given here produces a table that looks like:

| heading 1 | heading 2 | heading 3 |
| --- | --- | --- |
| col A1 | col A2 | col A3 |
| col B1 | col B2 | col B3 |

 |

## Advanced Formatting

More advanced text formatting.

| Notation | Comment |
| --- | --- |
| 
```
{noformat}
preformatted piece of text so *no* further _formatting_ is done here
{noformat}
```

 | 

Makes a preformatted block of text with no syntax highlighting. All the optional parameters of {panel} macro are valid for {noformat} too.

-   **nopanel:** Embraces a block of text within a fully customizable panel. The optional parameters you can define are the following ones:  
    

Example:

```
preformatted piece of text so *no* further _formatting_ is done here
```



 |
| 

```
{panel}
Some text
{panel}
```

```
{panel:title=My Title}
Some text with a title
{panel}
```

```
{panel:title=My Title|borderStyle=dashed|borderColor=#ccc|titleBGColor=#F7D6C1|bgColor=#FFFFCE}
a block of text surrounded with a *panel*
yet _another_ line
{panel}
```

 | 

Embraces a block of text within a fully customizable panel. The optional parameters you can define are the following ones:  

-   **title:** Title of the panel
-   **borderStyle:** The style of the border this panel uses (solid, dashed and other valid CSS border styles)
-   **borderColor:** The color of the border this panel uses
-   **borderWidth:** The width of the border this panel uses
-   **bgColor:** The background color of this panel
-   **titleBGColor:** The background color of the title section of this panel

Example:

**My Title**

a block of text surrounded with a **panel**  
yet _another_ line



 |
| 

```
{code:title=Bar.java|borderStyle=solid}
// Some comments here
public String getFoo()
{
    return foo;
}
{code}
```

```
{code:xml}
    <test>
        <another tag="attribute"/>
    </test>
{code}
```

 | 

Makes a preformatted block of code with syntax highlighting. All the optional parameters of {panel} macro are valid for {code} too. The default language is **Java** but you can specify others too, including **ActionScript**, **Ada**, **AppleScript**, **bash**, **C**, **C#**, **C++**, **CSS**, **Erlang**, **Go**, **Groovy**, **Haskell**, **HTML**, **JavaScript**, **JSON**, **Lua**, **Nyan**, **Objc**, **Perl**, **PHP**, **Python**, **R**, **Ruby**, **Scala**, **SQL**, **Swift**, **VisualBasic**, **XML** and **YAML**.

Example:

```
public String getFoo()
{
    return foo;
}

```

```
<test>
    <another tag="attribute"/>
</test>

```



 |

## Misc

Various other syntax highlighting capabilities.

| Notation | Comment |
| --- | --- |
| 
```
\X
```

 | Escape special character X (i.e. {) |
| 

```
:)
```

,

```
:(
```

etc | 

Graphical emoticons (smileys).

<table><tbody><tr><th>Notation</th><td>:)</td><td>:(</td><td>:P</td><td>:D</td><td>;)</td><td>(y)</td><td>(n)</td><td>(i)</td><td>(/)</td><td>(x)</td><td>(!)</td></tr><tr><th>Image</th><td><img src="https://jira.atlassian.com/images/icons/emoticons/smile.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/sad.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/tongue.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/biggrin.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/wink.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/thumbs_up.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/thumbs_down.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/information.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/check.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/error.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/warning.gif"></td></tr></tbody></table>

<table><tbody><tr><th>Notation</th><td>(+)</td><td>(-)</td><td>(?)</td><td>(on)</td><td>(off)</td><td>(*)</td><td>(*r)</td><td>(*g)</td><td>(*b)</td><td>(*y)</td><td>(flag)</td></tr><tr><th>Image</th><td><img src="https://jira.atlassian.com/images/icons/emoticons/add.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/forbidden.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/help_16.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/lightbulb_on.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/lightbulb.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/star_yellow.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/star_red.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/star_green.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/star_blue.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/star_yellow.gif"></td><td><img src="https://jira.atlassian.com/images/icons/emoticons/flag.gif"></td></tr></tbody></table>

<table><tbody><tr><th>Notation</th><td>(flagoff)</td></tr><tr><th>Image</th><td><img src="https://jira.atlassian.com/images/icons/emoticons/flag_grey.gif"></td></tr></tbody></table>

 |


## Use Cases

- Cheatsheet/Reference for Jira/Confluence Wiki Markup to Markdown

## References

- [Jira/Confluence Wiki Markup Cheatsheet - Text Formatting Notation Help](https://jira.atlassian.com/secure/WikiRendererHelpAction.jspa?section=all)

