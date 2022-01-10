# Archy

~~Heir~~Archy is a Confluence-esque hierarchical, web-based, rich, markdown-enabled note taking application themed around Windows 98.

I was annoyed that note taking apps: don't allow for infinitely nested navigation trees, beam data to questionable third parties, don't allow for inline image pasting, are closed source, are expensive, are native apps, are not accessible from anywhere, or aren't extensible, so I made Archy.

### Running

Create a Firebase app with auth, Firestore and a bucket, plop the API keys in `firebase.initializeApp`, host `index.html` & `main.css` and she's good to go!

### Features

- UI
	- Title bar
		- Page title
		- Page ID
		- Page creation date
		- Page modified date
		- Press the maximize button to find all `???` occurrences
	- Tree view
	- Page editor
	- Rendered page
- Tree view
	- Creation of child pages
	- Renaming of pages (`F2`)
	- Folding parents (`double click`)
	- Reordering of pages (`-` and `+`)
	- Restructuring of page (pick up and put down a page / group with <code>`</code>)
	- Deleting pages (`DEL` key)
	- Page ID on hover
- Editor
	- Markdown compliant
	- Indent text by selecting and pressing `TAB`
	- Convert selection to numbered list `CTRL + SHIFT + 7`
	- Convert selection to unordered list `CTRL + SHIFT + 8`
	- Switch to / from editor with `SHIFT + TAB`
	- Auto inserting closing tags: <code>~~</code> <code>``</code> <code>**</code> <code>()</code> <code>{}</code> <code>[]</code> <code>""</code>
	- Paste images inline
	- Link to other pages `[page](#7)`
	- Code syntax highlighting
		- Optional explicit language instruction e.g <code>```python</code>
- Database
	- Fold states
	- Last open page
	- Tree state
	- Documents (Base64)
- Image storage bucket
- Authentication - accessible by only authorised users
- TODO
	- Unify parent / child node syntax / logic
	- Verbose setup guide including adding auth controls to the FS bucket
	- Page sharing / exporting to PDF
	- On long pages, sync editor and render scroll heights
	- Nicer login UI
	- Fix font CORS errors
	- Clean CSS

### Architecture

An empty in-memory JSON object is filled with `metadata` (e.g last open page), `tree` state and all `documents`. Image data is downloaded as necessary on a page by page basis.

When a change is made to any of the above, it is written to the local DB, the remote DB (Google Firebase) and the DOM if necessary.

Written in HTML5. Uses `marked.js` for Markdown > HTML conversion. Uses `highlight.js` for code formatting. Uses `98.css` for styling. Uses Firebase SDKs for authentication, databases and image buckets.

Tree nodes have three actions. `onclick` instructs Archy to change page, save the prior page and update the `lastOpen` field in the DB. `oncontextmenu` triggers a new page to be created. `ondblclick` folds it.

### Screenshots

#### Rendered View

![image](https://user-images.githubusercontent.com/17722100/148754926-7748ac46-387c-46d8-b7b8-09bbf918f86e.png)

#### Editor View

![image](https://user-images.githubusercontent.com/17722100/148754974-26431cbd-8081-4061-91de-e4f5e8bede00.png)
