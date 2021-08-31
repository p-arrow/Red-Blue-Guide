**Common Restricted Shells**
- rbash
- rzsh
- lshell (Limited Shell)
- rssh (Restricted Secure Shell)

## How To

**Console Editors** (ed / ne / nano / pico / vim)
- :set shell=/bin/sh; shell
- :!/bin/sh
- !'/bin/sh'

**Pager Commands** (more / less)
- open a file long enough to invoke pager
- !'sh'
- v (vim editor)

**man and pinfo**
- invoke man page
- use more / less pager (start search "/" )

**Console Browsers** (links / lynx / elinks)
- open website (e.g. google.com)
- hit ESC, this will lead to configuration menu
- hit FILE > OS Shell

**find command**
- `find . -name [file] -exec awk 'BEGIN {system("cd /root; ls")}'`

**expect**
- `expect; spawn sh`
