# [Flems.io](https://flems.io)
Flems is a playground for web development. It's ideal for prototyping ideas & sharing working front-end code examples.

Unlike other playgrounds, Flems doesn't require a connection to the server after page load: all the code you write in a Flems is computed in the browser and saved as a compressed string in the URL. The only thing you need a connection for is downloading extra dependencies. This means you can type away without needing to 'save' a Flems and the URL in the location bar will always be a shareable link to exactly what you're seeing.

Every Flems starts with an HTML, JS and CSS file, but you can add more files - Flems supports [TypeScript](http://typescriptlang.org), [LiveScript](http://livescript.net) and [Babel (standalone)](https://github.com/babel/babel/tree/master/packages/babel-standalone) compilation too. You can add CSS & JS dependencies by specifying a full URL pointing to the desired file, or by giving a reference to an NPM package (and optional path) - these will be taken from unpkg.com. You can change file execution for any given file or dependency of the same type by hovering over it in the sidebar and using the up & down arrows.

Flems.io is based on the Open Source [Flems module](https://github.com/porsager/flems) which you can use for easy self hosting or embedding.

## The Flems.io url hash

The current hash is of the format `"#0=" + LZString.compressToEncodedURIComponent(JSON.stringify(state))` where `LZString.compressToEncodedURIComponent` is from [`lz-string`](https://github.com/pieroxy/lz-string) and `state` is an object as per below:

- `state.files` - The array of user files, where each file an object `file` with the following properties:
	- `file.name` - The name of the file
	- `file.contents` - The contents of the file
	- `file.selections` - An optional comma-separated list of the following:
		- `L:C` - A single cursor
		- `L:C-L:C` - A full selection, where the first is the start and the second is the end of the selection.
		- Lines and columns are both 0-indexed.
- `state.links` - The array of external links, where each file an object `file` with the following properties:
	- `link.name` - The name of the link to display.
	- `link.url` - The resolved URL of the link in question.
	- `link.type` - The type of link, either `'style'` for stylesheets, `'script'` for scripts, or `'document'` for the main document.
	- `link.patches` - An optional array of patches to apply to the resulting source of that link.
	- `link.selections` - An optional comma-separated list of selections within that link. Follows the same format as `file.selections`.
