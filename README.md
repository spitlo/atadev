# Atadev

A simple script to enable `@`:ing other devs in code.

Use it as a post-merge hook and it will check new files for any mentions and alert the user.

Usage example:

The office nitpicker commits and pushes the following in `src/index.js`:

```javascript
const myConst = { // @John Please use const and not var
  a: 1,
  b: 2, // @Bella I added a trailing comma here, see our style guide
}
// @John and @Bella You should both enable an ESLint plugin in your $EDITOR
```

When John runs `git pull`, he sees the following message:

```text
Mentions in ./src/index.js
==========================
On line 5:
  const myConst = { // @John Please use const and not var
On line 9:
  // @John and @Bella You should both enable an ESLint plugin in your $EDITOR
```

When Bella runs `git pull`, she sees the following message:

```text
Mentions in ./src/index.js
==========================
On line 7:
  b: 2, // @Bella I added a trailing comma here, see our style guide
On line 9:
  // @John and @Bella You should both enable an ESLint plugin in your $EDITOR
```

## Todo

- [x] Test as githook (separate branch?)
- [ ] Use git blame to show sender
- [ ] Escape strings in output
- [ ] Figure out a way to set behaviour depending on usage
- [ ] Improve documentation
