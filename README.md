# FConsole
Bunch* of useful debug tools for speeding up development process of [Pixi.js](https://github.com/pixijs/pixi.js)** based applications. Written in [TypeScript](https://github.com/Microsoft/TypeScript).

*Inspired by [Flash-Console](https://github.com/junkbyte/flash-console).*

> Use with Google Chrome for better experience and debug functionality.

# Demo
### **[Demo](https://flashist.github.io/fexamples/) | [Demo Source](https://github.com/flashist/fexamples)**

# Feedback
- Slack Channel: https://flashist.slack.com/messages/fconsole/
- Skype: flashist-ru
- Email: ruFlashist@gmail.com

# Features

## Display List Inspector

### Hierarchy
![Display List Inspector - Hierarchy](https://github.com/flashist/flashist.github.io/blob/master/fexamples/images/demo/display-list-inspector_hierarchy.gif?raw=true)

#### How to:
1. Open the console by inputting a password (default is **`**). In the [demo](https://flashist.github.io/fexamples/) the console is shown from the beginning.
2. Click on the **DL** button.
3. Move cursor over some visual elements.

### Properties Editing
![Display List Inspector - Editing](https://github.com/flashist/flashist.github.io/blob/master/fexamples/images/demo/display-list-inspector_editing.gif?raw=true)

#### How to:
1. Assing a capture key to the Display List popup (click to the **Capture key** button and press a key).
2. Move cursor over some visual elements.
3. Press the assinged key (see #1).
4. Open Developer Tools Console in browser (Google Chrome Win: F12 or Ctrl + Shift + I, MacOS: CMD + Alt + I).
5. Check the display list hierarchy in the console.
6. Expand an object and change it's properties
7. (Optional, Google Chrome) Store an object as a Global Variable from context menu (right click on the object)

### Additional Information
![Display List Inspector - Editing](https://github.com/flashist/flashist.github.io/blob/master/fexamples/images/demo/display-list-inspector_additional-info.gif?raw=true)

#### How to:
1. Click on the **Additional Info** button.
2. Move cursor over some visual elements.
3. Check the additional information next to the hierarchy visual elements.
4. (Optional) Parameters shown in the additional info mode can be modified by changing the `FC.config.displayListSettings.additionalInfoParams` parameter.

### Move Helper
![Display List Inspector - Editing](https://github.com/flashist/flashist.github.io/blob/master/fexamples/images/demo/display-list-inspector_move-helper.gif?raw=true)

#### How to:
1. Click on the **Move Helper** button.
2. Move cursor over some visual elements.
3. Press the **CTRL** button.
4. The text **[MOVABLE]** will be shown next to the current active movable object (if there is no **[MOVABLE]** text, it means that there is no selected objects).
5. Press the arrow keys (← ↑ → ↓) to move the active movable object. Combine the **SHIFT** key and the arrow keys to move objects to the 10px in any direction.
 
# Installation

FConsole can be installed with [NPM](https://docs.npmjs.com/getting-started/what-is-npm):

```
$> npm install fconsole
```

# Usage Example (TypeScript)

## With Modern PixiJS (v8+)

To use FConsole with PixiJS v8, you need to provide a shimmed stage that allows FConsole to access the renderer and ticker, as they are no longer globally exposed in the same way.

```typescript
import { Application } from "pixi.js";
import { FC } from "@flashist/fconsole";

(async () => {
    const app = new Application();
    await app.init({ resizeTo: window });
    document.body.appendChild(app.canvas);

    // FConsole v8 Shim: The stage needs direct access to the ticker and renderer
    const stageShim: any = app.stage;
    stageShim.ticker = app.ticker;
    stageShim.renderer = app.renderer;

    // Initialize the console
    FC.startInit(stageShim);
    FC.visible = true;

    // Toggle with Backquote (`)
    window.addEventListener("keydown", (e) => {
        if (e.code === "Backquote") {
            FC.visible = !FC.visible;
        }
    });
})();
```

# Notes
\* Actually, there are only 2 implemented features yet (up to the August 29, 2016): Display List Inspector and Properties Editing. In my opinion, these two are the most useful and important features from [Flash-Console](https://github.com/junkbyte/flash-console) and I wanted to implement them the first. [Other features are planned](https://github.com/flashist/fconsole/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement) to be implemented.

\*\* At the current moment (up to the August 29, 2016) the console works only with Pixi.js library but the [fgraphics](https://github.com/flashist/fgraphics) lib was developed to be enhanced for supporting different game engines. [The next major adapter which is planned](https://github.com/flashist/fconsole/issues/4) to be implemented is the [EaselJS](https://github.com/CreateJS/EaselJS) adapter.
