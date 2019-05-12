# sukeltaja-frontend documentation

## 🐗 Quick start

1. Install Expo Client from your favorite app store ([Google Play](https://play.google.com/store/apps/details?id=host.exp.exponent)) ([App Store](https://itunes.apple.com/us/app/expo-client/id982107779))
2. Make sure you're in the same wireless connection with your phone and the computer running the local frontend server
3. `git clone https://github.com/Sukeltaja-App/sukeltaja-frontend.git`
4. `cd sukeltaja-frontend`
5. `npm install`
6. `npm start`
7. Make sure your `.env` file is correct
8. Use your phone camera (iOS) or the Expo Client (Android) to scan the server QR code.

[More in-depth documentation and known issues here](frontend.md).

[Documentation about the user interface (looks) here](user_interface.md).

## ℹ General information

The frontend is developed using [React Native](https://facebook.github.io/react-native/) and [Expo](https://expo.io/).

### Debugging

There's some very good advice about debugging in [Expo's website](https://docs.expo.io/versions/latest/workflow/debugging/).

Supposedly debugging all of Redux, props and state works using [react-native-debugger](https://github.com/jhen0409/react-native-debugger). This has not been tested by us, instructions are on the Expo website link above.

If you ever need to inspect props or state, you can use Expo's `Debug Remote JS` in conjunction with [react-devtools](https://github.com/facebook/react-devtools). This slows down the app considerably, so you might not want to do this all the time.

Expo features live and hot reloading. There's also [a very handy performance monitor](https://docs.expo.io/versions/v28.0.0/react-native/performance/). You shouldn't test performance on Development mode though, as it's considerably slower. When looking at performance, all mobile apps should run at 60 frames per second all the time.

### React Native

React Native is a framework to develop mobile apps using [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) and [React](https://reactjs.org/). Using React Native you (most of the time) don't have to worry about iOS or Android platform specifics. However, it's possible to drop down into native code if needed.

### Expo

Expo is a set of development tools used with React Native to streamline React Native development.

Expo Client can be downloaded ([Google Play](https://play.google.com/store/apps/details?id=host.exp.exponent)) ([App Store](https://itunes.apple.com/us/app/expo-client/id982107779)) to a smartphone in order to develop with a real device and enjoy features such as live/hot reloading, inspecting elements, testing performance and debugging.

Or you can install [Android Studio](https://developer.android.com/studio) / [XCode](https://developer.apple.com/xcode/) and test your program using iOS or Android simulators.

### expo-cli

`expo-cli` is the command line interface for expo. Run `expo help` to get a list of commands to use. Most of the time you will be only starting the server (through `npm start`) or making a new build with `expo build:android` | `expo build:ios`. Configurations for expo build should be added on app.json on the root folder of the repository.

`expo eject` can be used to eject the project from Expo, providing you with native projects that can be opened and built in Xcode and Android Studio. This can be done if the project desperately needs a native module that Expo does not support. ⚠️**WARNING!**⚠️ You probably don't ever have to do this. Make sure that you understand what you are doing. [More info here](https://docs.expo.io/versions/latest/expokit/eject/).
