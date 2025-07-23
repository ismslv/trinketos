# <img src="https://trinketos.org/images/icon_tapps.png" height="40px"/> Tapps and Mini-Tapps

Tapps, or Trinket Apps, are custom applications or scripts you can write for TrinketOS. Users place them in `TrinketOS/Tapps` and `TrinketOS/Scripts` folders and add to their UI or launch from the menu.

They can be games, utilities, web api displays and even full-fledged interfaces, because users can assign Tapp to be a Tab.

### Devices and limitations

- TrinketOS supports small screens and all screen orientations. So try to make your Big Tapps flexible. We advice using percentage and query units, such as vh, vw, cqh, cdw.
- TrinketOS supports Android SDK from 23 to 33+. Features work the best starting from SDK 28. Different SDK embed different versions of WebView / Android Chromium engine, that have their own limitations.
- - For example, full-fledged webAssembly integration works only on SDK 32+.
- - JavaScript standards also differ dramatically from version to version.

### Game engines

Some game engines can generate web builds. As an example, Godot does it in latest versions. These web builds can work as Tapps, because integrated local server can serve wasm/application file types.

> [!WARNING]
It highly depends on technology used and how js files are formed. Newer js standards, such as those that latest Godot versions are generating, need transpiling to older standards, e.g. using Babel. WebAssembly integration can also be an issue on older Android versions.

### Features that you can use in your Tapps

<table>
<tr><td><b>Tapps</b></td><td><b>Mini-Tapps</b></td></tr>
<tr><td>
Resources: <a href="#font">font</a>, <a href="#icons">icons</a>, <a href="#system-design">borders</a>
</td><td>
<a href="#types">On click actions</a>
</td></tr>
<tr><td>
<a href="#data">System data (username, colors)</a>
</td><td>
<a href="#files">Files</a> and <a href="#web">web</a> access
</td></tr>
<tr><td>
<a href="#sprite">Sprite speech</a>
</td>
<td>
<a href="#types">Sprite speech</a>
</td></tr>
<tr><td>
<a href="#stats">Stats</a>
</td><td>
<a href="#tapp-stats">Tapp stats</a>
</td></tr>
<tr><td>
<a href="#menu">Menu, checklist menu</a>
</td><td>
<a href="#menu-1">Menu</a>
</td></tr>
</table>

# <img src="https://trinketos.org/images/icon_tapp.png" height="40px"/> Tapps

Tapps are html applications that can be rendered into TrinketOS UI, use some system features and share system design.

There are three ways to load a Tapp: from `Settings → Tapps` list, create a list item for a list page or create a whole page that is a Tapp. Tapps can only be wide pages, i.e. take up both sides.

Use `Reload` to update the tapps list (it also happens on app start).

Tapps are placed into `TrinketOS/Tapps`. Each Tapp is a folder with files inside. The bare minimum is one html file. To use additional features, such as icon or configurations, create a file `config.json`.

If config file is not found, system will try to find index.html. Otherwise, it will use an html file defined in a config file.

You can also use images, fonts, js, css, wasm files or even game builds such as Godot.

Tapps support local storage, so you can save data between sessions. For example, if your tapp is a game, you can save user's score. You can also use **Stats** api instead, so your data is better integrated into the system and more safe between sessions.

### System UI

When tapp is running, interface is rendered in the following order:

<img src="https://trinketos.org/images/ui_stack.png?5" width="800px"/>

1. User-selected tab background
2. Background effects (lighten, darken)
3. Tapp background (behind the tapp and tab icon area). Color is blac kby default and can be set in config.json
4. WebView with tapp
5. Screen effects (such as CRT, noise etc).
6. Screen borders and mask
7. Tapp icon
8. Sprite and sprite speech bubble
9. Popup UI (e.g., achievements)

### Config file

Here's an example config.json in folder "test".

```json
{
    "name": "Test game",
    "html": "start.html",
    "icon": "icon.png",
    "author": "The Wizard",
    "link": "https://github.com/ismslv",
    "color": "#000000",
    "settings": {
        "key": "text",
        "with_animation": "check"
    },
    "stats": [
        ["highscore", "Highscore: %x", "trophy"],
        ["played_time", "Played for %x total"]
    ]
}
```

