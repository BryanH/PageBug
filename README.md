# PageBug

Forked from [Auz/Bug][1].

Add bugs to your website's page.

## Features
* Creates multiple fruit flies which fly and walk around the browser window.
* Creates multiple spiders which walk around the browser window.
* Flies are responsive to mouse movements (optional) and mouseover events.


## Demo
See [original project page][3].


## Dependencies
None, all native js code


## Compatibility
Works on all browsers that support CSS3 transforms, even mobile (that I've tested).

See [browsers that support 2D Transforms][2].


### How to use
Include the JS somewhere, and then initialize with
```js
  new BugController();
```
or
```js
  new BugController({'minBugs':10, 'maxBugs':50, 'mouseOver':'die'});
```
You can use SpiderController() as a shortcut for loading options and the sprite for the spiders.

```js
  new SpiderController({'minBugs':2, 'maxBugs':6});
```

See [example.html][5] for sample usage.

BugController constructor can optionally take an object of options. To make this js more async friendly, you can adjust the default options at the top of bug.js, and then instantiate at the bottom of the file as above. This will allow one to wrap the entire script in a closure to prevent any global window name space overlaps.

#### Async code
```js
  var targethead = window.document.getElementsByTagName("head")[0],
    loadedSpiders = false,
    jst = window.document.createElement("script");
  jst.async = true;
  jst.type = "text/javascript";
  jst.src = "/path/to/bug-min.js";
  jst.onload = jst.onreadystatechange = function() {
    if (!loadedSpiders && (!this.readyState || this.readyState == 'complete')) {
      loadedSpiders = true;
      // start fire the JS.
      new BugController();
    }
  };
  targethead.appendChild(jst);
```

## Options
| Option| Description| Default|
| ----- | --- | :---:|
| `minDelay`| Minimum delay before a bug will appear on the page.| 500|
| `minDelay`| Minimum delay before a bug will appear on the page.| 500|
| `maxDelay`| Maximum delay before a bug will appear on the page.| 10000|
| `minBugs`| Minumum number of bugs to show.| 1|
| `maxBugs`| Maximum number of bugs to show.| 20|
| `minSpeed`| Minimum speed of a bug, in no particular units.| 1|
| `maxSpeed`| Maximum speed of a bug, in no particular units.| 3|
| `imageSprite`| Location of the fly sprite sheet.| 'fly-sprite.png'|
| `bugWidth`| The width of the fly sprite cell, and also div width.| 13|
| `bugHeight`| The height of the fly sprite cell, and also div height.| 14|
| `num_frames`| The number of frames in the sprite walk animation.| 5|
| `monitorMouseMovement`| If enabled, a mousemove event will be added to the window, and used to detect if the cursor is near a fly. Probably best to leave this one off.| false|
| `eventDistanceToBug`| If monitorMouseMovemenet is enabled, this is the distance from the bug in pixels which will trigger the near bug event.| 40|
| `minTimeBetweenMultiply`| When in 'multiply' mode, this is the minimum time in ms between a multiply event.| 1000|
| `mouseOver`| The insect's behavior when the mouse is over (or near) it. See **Modes** (below) for options.| random|
| `canFly`| Whether or not to allow fly modes, and to use wings open animation (second row of sprite).| true|
| `canDie`| Whether or not to allow the bug to 'die' - need bottom row of sprite with dead version.| true|
| `zoom`| Minimum amount to scale the bug, out of 10. So a zoom of 5 would randomly choose a zoom (css scale) value between 1/2 and 1 for each bug size.| 10 (no zooming)|
| `maxLargeTurnDeg`| When making a large turn, the maximum number of degrees to turn.| 150|
| `maxSmallTurnDeg`| When making a smaller turn, the maximum number of degrees to turn.| 10|
| `maxWiggleDeg`| When wiggling around the screen, this is the maximum number of degrees to turn.| 5|


## Modes
Action to take when mouse is over the insect.

* `random`: Randomly pick one of the other modes on each mouse over/near event
* `fly`: The bug will fly away to another random point on the page (if 'canFly' is true)
* `flyoff`: The bug will fly off the screen... and slowly work its way back (if 'canFly' is true)
* `multiply`: The bug will spawn a new bug and both will fly away to other parts of the page
* `nothing`: Do nothing
* `die`: The bug will be struck dead, and fall to the bottom of the page

## Credits
[Original Screen Bug on GoogleCode][4] (now defunct)

Released under WTFPL license.

[1]: https://github.com/Auz/Bug
[2]: http://caniuse.com/transforms2d
[3]: http://auz.github.io/Bug/
[4]: http://screen-bug.googlecode.com/git/index.html
[5]: blob/master/example.html