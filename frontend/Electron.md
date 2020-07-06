Electron
==========

```shell script
npm install --save electron

npm i --save fluent-ffmpeg // get video info
```

## Inter process communication (IPC)
              IPC
Electron App <--->  Main Window
// index.html
```shell script
const electron = require('electon')
const { ipcRenderer } = electon;

button.on('click', () => {
  ipcRenderer.send('video:submit', filepath);
})


ipcRenderer.on('video:metadata', (event, duration) => {
  
})
```

// index.js
```shell script
const ffmpeg = require('fluent-ffmpeg');
const electron = require('electron');
const { app, BrowserWindow, ipcMain } = electron;

let mainWindow;
app.on('ready', () => {
  mainWindow = new BrowserWindow({});
  mainWindow.loadURL(`file://${__dirname}/index.html`);
  mainWindow.on('closed', () => app.quit()); // browser is closed
});

ipcMain.on('video:submit', (event, path) => {
  ffmpeg.ffprobe(path, (err, metadata) => {
    mainWindow.webContents.send('video:metadata', metadata.format.duration);
  })
})
```

## Menu
// index.js
```shell script
const { app, BrowserWindow, Menu } = electron;

app.on('ready', () => {
  mainWindow = new BrowserWindow({});
  mainWindow.loadURL(`file://${__dirname}/index.html`);

  const mainMenu = Menu.buildFromTemplate(menuTemplate);
  Menu.setApplicationMenu(mainMenu);
});

const menuTemplate = [
  // {}, // default menu "Electron"
  {
    label: 'File',
    submenu: [
      { role: 'reload' }, // reload window
      { label: 'New Todo' 
        click(): { createNewWindow(); }
      },
      {
        label: 'Quit',
        //accelerator: 'Command+Q', // shortcut for Mac
        accelerator: ( () => {
          return process.platform === 'darwin' ? 'Command+Q' : 'Ctrl+Q';
        }),
        click() {
          app.quit();
        }
       }
    ]
  }
];

if (process.platform === 'darwin') {  // Mac
  menuTemplate.unshift({}); // make Mac menu appeare the same as Windows
}
``` 

## New Window
// index.js
```shell script
function createAddWindow() {
  addWindow = new BrowserWindow( {
    width: 300,
    height: 200,
    title: 'Add New Todo',
    frame: false,  // hide task bar, eg close, maximize
    resizable: false
  });
  addWindow.loadURL(`file://${__dirname}/add.html`);
  addWindow.on('closed', () => addWindow = null); // for GC
}

if (process.env.NODE_ENV != 'production') {
  menuTemplate.push({
    label: 'View',
    accelerator: process.platform === 'darwin' ?  'Command+Alt+I' : 'Ctrl+Alt+I',
    submenu: [
      {
        label: 'Toggle Dev Tools',
        click(item, focusedWindow): {
          focusedWindow.toggleDevTools();
        }
      }
    ]   
  }
  });
}

ipcMain.on('todo:add', (event, todo) => {
  mainWindow.webContents.send('todo:add', todo); 
  addWindow.close();
}

```

// main.html
```shell script
const { ipcRenderer } = electron;
ipcRenderer.on('todo:add', (event, todo) => {
  todos.push(todo); 
}
```


## Status Tray
[Sample code](github.com/stephenGrider/electronCode)
// index.js for electron
```shell script
const path = require('path');
const electron = require('electron');
const TimerTray = require('./app/timer_tray');
const MainWindow = require('./app/main_window');

const { app, ipcMain } = electron;

let mainWindow;
let tray;

app.on('ready', () => {
  app.dock.hide();
  mainWindow = new MainWindow(`file://${__dirname}/src/index.html`);

  const iconName = process.platform === 'win32' ? 'windows-icon.png' : 'iconTemplate.png';
  const iconPath = path.join(__dirname, `./src/assets/${iconName}`);
  tray = new TimerTray(iconPath, mainWindow);
});

ipcMain.on('update-timer', (event, timeLeft) => {
  tray.setTitle(timeLeft);
});
```

// main_window.js
```shell script
const electron = require('electron');
const { BrowserWindow } = electron;

class MainWindow extends BrowserWindow {
  constructor(url) {
    super({
      height: 500,
      width: 300,
      frame: false,
      resizable: false,
      show: false,
      webPreferences: { backgroundThrottling: false }
    });

    this.loadURL(url);
    this.on('blur', this.onBlur.bind(this));
  }

  onBlur() {
    this.hide();
  }
}

module.exports = MainWindow;
```

// timer_tray.js
```shell script
const electron = require('electron');
const { Tray, app, Menu } = electron;

class TimerTray extends Tray {
  constructor(iconPath, mainWindow) {
    super(iconPath);

    this.mainWindow = mainWindow;

    this.setToolTip('Timer App'); // tray tooltip
    this.on('click', this.onClick.bind(this));
    this.on('right-click', this.onRightClick.bind(this));
  }

  onClick(event, bounds) {
    // Click event bounds
    const { x, y } = bounds;

    // Window height and width
    const { height, width } = this.mainWindow.getBounds();

    if (this.mainWindow.isVisible()) {
      this.mainWindow.hide();
    } else {
      const yPosition = process.platform === 'darwin' ? y : y - height;
      this.mainWindow.setBounds({
        x: x - width / 2,
        y: yPosition,
        height,
        width
      });
      this.mainWindow.show();
    }
  }

  onRightClick() {
    const menuConfig = Menu.buildFromTemplate([
      {
        label: 'Quit',
        click: () => app.quit()
      }
    ]);

    this.popUpContextMenu(menuConfig);
  }
}

module.exports = TimerTray;
```


