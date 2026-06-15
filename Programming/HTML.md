# Text

- The website should contain only one h1
- <font attributes=””>text</font>: size, color(name&hex) and face(font)
- To get all spaces and break lines <pre>h t m l</pre>, but it is not preferable
- <b> </b> → bold
- <i> </i> → italic
- <u> </u>→ underline
- <br/>(no close), this only → break line
- <hr/> (no close), this only → horizontal separator
- &nbsp (nonbreakablespace) → space *breakable ely heya lama tool el satr yekhlas*
- &lt - &gt→ less/greater than
- <center></center> → center text
- <div attributes=””></div>(Block element) →**accept alignment,** attributes: align
- <p></p>(Block element) →**accept alignment,** attributes: align
- <span></span> (Inline element)→ in line text display, **do not accept alignment**

---

# Lists

Got 3 types:

#### unordered

<ul></ul> and members in between in list item <li>

- <li attributes=””></li> → attributes : type: circle …etc
    - Can have nested just like the ones im using in notion

---

#### ordered

<or></or> and members in between in list item <li>

- <li attributes=””></li> → attributes : type … a/A/i/I(roman) - start 2,3 same if roman not ii

---

#### definition

<dl></dl> Have title and definitions

<dt></dt> → definition title
<dd></dd> → definition, displayed under its title

---

# Linking

Got 3 types:

#### To File

#### External File (URL)

`<a href=”https://xyz.com”> Click here </a>`

#### Internal File (Path)

Whether by:

- Absolute path **USING “”**
    - starting from drive going through each folder. even if both pages was in the same →  `href = “drive/folder/folder/file.html”`
- Relative path **NO USE OF “”**
    - If in same exact folder → `href = file.html`
    - If in a folder in the same folder → `href=folder/file.html`

Notes: 

1. `../` → to go to the mother folder`../../`is x2
2. `./` → means in the same folder and can be a mix of absolute *(using”)* and relative *(not full path)* by doing this `href=”./file.html”`

---

#### To Anchor

#### To a section on the same page

`<a href=”#sectionname”> Click here </a>
…<!--code-->…
<a name=”sectionname”>...<!--code-->...</a>`

#### To a section on Different page

Page 1

`<a href=”<Pathofpage2>/file.html#sectionname”> Click here </a>`

Page 2

`<a name=”sectionname”>...<!--code-->...</a`

---

#### to email

`<a href=”mailto:email"> Click here to contact </a>`

- Can add some attributes by adding `..?..`then the attribute
`<a href=”mailto:email?subject=xyz"> Click here to contact </a>` 
attributes like subject : CC, BCC, Body
    - **`BCC/CC`**→ `<a href="mailto:test@email.com?bcc=secret@email.com>`
    - **`BCC+CC`** *using (&)* → `<a [href="mailto:test@email.com](mailto:href=%22mailto:test@email.com)?cc=copied@email.com**&**bcc=secret@email.com">`
    - **`&`** → Combines multiple fields together
    - `body..%20..body..%0A..body..` → `%20`Translates to space, `%0A` Translates to line break. Both work whatever the attribute
    - `<a href="mailto:?subject=Spontaneous%20Message">` → Blank recipient (removes the assigned mail and let the user input it manually)
    - `<a [href="mailto:one@email.com](mailto:href=%22mailto:one@email.com)[,two@email.com](mailto:,two@email.com)">` →  ( `,` )Sends to multiple primary recipients at once

---

---

---

---

---

---

---

---

# Notes

1. The `color` attribute can be used in `<link>`, `<font>`, and `<hr>` tags, but ***not*** in `<p>`, `<div>`, `<span>`, or `<body>` tags.