# Atadev

A simple script to enable `@`:ing other devs in code.

Use it as a post-merge hook and it will check new files for any mentions and alert the user.

Use it as a command line tool and it will show you all your messages.

## Installation

If you’re not using a post-merge hook at the moment, the easiest way is probably to symlink `post-merge` to this script.

```bash
cd my-project/.git/hooks
ln -s ~/path/to/atadev post-merge
```

For JavaScript projects you can use [husky](https://github.com/typicode/husky). Copy this script to your project’s scripts folder, and add something like this to `package.json`:

```json
  "husky": {
    "hooks": {
      "post-merge": "bin/atadev hook"
    }
  }
```

## Usage example

The office nitpicker commits and pushes the following in `src/index.js`:

```javascript
var myConst = { // @John Please use const and not var
  a: 1,
  b: 2 // @Bella Please add a trailing comma here, see our style guide
}
// @John and @Bella You should both enable an ESLint plugin in your $EDITOR
```

When John runs `git pull`, he sees the following message:

```text
Mentions in ./src/index.js
==========================
On line 5:
  var myConst = { // @John Please use const and not var
On line 9:
  // @John and @Bella You should both enable an ESLint plugin in your $EDITOR
```

When Bella runs `git pull`, she sees the following message:

```text
Mentions in ./src/index.js
==========================
On line 7:
  b: 2 // @Bella Please add a trailing comma here, see our style guide
On line 9:
  // @John and @Bella You should both enable an ESLint plugin in your $EDITOR
```

Bella and John makes their respective changes and remove the relevant message.

Perhaps one of them adds a new message:

```javascript
const myConst = {
  a: 1,
  b: 2,
}
// @John and @Bella You should both enable an ESLint plugin in your $EDITOR
// Hey, @OfficeNitpicker, it’s better to @ one dev per line, see our style guide
```

## Todo

- [x] Test as githook (separate branch?)
- [x] Use git blame to show sender
- [x] Test if the githook works with newly added files
- [ ] Escape strings in output
- [x] Figure out a way to set behaviour depending on usage
- [x] Improve documentation
- [ ] Editor plugins!
