                           ████████╗███████╗██████╗ ███╗   ███╗        ██╗███████╗
                           ╚══██╔══╝██╔════╝██╔══██╗████╗ ████║        ██║██╔════╝
                              ██║   █████╗  ██████╔╝██╔████╔██║        ██║███████╗
                              ██║   ██╔══╝  ██╔══██╗██║╚██╔╝██║   ██   ██║╚════██║
                              ██║   ███████╗██║  ██║██║ ╚═╝ ██║██╗╚█████╔╝███████║
                              ╚═╝   ╚══════╝╚═╝  ╚═╝╚═╝     ╚═╝╚═╝ ╚════╝ ╚══════╝
<br>
<p align="center">
  <a href="https://github.com/bus-stop/term.js/tags">
    <img src="https://img.shields.io/github/tag/bus-stop/term.js.svg?label=version&style=for-the-badge" alt="version">
  </a>
  <a href="https://github.com/bus-stop/term.js/stargazers">
    <img src="https://img.shields.io/github/stars/bus-stop/term.js.svg?&style=for-the-badge" alt="stars">
  </a>
  <a href="https://github.com/bus-stop/term.js/network">
    <img src="https://img.shields.io/github/forks/bus-stop/term.js.svg?style=for-the-badge" alt="forks">
  </a>
  <a href="https://david-dm.org/bus-stop/term.js?type=dev">
    <img src="https://img.shields.io/david/dev/bus-stop/term.js.svg?label=devDependencies&style=for-the-badge" alt="devDependencies">
  </a>
</p>
<h3 align="center">A terminal written in javascript.&nbsp;❤️</h3>
<h5 align="center">A fork of <a href="https://github.com/chjj/term.js">chjj/term.js<a/></h5>
<h6 align="center">Used by <a href="https://github.com/chjj/term.js">tty.js<a/></h6>
<br>

## Example

Server:

```js
var term = require('term.js');
app.use(term.middleware());
...
```

Client:

```js
window.addEventListener('load', function() {
  var socket = io.connect();
  socket.on('connect', function() {
    var term = new Terminal({
      cols: 80,
      rows: 24,
      screenKeys: true
    });

    term.on('data', function(data) {
      socket.emit('data', data);
    });

    term.on('title', function(title) {
      document.title = title;
    });

    term.open(document.body);

    term.write('\x1b[31mWelcome to term.js!\x1b[m\r\n');

    socket.on('data', function(data) {
      term.write(data);
    });

    socket.on('disconnect', function() {
      term.destroy();
    });
  });
}, false);
```

## Tmux-like

While term.js has always supported copy/paste using the mouse, it now also
supports several keyboard based solutions for copy/paste.

term.js includes a tmux-like selection mode (enabled with the `screenKeys`
option) which makes copy and paste very simple. `Ctrl-A` enters `prefix` mode,
from here you can type `Ctrl-V` to paste. Press `[` in prefix mode to enter
selection mode. To select text press `v` (or `space`) to enter visual mode, use
`hjkl` to navigate and create a selection, and press `Ctrl-C` to copy.

`Ctrl-C` (in visual mode) and `Ctrl-V` (in prefix mode) should work in any OS
for copy and paste. `y` (in visual mode) will work for copying only on X11
systems. It will copy to the primary selection.

>Note: `Ctrl-C` will also work in prefix mode for the regular OS/browser
selection. If you want to select text with your mouse and copy it to the
clipboard, simply select the text and type `Ctrl-A + Ctrl-C`, and
`Ctrl-A + Ctrl-V` to paste it.

For macOS users: consider `Ctrl` to be `Command/Apple` above.

## Contribution and License Agreement

If you contribute code to this project, you are implicitly allowing your code
to be distributed under the MIT license. You are also implicitly verifying that
all code is your original work. `</legalese>`

## License

[![MIT](https://img.shields.io/badge/License-MIT-blue.svg?longCache=true&style=for-the-badge)](LICENSE)
