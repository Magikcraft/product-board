![Magikcraft Banner](readmeResources/logo.png)

# Magikcraft Release Notes

## Tuesday 8 August, 2017

### Bugfix: Spell syncing stops working until the GraphQL server is rebooted

**Cause:** EventEmitters were limited on the GraphQL server pub-sub system.

**Consequence:** After a certain number of users connected, spell syncing would stop and you saving spells in the Play App had no effect in Minecraft.

**Fix:** The EventEmitter limit was raised to Infinity!

**Result:** Spell syncing should now work reliably. When you save a spell in the Play App, it should be available immediately in Minecraft for you to cast it.

## Saturday 12 August, 2017

### Enhancement

The [Magikcraft Bar package](http://github.com/magikcraft/magikcraft-lore-ui-bar) is now part of the Magikcraft organisation on GitHub. Create cool interface bars with ease using this package.

![UI Bar](https://media.giphy.com/media/xTkcEzfUCkrTC1q6li/giphy.gif)

## Thursday 17 August

* Version 1.1.18 of the Magikcraft API 
* Version 0.32 of the Server

To view the current versions of a Magikcraft server, use the command `/magikcraft`.

### In this release:

1. Internal changes to better support dynamic updating of the Magikcraft API. There is no user-visible impact at this time. We're working on a workaround for https://github.com/npm/npm/issues/18178 at the moment.

2. The global `eventbus` object, which allows pub/sub communication between JS Engines, is re-enabled. The eventbus can be used to make spells that share player locations (for example, to let you publish your location for others to teleport to you) or shared state like a game score.

Here is an example using it:

`pubtest.js`
```
const magik = magikcraft.io;
const topic = 'sitapati.msg';

function pubtest() {
    eventbus.publish(topic, 'Hello from the eventbus');
    eventbus.publish(topic, {ok: true});
}
```

`subtest.js`
```
const magik = magikcraft.io;
const topic = 'sitapati.msg';

function subtest() {
    const say = magik.dixit;
    if (global.sub) {
        //say(global.sub.toString());
        // unsubscribe is currently broken
        //say('Cancelling existing subscription');
        // global.sub.unsubscribe();
        return;
    }
    say('Subscribing ')
    global.sub = eventbus.subscribe(
        topic, 
        data => magik.dixit(data.data.toString())
    );
}
```
