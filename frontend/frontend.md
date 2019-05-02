# sukeltaja-frontend

## 🐞 Known issues

### Changes to `.env` files are not updated

This is [an issue with react-native-dotenv](https://github.com/zetachang/react-native-dotenv#faq). Manually edit and re-save the file that imports the environment variables from `react-native-dotenv`. We didn't during the project find any better alternative to replace [dotenv](https://github.com/motdotla/dotenv), which does not run on React Native.

### "SyntaxError: Try to import dotenv variable..." when running tests in Travis

More `.env` problems, a hacky hotfix was to create an `.env.development` with only the required keys and NO values whatsoever. Probably not the best solution.

## 📖 Notes on packages used

A link to the documentation of each package is provided in each heading.

### [axios](https://github.com/axios/axios)

An http client used to make http requests. Basically a replacement for Fetch API.

### [axios-retry](https://github.com/softonic/axios-retry)

An axios plugin that retries failed requests. We used this originally due to Heroku servers notoriously not working that well. All instances of `axios-retry` could in theory be deleted in the future.

### [luxon](https://moment.github.io/luxon/docs/index.html)

A powerful wrapper to deal with JavaScript dates and times. Has built-in localization which has been used in the frontend, but [React Native for Android doesn't support intl out of the box](https://moment.github.io/luxon/docs/manual/install.html).

### [react-native-elements](https://react-native-training.github.io/react-native-elements/docs/overview.html)

UI toolkit similar to Bootstrap. The philosophy regarding usage has been mostly:

1. use `react-native` components where possible
2. if not, use `react-native-elements` where possible
3. if not, find another, well-maintained alternative.

### [react-native-maps](https://github.com/react-native-community/react-native-maps)

The map component used in the app. By default uses Google Maps on Android phones, Apple Maps on iOS phones.

### [react-native-maps-super-cluster](https://github.com/novalabio/react-native-maps-super-cluster)

Wraps [react-native-maps](https://github.com/react-native-community/react-native-maps) with a clustering engine in order to easily cluster map markers together.

### [react-navigation](https://reactnavigation.org/docs/en/getting-started.html)

Used to navigate between different views in the app. The component folders have a file called `index.js` to most of the time handle the navigation. [StackNavigators](https://reactnavigation.org/docs/en/stack-navigator.html) and [SwitchNavigators](https://reactnavigation.org/docs/en/switch-navigator.html) should cover most of your needs.

Sometimes using a conditional return is favorable compared to using SwitchNavigators, if for example you need to check that a user is logged in before they're allowed on a screen. Make sure to use a class component and give the appropriate router to the component as a static variable. And finally, pass props to the component. **(insert relevant links here)**

### [socket.io-client](https://github.com/socketio/socket.io-client)

Used to communicate through [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) in order to update "real-time" events such as event chat, updates to events, invites to events and so on. React Native actually has [WebSocket support out of the box](https://facebook.github.io/react-native/docs/network#websocket-support), so using `socket.io` was not totally necessary, as it supposedly adds a [180 Kb overhead to every connection](https://stackoverflow.com/a/38558531).

### [tcomb-form-native](https://github.com/gcanti/tcomb-form-native)

Styled and auto-validated forms for React Native. Not maintained that much anymore, and at least on iOS Expo (production mode) opening views with forms [dropped some frames](https://github.com/Sukeltaja-App/sukeltaja-frontend/issues/18). Might need replacement in the future.
