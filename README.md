# [Flems.io](https://flems.io)
Flems is a playground for web development. It's ideal for prototyping ideas & sharing working front-end code examples.

Unlike other playgrounds, Flems doesn't require a connection to the server after page load: all the code you write in a Flems is computed in the browser and saved as a compressed string in the URL. The only thing you need a connection for is downloading extra dependencies. This means you can type away without needing to 'save' a Flems and the URL in the location bar will always be a shareable link to exactly what you're seeing.

Every Flems starts with an HTML, JS and CSS file, but you can add more files - Flems supports [TypeScript](http://typescriptlang.org), [LiveScript](http://livescript.net) and [Babel (standalone)](https://github.com/babel/babel/tree/master/packages/babel-standalone) compilation too. You can add CSS & JS dependencies by specifying a full URL pointing to the desired file, or by giving a reference to an NPM package (and optional path) - these will be taken from unpkg.com. You can change file execution for any given file or dependency of the same type by hovering over it in the sidebar and using the up & down arrows.

Flems.io is based on the Open Source [Flems module](https://github.com/porsager/flems) which you can use for easy self hosting or embedding.