No fields are necessary.

If **name** is not defined, folder name will be used as a name.

If **html** is not defined, system will search for index.html.

**author** and **link** can be used to display your name and link in the tapps list.

**icon** is a name of the png file in the root of your tapp's folder.

**color** is used to paint background and tab area when tapp is running. It is black by default, but can even be transparent.

**settings** is a dictionary of name and type. Type can be **text** (for string input) and **check** (for checkbox). These settings will be shown in the tapp's menu. Their values will be sent to your tapp as url arguments for your html.

**stats** is an array of arrays. Inner arrays can be 2 or 3 items long. See `Stats` section.

If key is set to "secret" and with_animation is set to true, this example tapp will produce the following url: `TrinketOS/Tapps/test/start.html?key=secret&with_animation=1`

### Icon

Icon is a square png file with a transparent background.

We recommend creating white monochrome pixel icons, so that system could recolor them according to user's chosen colors.

Pixel-perfect icon is 16×16 px with 1-2 px margin around it. For not pixel-perfect we recommend choosing a size around 60-100px, so that Big Icons page could stretch them to a big size.

<img src="https://trinketos.org/images/icon_example.png?1" width="120px"/>

> [!NOTE]
> In some instances, if user choses so, you icon can be automatically pixelated.

## Resources

TrinketOS shares resources with Tapps, and we highly encourage you to match system style if possible.

Here's how to access them.

### Font

To use the system font, just use this in css:

```css
font-family: "pixelfont";
```

### Icons

To use icons, write url (for images or in css) in the following format, without extension:

```html
<img src="http://localhost:8080/trinketos/icons/aquarius" />
```

```css
.image-mushroom {
  background-image: url("http://localhost:8080/trinketos/icons/mushroom");
}
```

The names of the icons are listed in any place that lets you select a custom icon, for example in `Settings → Tabs`

### System design

If you want to create a block with system styles "border" (like tab or menu border) or "scroll", use the following styles (adapt padding to your case):

```css
.border {
    padding: 5px 10px 5px 10px;
    border: 12px solid;
    border-image: url("http://localhost:8080/trinketos/images/border") 10 10 10 10 stretch;
}

.scroll {
    padding: 15px 20px 15px 15px;
    border: 12px solid;
    border-image: url("http://localhost:8080/trinketos/images/scroll") 18 12 18 12 stretch;
}
```

## API

### Data

You can also access some system data. To be sure that data is available, listen to the "trinketDataReady" event:

```js
document.addEventListener('trinketDataReady', function(event) {
    document.getElementById('text').innerText = trinketData.strings.username;
    document.body.style.color = trinketData.colors.text;
});
```

The available data in **trinketData** object is:

- colors
- - text
- - titles
- - tab_icons
- - trinkets_top
- - trinkets_bottom
- - music
- - sprite
- strings
- - username

### Stats

Tapps can also have data accessible by the system. It is used in the following cases:

- In tapps list, to show current stats
- If a script has access to the tapp, it can show data on it's item
- If achievements are connected to the tapp (no public api for now), they check the stats

Stats are saved in the form of `<tappFolderName>_stats.json` in Tapps folder.

The structure of stats in config.json is the following: [statKey, statDescription, statIcon]

In stat description, `%x` will be replaced by the actual data. For example, `Highscore: %x` will become `Highscore: 100`. If no data is available, it will become **?** symbol.

If you want stat to be invisible in the menu (for example, for game save data that user has no use of), use only statKey without any description.

Stat icon is the optional parameter that will show an icon on the menu item. If icon is not specified, 'star' icon will be used. Icons names are found in the same place as script result icons.

- `["saveData"]` will allow loading and saving some data, but will not show it in the menu
- `["highscore", "Highscore: %x"]` will add it to the menu in the form "Highscore: 100"
- `["highscore", "Highscore: %x", "trophy"]` will add trophy icon to the menu item

To save the stats, use the following api:

```js
// TrinketOS.saveStat(statKey, statData)
TrinketOS.saveStat("highscore", highscore);
```

