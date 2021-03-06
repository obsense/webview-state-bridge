# webview-state-bridge

## About

The `webview-state-bridge` package is a [redux](https://redux.js.org/)-powered state bridge between any [react](https://reactjs.org/) app running in a [react-native](https://reactnative.dev/) app through a [react-native-webview](https://github.com/react-native-community/react-native-webview).

## Getting Started

### Installation

In both react and react-native apps, install as follows.

```sh
yarn add webview-state-bridge
```

### Provider Components

In the `react` app, wrap the app root with the `NativeProvider` component.

```jsx
// react app root
import { WebProvider } from 'webview-state-bridge';
// ... Other code here ...
<WebProvider>
  <App />
</WebProvider>
```

```jsx
// react-native
import { NativeProvider } from 'webview-state-bridge';
import { WebView } from 'react-native-webview';
// ... Other code here ...
<NativeProvider>
  <WebView source={{ uri: 'https://localhost:3000' }} />
</NativeProvider>
```

### Redux Middleware

This package has two different pieces of [redux middleware](https://redux.js.org/advanced/middleware) for the two different react and react-native environments that help sync the redux states that need to be added to each app's redux store configuration.

#### With Redux

In the react app, add the middleware to the store configuration similar to the following.

```js
// react store config
import { createStore, applyMiddleware } from 'redux'
import { webMiddleware } from 'webview-state-bridge';
// ... Other code here ...
const store = createStore(yourReducers, yourInitialState, applyMiddleware(webMiddleware));
```

```js
// react-native store config
import { createStore, applyMiddleware } from 'redux'
import { nativeMiddleware } from 'webview-state-bridge';
// ... Other code here ...
const store = createStore(yourRootReducer, yourPreloadedState, applyMiddleware(nativeMiddleware));
```

#### With Redux Toolkit

[Redux Toolkit](https://redux-toolkit.js.org/) is `The official, opinionated, batteries-included toolset for efficient Redux development`. To preserve the default store configurations it provides install in your react and react-native apps as follows.

```js
// react store config
import { configureStore, getDefaultMiddleware } from '@reduxjs/toolkit';
import { webMiddleware } from 'webview-state-bridge';
// ... Other code here ...
const store = configureStore({
  reducer: yourRootReducer
  middleware: [...getDefaultMiddleware(), webMiddleware]
  devTools: process.env.NODE_ENV !== 'production',
  preloadedState: yourPreloadedState,
});
```

```js
// react-native store config
import { configureStore, getDefaultMiddleware } from '@reduxjs/toolkit';
import { nativeMiddleware } from 'webview-state-bridge';
// ... Other code here ...
const store = configureStore({
  reducer: yourRootReducer
  middleware: [...getDefaultMiddleware(), nativeMiddleware]
  devTools: process.env.NODE_ENV !== 'production',
  preloadedState: yourPreloadedState,
});
```

## Setup explained

WIP

## Example Integration

We wanted the setup and experience of using this package to be quick and enjoyable, so we've created two example apps to demo how this package enables easy universal react apps that can run anywhere.

The first app is a [Next.js](https://nextjs.org/) (hybrid SSG/SSR react framework) [PWA](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) that demos various hardware integrations through the `webview-state-bridge`.

The second is a simple `react-native` app running without the overhead of [Expo](https://expo.io/) (`webview-state-bridge` is fully compatible with Expo). The native app code is minimal, as a primary goal of this package is to provide the means to use traditional rock-solid web technologies we know and love such as react for the majority of the app code, while react-native is used as a native API provider to the react app with `webview-state-bridge` as the intuitive bridge between the two.

### Example/Starter App Integration

We've built out two entire applications that comprise two parts of a universal react app supporting desktop, android, and ios platforms with offline support.  

Please see the example/starter at [nextjs-react-native-starter](https://github.com/obsense/nextjs-react-native-starter).

## Contributing

We face difficult times together as our planet rapidly changes, we need to collaborate to face these daunting challenges. If this project helps you or your organization build universal apps faster, please consider contributing to the ongoing development and maintenance of this effort. We welcome any and all contributions which may include (but not limited to) any of the following.

- Reporting bugs, asking questions, proposing improvements, or any other ideas by [opening an issue](TODO-url-here).
- Documentation improvements, always appreciated!
- Code contributions! Please feel free to dig into the code to fix a bug, [open a PR](TODO-url-here), and we'll make sure the effort gets the attention it deserves.
- Feedback! All important to improving anything, we love to hear how you or your organization are using this code, what's working, what could be improved, and what isn't appreciated.
- Resources! If there's any related project/effort that we can link to and help our community find resources and grow, the better! Open an issue to mention it or better yet open a PR to add to the documentation.
