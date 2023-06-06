# [Flems.io](https://flems.io)

Flems is a playground for web development. It's ideal for prototyping ideas & sharing working front-end code examples.

Unlike other playgrounds, Flems doesn't require a connection to the server after page load: all the code you write in a Flems is computed in the browser and saved as a compressed string in the URL. The only thing you need a connection for is downloading extra dependencies. This means you can type away without needing to 'save' a Flems and the URL in the location bar will always be a shareable link to exactly what you're seeing.

Every Flems starts with an HTML, JS and CSS file, but you can add more files - Flems supports [TypeScript](http://typescriptlang.org), [LiveScript](http://livescript.net) and [Babel (standalone)](https://github.com/babel/babel/tree/master/packages/babel-standalone) compilation too. You can add CSS & JS dependencies by specifying a full URL pointing to the desired file, or by giving a reference to an NPM package (and optional path) - these will be taken from unpkg.com. You can change file execution for any given file or dependency of the same type by hovering over it in the sidebar and using the up & down arrows.

Flems.io is based on the Open Source [Flems module](https://github.com/porsager/flems) which you can use for easy self hosting or embedding.

## The Flems.io URL hash

Flems.io stores the state of the application in a URL hash. The current hash is of the format:

```js
`#0=${LZString.compressToEncodedURIComponent(JSON.stringify(state))}`;
```

where `LZString.compressToEncodedURIComponent` is from [`lz-string`](https://github.com/pieroxy/lz-string) and `state` is an object as per below:

### state.files

The array of user files. Each file is an object with the following properties:

| property   | type   | required | default              | description                                                                                                                   |
| ---------- | ------ | -------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| name       | string | yes      | N/A                  | The name of the file                                                                                                          |
| content    | string | no       | `''`                 | The contents of the file                                                                                                      |
| type       | string | no       | Inferred from `name` | One of `'document'` (main HTML), `'script'` (JS and friends), or `'style'` (CSS and friends)                                  |
| compiler   | string | no       | N/A                  | Compiler to use for the file, one of `styl`, `sass`, `less`, `ts`, `babel`, `ls`, `coffee`, or `sibilant`                     |
| selections | string | no       | N/A                  | Comma-separated list of cursor (`L:C`) and selection (`L:C-L:C`) locations, where lines (`L`) and columns (`C`) are 0-indexed |

The format of `state.files` matches the [same option in the Flems module](https://github.com/porsager/flems#contents). If unspecified, the default value of `state.files` is:

```js
[
  { name: ".html", content: "" },
  { name: ".js", content: "" },
  { name: ".css", content: "" },
];
```

### state.links

The array of external links. Each link is an object with the following properties:

| property   | type     | required | default             | description                                                                                                                   |
| ---------- | -------- | -------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| url        | string   | yes      | N/A                 | URL of the linked file                                                                                                        |
| name       | string   | no       | Inferred from `url` | The name of the linked file                                                                                                   |
| type       | string   | no       | Inferred from `url` | One of `'document'` (main HTML), `'script'` (JS and friends), `'style'` (CSS and friends), or a supported file extension      |
| patches    | string[] | no       | N/A                 | An array of patches to apply to the resulting source of the link                                                              |
| selections | string   | no       | N/A                 | Comma-separated list of cursor (`L:C`) and selection (`L:C-L:C`) locations, where lines (`L`) and columns (`C`) are 0-indexed |

The format of `state.links` matches the same option [in the Flems module](https://github.com/porsager/flems#links). If unspecified, the default value of `state.links` is `[]`.

### Other options

The `state` object may also contain any of the [options available to the Flems module](https://github.com/porsager/flems#options). In addition, the following options are valid on Flems.io:

| property         | type    | required | default | description                                                                                        |
| ---------------- | ------- | -------- | ------- | -------------------------------------------------------------------------------------------------- |
| fullscreenButton | boolean | no       | `true`  | Show or hide the fullscreen button (Note: fullscreen functionality is currently disabled; see #25) |