To get the stats, use the following api. You can use this instead of localStorage.

```js
// TrinketOS.getStat(statKey)
var clicks = TrinketOS.getStat('highscore');
```

### Sprite

<img src="https://trinketos.org/images/ui_sprite.png?1" width="300px"/>

You can make Sprite say your text. For example, you can use this to inform about events in your game like reaching some level, or alert about something. For this, use the following api:

```js
TrinketOS.spriteSay("You've reached " + level + " level!")
```

> [!NOTE]
> User can hide Sprite. Hidden Sprite does not talk.

### Menu

<img src="https://trinketos.org/images/ui_menu.png" width="400px"/>

You can show system popup menu with texts and icons or checkboxes and receive the result.

To show a menu:

```js
TrinketOS.showMenu(
    JSON.stringify([
        {
            text: "Choose a method!"
        },
        {
            text: "Throw a dice",
            icon: "DICE_5",
            result: "random_dice"
        },
        {
            text: "Look at magic orb",
            icon: "MIDNIGHT",
            result: "random_orb"
        },
        {
            text: "Roll a 9-ball",
            icon: "BALL",
            result: "random_ball"
        }
    ])
);
```

To show a menu with checkboxes:

```js
// Choose game difficulty
TrinketOS.showMenuChoose(
    JSON.stringify([
        {
            text: "Easy",
            result: "difficulty_1"
        },
        {
            text: "Normal",
            result: "difficulty_2",
            chosen: true
        },
        {
            text: "Hard",
            result: "difficulty_3"
        },
    ])
);
```

> [!NOTE]
> **icon** is optional
> 
> If you omit **result**, this item will be rendered as a title
> 
> Show the menu with only one title item to use it as a popup message

To retrieve the result, listen to the **trinketMenuResult** event:

```js
document.addEventListener('trinketMenuResult', function(event) {
    let result = event.detail.result;
    if (result == "difficulty_1") {
        // do somethign with the result
    }
    
    // If you have multiple menus in the app, you can pass menu name in the result
    if (result.startsWith("difficulty_")) {
        // Difficulty chooser
        let difficulty = result.substring(11);
    } else if (result.startsWith("random_")) {
        // Action chooser
        let action = result.substring(7);
    }
});
```

# <img src="https://trinketos.org/images/icon_script.png" height="40px"/> Mini-Tapps

Mini-Tapps really conform to their name. They provide user only two things: information rendered on a list item and a tap.

On the back end, they are scripts that are executed when page containing an item is rendered. For now, you can use JS or LUA languages.

Script files are placed into `TrinketOS/Scripts`. This folder is accessible to scripts, so your script can load other scripts from it, or read and write files.

