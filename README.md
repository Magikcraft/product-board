![Magikcraft Banner](readmeResources/logo.png)

# Magikcraft Release Notes

Magikcraft is the world's number 1 way to learn to code JavaScript in Minecraft.

Check out the [Magikcraft website](https://www.magikcraft.io) and the [Magikcraft YouTube channel](https://www.youtube.com/channel/UC9cEOcTkQEyiKr2nCZDBYeg/videos).

These release notes are updated with new releases. Star this repo to get notifications when it is updated. 

## Sunday 20 August

* Version 1.1.15 of the Magikcraft API

1. **magik.clearTimeout()**: `magik.clearTimeout()` now cancels a timeout task created with `magik.setTimeout()`. Prior to this release it did not cancel the task. For an example of `magik.setTimeout()` and `magik.clearTimeout()`, see [runTests.js](https://gist.github.com/jwulf/17c6151ee47c7972f3523d84f5f52e78#file-runtests-js).

## Saturday 19 August

* Version 1.0.2 of the [Spellbook App](https://play.magikcraft.io)
* Version 0.10.0 of the Magikcraft Endpoint

### In this release

1. **Gist View**: The 'Gist View' button in the [spellbook](https://play.magikcraft.io) now opens a new browser tab with your Magikcraft spells on GitHub. This allows you to easily copy a link to a specific spell to share with a friend.

![Gist View Button](readmeResources/Screen%20Shot%202017-08-19%20at%206.59.25%20pm.png)

2. **Use yarn**: We switched the Magikcraft server from `npm` to use `yarn` instead, to work around [https://github.com/npm/npm/issues/18178](https://github.com/npm/npm/issues/18178#issuecomment-323504516). Packages installed from GitHub repos now reliably update. 

### Known Issues

1. **/magikcraft command**: The `/magikcraft` command in Minecraft reports the version at the time that the server is started, even when the API has been updated during the server's lifetime.

## Thursday 17 August

* Version 1.1.18 of the Magikcraft API 
* Version 0.32 of the Server

To view the current versions of a Magikcraft server, use the command `/magikcraft`.

### In this release:

1. Internal changes to better support dynamic updating of the Magikcraft API. There is no user-visible impact at this time. We're working on a workaround for https://github.com/npm/npm/issues/18178 at the moment.

2. **Eventbus**: The global `eventbus` object, which allows pub/sub communication between JS Engines, is re-enabled. The eventbus can be used to make spells that share player locations (for example, to let you publish your location for others to teleport to you) or shared state like a game score. See the See the [README file for `magikcraft-lore-core`](https://github.com/Magikcraft/magikcraft-lore-core/blob/master/README.md#tojson-and-fromjson) for an example of the eventbus.

3. **JSON Marshalling methods**: `toJSON` and `fromJSON` methods added to the Magikcraft API. These methods marshall a BukkitLocation to and from JSON. See the [README file for the `magikcraft-lore-core`](https://github.com/Magikcraft/magikcraft-lore-core/blob/master/README.md#tojson-and-fromjson) for an example use of these methods.

## Saturday 12 August, 2017

### Enhancement

The [Magikcraft Bar package](http://github.com/magikcraft/magikcraft-lore-ui-bar) is now part of the Magikcraft organisation on GitHub. Create cool interface bars with ease using this package.

![UI Bar](https://media.giphy.com/media/xTkcEzfUCkrTC1q6li/giphy.gif)

## Tuesday 8 August, 2017

### Bugfix: Spell syncing stops working until the GraphQL server is rebooted

**Cause:** EventEmitters were limited on the GraphQL server pub-sub system.

**Consequence:** After a certain number of users connected, spell syncing would stop and you saving spells in the Play App had no effect in Minecraft.

**Fix:** The EventEmitter limit was raised to Infinity!

**Result:** Spell syncing should now work reliably. When you save a spell in the Play App, it should be available immediately in Minecraft for you to cast it.


