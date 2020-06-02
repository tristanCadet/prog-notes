# Ionic

Build cross-platform apps for iOS, Android and the Web with only one code-base

##### Prerequisite

- Node.js
- Ionic

```bash
npm install -g @ionic/cli 								# install ionic via npm
```

##### Project Set-up

```bash
ionic start myProject predefinedTemplate --type react 	# create new react project
cd myProject
ionic serve 											# serve live reload server
```

##### My First-app

https://ionicframework.com/docs/react/your-first-app

```bash
# native-run, used to run native binaries on devices and simulators/emulators
# cordova-res, used to generate native app icons and splash screens
npm install -g native-run cordova-res 
```

```bash
# capacitator allows access to native SDK and cross-platform deployment
# (Software Development Kit, to develop on specific platforms)
ionic start photo-gallery tabs --type=react --capacitor
#> ionic integrations enable capacitor
cd photo-gallery
```

```bash
# React Hooks: react library for capacitator
# PWA (Progressive WebApps) elements: pre-built web-based UI elems such as camera/video
npm install @ionic/react-hooks @ionic/pwa-elements
```

###### Use PWA elements

```typescript
// index.tsx
import { defineCustomElements } from '@ionic/pwa-elements/loader';

// Call the element loader after the app has been rendered for the 1st time
defineCustomElements(window);
```

###### Run app (available in browser)

```bash
ionic serve
```

###### Photo Gallery

**IonHeader** top navigation and toolbar

**IonContent** visual aspect of app (e.g. camera, photo)

**FAB** (Floating-Action Button) fixed button that contains a list of action buttons

**Action sheet** dialog button that displays a set of options

tab2.tsx <

- change header title
- import ionic icons and various components
- add FAB (align, onClick fun, icon)

App.tsx <

- change IonTabButton icon & label in IonTabBar (tabs at the bottom of the app)