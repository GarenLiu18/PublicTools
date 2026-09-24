# ToolBox

A lightweight collection of browser-based development tools built with pure HTML, CSS, and JavaScript.

No backend is required. All tools run locally in the browser.

## Tools

### SequanceChecker

A local viewer for PNG frame sequences and GIF animations.

Useful for quickly browsing animation assets and copying normalized resource paths.

#### Features

* Select and recursively scan a local folder
* Preview PNG frame sequences as animations
* Preview GIF files directly
* Automatically group numbered PNG frames into sequences
* Preserve the original folder structure
* Collapse folders by default
* Automatically flatten folders that contain only one sequence
* Click an animation to copy its normalized resource path
* Adjustable preview image scale
* Fixed preview frame size
* Lazy rendering

  * Animations are only rendered while their folder is expanded
  * Animation timers and Blob URLs are released when the folder is collapsed
* Remember the previously selected folder
* Automatically reload the latest files from that folder
* No file upload
* No backend

## Supported Sequence Naming

SequanceChecker detects frame numbers at the end of a file name.

For example:

```text
Idle001.png
Idle002.png
Idle003.png
```

```text
Idle01.png
Idle02.png
Idle03.png
```

```text
Idle_001.png
Idle_002.png
Idle_003.png
```

All of the examples above are grouped as:

```text
Idle
```

Another example:

```text
Attack_0001.png
Attack_0002.png
Attack_0003.png
```

is grouped as:

```text
Attack
```

## Path Copying

Given this folder structure:

```text
Sequance/
└── Avatar/
    └── Idle/
        ├── Idle001.png
        ├── Idle002.png
        └── Idle003.png
```

Clicking the `Idle` animation copies:

```text
Sequance/Avatar/Idle/Idle
```

The frame number and file extension are automatically removed.

## Folder Display

If a folder contains multiple sequences:

```text
Combat/
├── Attack001.png
├── Attack002.png
├── Hit001.png
└── Hit002.png
```

the folder remains available as a collapsible group.

If a folder contains only one sequence:

```text
Idle/
├── Idle001.png
├── Idle002.png
└── Idle003.png
```

the extra folder level is flattened in the UI and the animation is displayed directly in its parent folder.

The copied path is not affected by this visual flattening.

## Project Structure

```text
ToolBox/
├── index.html
├── SequanceChecker.html
└── README.md
```

### `index.html`

Main entry point for ToolBox.

Displays the available tools.

### `SequanceChecker.html`

PNG sequence and GIF animation viewer.

## Usage

Clone or download the repository:

```bash
git clone <repository-url>
```

Open:

```text
index.html
```

Then select:

```text
SequanceChecker
```

Click:

```text
Select Folder
```

and choose the root folder containing your animation assets.

## Folder Persistence

SequanceChecker uses the File System Access API together with IndexedDB.

After selecting a folder for the first time, the browser stores its `FileSystemDirectoryHandle`.

On future visits:

* If permission is still granted, SequanceChecker reloads and rescans the folder automatically
* If permission must be renewed, the user can authorize the previously selected folder again
* The actual PNG and GIF files are not stored in IndexedDB
* Animation data is always loaded again from the local folder

This means newly added or modified files are visible after rescanning.

## Privacy

All assets are processed locally inside the browser.

SequanceChecker does not:

* Upload files
* Upload folders
* Send animation assets to a server
* Store PNG or GIF contents
* Require an account
* Require a backend service

Only the browser-provided folder handle is persisted locally.

## Browser Support

Chromium-based browsers are recommended:

* Google Chrome
* Microsoft Edge

SequanceChecker relies on the File System Access API, so functionality may be limited or unavailable in browsers that do not support it.

## GitHub Pages

ToolBox is completely static and can be hosted directly with GitHub Pages.

A typical repository structure is:

```text
/
├── index.html
├── SequanceChecker.html
└── README.md
```

Enable GitHub Pages for the repository and use `index.html` as the entry page.

Local files are still accessed only after the user explicitly grants folder access through the browser.

## Adding More Tools

Create another HTML file:

```text
YourTool.html
```

Then add a card to `index.html`:

```html
<a class="tool-card" href="./YourTool.html">

    <div class="tool-icon">
        🛠️
    </div>

    <div class="tool-name">
        YourTool
    </div>

    <div class="tool-description">
        Tool description
    </div>

</a>
```

## Tech Stack

* HTML
* CSS
* Vanilla JavaScript
* File System Access API
* IndexedDB
* Clipboard API

## License

Add the license of your choice to the repository.

For example, if you want the project to be freely reusable and modifiable, you can add an MIT License.
