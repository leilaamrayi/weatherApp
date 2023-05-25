# weather-app

There are two different codes for this app which each one has different way of searching for location and different way in showing the last three search locations buttons.

#weather-app-searchAutomaticlyByUserLocation
If you open and run the code in this folder app start to search the weather automatically by user location for starting the app user need to allow the app to access to user location.
There are three fixed buttons which value of the first one is user current location, the two other buttons will be updated one by one by , by value of location of three last searched locations.

#weather-app-searchByLocation
If you open and run the code in this folder app first ask to enter the location, when you entered the location app show the information of weather of the location and add a button to app that is equal to value of entered location. If you search other location the second button with the value of the entered location add to the app. This happened for third searched locations after the third searched the value of the buttons will updated with new searches one by one.

## Project Setup
 npm install
## Compile and Hot-Reload 
npm run dev












This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin) to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension
    1) Run `Extensions: Show Built-in Extensions` from VSCode's command palette
    2) Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`
2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```
