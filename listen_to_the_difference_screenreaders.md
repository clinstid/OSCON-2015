# Listen to the Difference: Screenreaders
Slides: http://incl.ca/archives

# Popular Screenreaders
- JAWS - Windows
- NVDA - Windows
- VoiceOver Mac, iOS
- ORCA for Linux, https://wiki.gnome.org/Projects/Orca

# Users
- Vision impairments
- Cognitive impairments
- Developers

# NVDA
NonVisual Desktop Access
http://nvaccess.org

# Bad alternate text
- No alternate text for images - NVDA ends up saying "blank", not helpful
- Default of file name for alternate text probably won't help either
- http://www.w3.org/WAI/tutorials/images/decision-tree/

# Bad data tables
Tables need context because it will get complicated as the reader moves through the rows and columns.
- Use actual tables - Use column & row headers
    - For rows, use `<th scope="row">Row name</th>`
- Associate cells with relevant headers
- Use a `<caption>`

The main point is to try to make sure the reader actually gives context for each cell so the listener can easily remember where they are in the table.

# Forms
- Label controls - `<label for="input-id">`
- Group related controls with a `<fieldset>`
- Use a `<button>` or `<input type="submit">`
- Clearly identify required fields - Use `required` instead of a symbol
- Avoid time limits on form submit or at least warn or provide a way to turn it off

# Headings
- Use the actual `<hN>` elements for logical headings, don't just use them for style.
- For logical sections, actually use `<hN>` elements for headings, don't just use the same style.

# Bad Dropdown Menu
- Don't use hover to show the menu!
- Don't use pseudo buttons that can't be focused
- Keep menus simple
- For showing menus, use both `a:focus` and `a:hover`
- Test with the keyboard, make sure you can get everywhere you need to with it
