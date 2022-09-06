# autoclip

Automatically react to clipboard contents

## What

`autoclip` watches your clipboard for changes, and when it detects
new clipped content, will attempt to call any number of custom response
hooks

## How

#### On Linux
Awaits clipboard content changes via `xclip` and fires response hooks upon
receiving a change event.

#### On MacOS
Loops constantly over the output of `pbpaste` looking for changes to clipped
content every second and fires response hooks upon seeing changes.

## Hooks

Hooks are files that perform an action given clipboard content as an input.

Each hook will be called with a single input, which is the clipboard content
provided as a string.

A hook must be an executable file and can be a script or a program written in
any language, and must all live in the hook directory and end with `.hook` as
the file extension.

Hooks are called in a non-guaranteed order.

If execution of a hook returns `0`, it will be considered a "terminating" event
and no further hooks will be processed. Any other non-zero return code is not
"terminating", so futher hooks will continue to be called.

It is up to each individual hook to:

1. Receive input from the command line execution environment
2. Decide if the given input is relevant to the hook, otherwise exit
3. If relevant and processed, decide if this hook is terminating or not

### Example

Copy the `res/example-hooks/01-open-youtube-urls.hook` into your hook configuration directory.
This hook will open your browser to a YouTube video any time it detects a YouTube URL inside of
the clipboard contents.

## License
GPL 2.0
```
  Copyright (C) 2022 Peter Yamanaka

  This program is free software; you can redistribute it and/or modify
  it under the terms of the GNU General Public License as published by
  the Free Software Foundation; either version 2 of the License, or
  (at your option) any later version.

  This program is distributed in the hope that it will be useful,
  but WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  GNU General Public License for more details.
  You should have received a copy of the GNU General Public License
  along with this program; if not, write to the Free Software
  Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
```