> [!IMPORTANT]
> To execute JS scripts, we use [Rhino library](https://github.com/mozilla/rhino). It does not support all the newest standards of JavaScript, notably part of ES6 specifications.

### Display

`Settings → Tapps → Mini-Tapps`

Use `Reload` to update the scripts list (it also happens on app start).

Use `Manage` to see the list of loaded scripts. You can click items in list to see the result.

Then you can add scripts to UI using `Tabs → <your tab with List Page> → add Mini-Tapp`, then select script from the menu. When tab is opened, script will be executed and the result rendered into the list.

### Result

The simple way is to just return data in text form. Item will show the icon that user has set in tabs menu.

You can also return json. The possible values are:

- **result**: your text
- **icon**: the name of icon to show
- **type**: what item will do on click, see `Types`
- **typeResult**: data to act upon

### Types

<table>
<tr><td><b>type</b></td><td><b>on click</b></td><td><b>typeData</b></td></tr>
<tr><td><b>none</b></td><td>does nothing (default value)</td><td>-</td></tr>
<tr><td><b>self</b></td><td>reloads the script and rerenders the item</td><td>-</td></tr>
<tr><td><b>web</b></td><td>shows web view on the opposite side</td><td>url</td></tr>
<tr><td><b>tapp</b></td><td>tries to launch tapp</td><td>tapp's folder name</td></tr>
<tr><td><b>app</b></td><td>tries to launch app</td><td>app's name (not package name!)</td></tr>
<tr><td><b>folder</b></td><td>shows folder view on the opposite page</td><td>folder path in internal storage (e.g. `/TrinketOS/Scripts`)</td></tr>
<tr><td><b>tab</b></td><td>opens the tab</td><td>name of the tab</td></tr>
<tr><td><b>sprite</b></td><td>makes Sprite say your text</td><td>text to say</td></tr>
<tr><td><b>menu</b></td><td>shows menu</td><td>menu data (see Menu section)</td></tr>
</table>

### Return examples

```js
// Simple return
var currentdate = new Date();
currentdate.getDate();
```

```js
// json return
var currentdate = new Date();
JSON.stringify({
  result: currentdate.getDate(),
  icon: "book",
  type: "app",
  typeData: "Calendar"
});
```

## API

### Files

To access the files in "Scripts" folder, use `file.read` and `file.write`

Example (shows random quote from the file):

```js
// JS
var quotes = file.read("quotes.txt").split("\n");
quotes[Math.floor(Math.random() * quotes.length)];
```

```lua
-- LUA
local q = file.read("quotes.txt")
-- split method is not implemented here for brevity
local quotes = q:split("\n")
return quotes[math.random(#quotes)]
```

### Web

To make API calls, use `http.get`

```js
// JS
var response = http.get("https://goweather.xyz/weather/Paris");
var data = JSON.parse(response);
data.temperature;
```

```lua
-- LUA
json = require "json"
-- this will load json.lua from the Scripts folder
local response = http.get("https://goweather.xyz/weather/Paris")
local weather = json.decode(response)
return json.encode({
    icon = "rainy_day",
    result = weather.temperature
})
```

> [!NOTE]
> Web access can be slow, so Script will be loaded first with an empty value and than will try to get a result asynchronously.

> [!IMPORTANT]
> Note that web, files and tapp access can be a vulnerability for user's data, so user has the ability to disable this access for scripts. This means you are not guaranteed to be able to get that data.

### Tapp stats

You can access data from a tapp. Example usage is if you want to create a pair of tapp + script: item that shows tapp's stats and launches that tapp on click.

For this, use `tapp.getStat` with tapp's folder name (not tapp name!) and stat name.

```js
// JS
var highscore = tapp.getStat('mytapp', 'highscore')
JSON.stringify({
  result: "Highscore: " + highscore,
  icon: "star",
  type: "tapp",
  typeData: "mytapp"
});
```

```lua
-- LUA
json = require "json"
local highscore = tapp.getStat("mytapp", "highscore")
return json.encode({
    icon = "star",
    result = "Highscore: " .. highscore,
    type = "tapp",
    typeData = "mytapp"
})
```

### Menu

As in big Tapps, you can show menu on item click. For this, in return set **type** to **menu** and form **typeData** in the following manner: `item1Text|item1Icon,item2Text|item2Icon`

Icon is optional, but don't forget | symbol.

To render item as title, use _ prefix for name.

Example:

```js
JSON.stringify({
    result: "show menu",
    icon: "list",
    type: "menu",
    typeData: "_Select website!|,Throw a dice|dice_5,Look at orb|midnight,Roll a 9-ball|ball"
});
```

```lua
return json.encode({
    result = "show menu",
    icon = "list",
    type = "menu",
    typeData = "_Select website!|,Throw a dice|dice_5,Look at orb|midnight,Roll a 9-ball|ball"
})
```

When menu item is clicked, system will run the same script again, injecting the name of the selected item as `inputVal` global variable. Then it will retrieve the result and if it is not empty or "none", will "click" on it again.

Example mini-tapp for sites list:

```js
const sites = {
    "Site1": "site1.net",
    "Site2": "site2.org"
};

if (inputVal != "") {
    // Open site
    JSON.stringify({
        result: "",
        type: "web",
        typeData: sites[inputVal]
    });
} else {
    // Show menu
    var sitesItems = Object.keys(sites).map(function(key) {
        return key + '|web';
    }).join(',');

    JSON.stringify({
        result: "Important sites",
        icon: "web",
        type: "menu",
        typeData: "_Choose a site to open|," + sitesItems
    });
}
```
