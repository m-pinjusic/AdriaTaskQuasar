# AdriaTaskQuasar
Task for insight into the ability to perform work

## Install the dependencies

```
npm install -g @quasar/cli
```

```bash
npm install
```


### Start the app in development mode (hot-code reloading, error reporting, etc.)

```bash
quasar dev
```

### Lint the files

```bash
npm run lint
```

### Format the files

```bash
npm run format
```

### Build the app for production

```bash
quasar build
```

### Customize the configuration

See [Configuring quasar.conf.js](https://quasar.dev/quasar-cli/quasar-conf-js).

### If error

If there is a error “quasar. ps1 cannot be loaded because running scripts is disabled on this system…”
Run Poweshell and run command “Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned “.

### Function test:

To check the quality of air in Rijeka, see 5 important air quality elements in header of page. To see more details about it, hover with mouse over element. 
On the left is drawer with home tab and list of all controllers. On the bottom of drawer is todays date and date of next holiday in Croatia. To see more about that check console log on page.

On first page there is a list of all controllers and their zone, name and address. Every controller has QR code button and Details button. Clicking on QR code button generates QR code with name of controller. Button details opens new page just like tabs on drawer. Controller page has all basic details and selected properties: Set temperature, Current temperature, DND and Occupied. If there is no DND or Occupied, it means that the value is false. Set temperature is saved on local storage every time page of controller is loaded and it can be seen on console or in storage of browser(Inspect element->Application->Storage->Local Storage). Button Settings on controller page opens a list of all settings parameters. 
