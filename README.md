# Capacitor

## [Install CLI](https://ionicframework.com/docs/intro/cli)

```bash
$ npm uninstall -g ionic
$ npm install -g @ionic/cli
```

## Resources
- [Building Ionic Desktop Apps with Capacitor and Electron](https://devdactic.com/ionic-desktop-electron)

## Getting Started
```bash
ionic start capacitorApp blank --type=react --capacitor
cd ./capacitorApp

# If your template is not yet using Angular 9
#ng update @angular/cli @angular/core --allow-dirty

# Needed to run once before adding Capacitor platforms
ionic build # or npm run build
# Run following in dist folder to see application in the browser
cd dist
ionic serve
```

### Adding electron - old
```bash
npm install ngx-electron electron
npm install electron-packager --save-dev
# Run `ionic capacitor add` to add a native iOS or Android project using Capacitor
cd ../
npx cap add electron
npx cap open electron
ionic build
npx cap copy
npx cap open electron
```
To build your electron application add the following to `package.json`
```json
"scripts": {
  "electron:mac": "electron-packager ./electron SimonsApp --overwrite --platform=darwin --arch=x64 --prune=true --out=release-builds",
  "electron:win": "electron-packager ./electron SimonsApp --overwrite --asar=true --platform=win32 --arch=ia32 --prune=true --out=release-builds --version-string.CompanyName=CE --version-string.FileDescription=CE --version-string.ProductName='Simons Electron App'"
}
```
then run `npm run electron:win` or `npm run electron:mac`
The above doesn't built as it outputs
`ENOENT: no such file or directory, stat 'D:\Users\Public\dev\git\capacitorApp\electron'`.


### Adding electron - new

```bash
npm install @capacitor-community/electron
npx cap add @capacitor-community/electron
npx cap open @capacitor-community/electron
```
You can use other `npx cap` commands with the platform by: `npx cap <command> @capacitor-community/electron`
You may need to update some of the electron packages with;
```bash
npm view electron-updater version
npm install electron-updater@6.1.7
npm view electron-builder version
npm install electron-builder@24.9.1
```

```bash
cd electron
# WIthin the electron/package.json you'll see list of scripts you can run.
npm run build
npm run electron:start-live
npm run electron:pack
npm run electron:make
```
If make fails due to no publishing repository specified then remove the following from `electron/electron-builder.config.json`
```json
"publish": {
  "provider": "github"
},
```

### Adding [Android](https://capacitorjs.com/docs/android)

```bash
npm install @capacitor/android
npx cap add android
npx cap open android
```
You can either run your app on the command-line or with Android Studio.
```bash
npx cap run android
```
If the above errors. You'll likely need to have [a virtual device](https://developer.android.com/studio/run/managing-avds) created. Either a physical Android device or a downloaded emulator system image is required to use the run command.
Errors in android studio, you'll likely have to update android studio's, the SDK and the virtual device.

### Adding [IOS](https://capacitorjs.com/docs/ios)
IOS 13+ is supported and uses WKWebView.
Requirements:
- XCode 14.1+, which can only be installed on macOS

```bash
npm install @capacitor/ios
npx cap add ios
npx cap open ios
npx cap run ios
```
Alternatively you can open xcode by running;
```bash
open ios/App/App.xcworkspace
```
