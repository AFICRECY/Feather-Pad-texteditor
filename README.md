# Feather-Pad (Social Media API)


## Technology Used:
| Technology Used         | Resource URL           |
| ------------- |:-------------:|
| Git | [https://git-scm.com/](https://git-scm.com/)     |
| HTML    | [https://developer.mozilla.org/en-US/docs/Web/HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) |
| CSS     | [https://developer.mozilla.org/en-US/docs/Web/CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)      |
| JavaScript  | [https://www.javascript.com/](https://www.javascript.com/)      |
| Node.js | [https://nodejs.org/en](https://nodejs.org/en)      |
| Express.js  | [https://expressjs.com/](https://expressjs.com/)   |
|  Nodemon  |     [https://www.npmjs.com/package/nodemon](https://www.npmjs.com/package/nodemon)   |
|  IndexedDB  |  [https://www.npmjs.com/package/idb](https://www.npmjs.com/package/idb)   |
|  Inject Manifest    |   [https://developer.chrome.com/docs/workbox/#injectmanifest_plugin](https://developer.chrome.com/docs/workbox/#injectmanifest_plugin)    |
| Workbox    |  [https://developer.chrome.com/docs/workbox/the-ways-of-workbox/#using-a-bundler](https://developer.chrome.com/docs/workbox/the-ways-of-workbox/#using-a-bundler)    |
|  Webpack   |   [https://webpack.js.org/](https://webpack.js.org/)    |


## Description:

Deployed Application Link:  https://feather-pad-texteditor.herokuapp.com/

Note-taking apps have become an essential tool in today's society as they offer convenience, organization, and accessibility for individuals across various domains. Whether it's capturing important ideas, creating to-do lists, or recording meeting minutes, these apps provide a digital space for efficient note-taking, eliminating the need for traditional pen and paper. Moreover, their synchronization capabilities enable seamless access to notes across multiple devices, ensuring information is readily available whenever and wherever it is needed. My task was to build a text editor that can both run in a browser as well as have the ability to be installable as an app. This application should also be accessible on a user’s device without internet connection. I created the Feather pad text editor application considering the criteria of a progressive web app (PWA). The key focus of this project is to ensure a seamless user experience with access to a note taker application that can be installed on a user's device and usable even offline. To create Feather Pad, I brought together many different kinds of software, plugins, and packages. The Feather Pad app can become an indispensable tool for students, researchers, and professionals, offering them the ability to store, organize, and collaborate on notes and research projects. Note taking applications that do not rely on the internet  play a crucial role in enhancing productivity and facilitating efficient information management in various domains. This digital notebook serves as a modern counterpart to traditional paper notebooks, enabling users to conveniently organize their notes and information and auto save on the go. 


### Screenshot of Functioning Web Application:

![App In Use](/client/src/images/Screenshot-of-app.png)


### Gif (Animation of app installation)
![Feather-pad](https://github.com/AFICRECY/NetBlend-SocialMedia-API/assets/101257805/dcdccdf1-f5b8-4686-870c-92daaf6fd88d)



## Table of Contents:
* [Description](#description)
* [Installation](#installation) 
<br>
(HTML, CSS, JavaScript, Node.js, NPM Packages, Webpack, PWA Paradigm, Functions, IndexedDB, Express.js, Heroku, Manifest.json, Service Workers)
<br>

* [Usage](#usage)
* [Credits](#credits)
* [License](#license)


<p>&nbsp;</p>


### Installation:

To install this project, a knowledge of HTML, CSS, JavaScript, Node.js, and Express.js, the Progressive Web Application Paradigm (PWAs), IndexedDB, Git, and Heroku  were required.  I had to first install Node.js to my computer and then install the Express and NPM packages. I installed the following dependencies with my npm install (express, manifest.json, webpack plugins, babel, workbox plugins, and nodemon).The Express package allowed me to use the express framework in Node.js. In order to create this application. The Feather Pad test editor application is designed as a single-page application, meeting the criteria of a Progressive Web App (PWA). Furthermore, it  incorporates various data persistence techniques, and functions within the browser as well as an installable app using the manifest dependency package. Additionally, the Feather Pad text editor has offline functionality, allowing users to continue using it even without an internet connection thanks to my usage of IndexedDB.  To simplify this process, I will employ the "idb" package, a lightweight wrapper around the IndexedDB, which is widely trusted by major companies like Google and Mozilla. By combining these technologies, I aim to create a powerful text editor that enables users to work on their documents seamlessly, regardless of their internet connectivity. This application extends beyond note-taking, offering versatile functionality for journaling, team tasks, work projects, programming, planning, and more. With its user-friendly interface and intuitive design, it seamlessly caters to both individual and team-based projects, ensuring a great user experience. 

The user should be able to navigate to the heroku deployed site linked at the start of this readme and click the install button. The Feather Pad text editor will install onto the users device and is ready for use. The code below make this happen: 

<p>&nbsp;</p>


### Root package.json
```json 
 "scripts": {
   "start:dev": "concurrently \"cd client && npm run dev\" \"cd server && npm run server\" ",
   "start": "npm run build && cd server && node server.js",
   "server": "cd server node server.js --ignore client",
   "build": "cd client && npm run build",
   "install": "cd server && npm i && cd ../client && npm i",
   "client": "cd client && npm start"
 },
```
(Above: The code lives in the root package.json files and they connect all of the package.json files in the client and sever folders. This package.json defines a set of scripts for running and building a full-stack application. It includes commands for starting the development environment concurrently, building the application, installing dependencies for both the server and client sides, and starting the client-side application.)


<p>&nbsp;</p>


### Server Folder: htmlRoutes.js
```js
const path = require('path');

module.exports = (app) =>
 app.get('/', (req, res) =>
   res.sendFile(path.join(__dirname, '../client/dist/index.html'))
 );
```
(Above: This code exports a function that takes an "app" parameter and defines a route for the root URL ("/") using the GET method. When this route is accessed, it sends the index.html file located in the "../client/dist" directory as the response. The "path" module is used to construct the file path in a platform-independent way.)

<p>&nbsp;</p>

### Server Folder: package.json
```json
 "scripts": {
   "dev": "webpack-dev-server",
   "build": "webpack --mode production",
   "start": "webpack --watch",
   "heroku-prebuild": "npm install --dev"
 },
```
(Above: This code defines a set of scripts that can be executed using npm. The "dev" script launches the webpack-dev-server for development purposes, while the "build" script triggers the production mode build with webpack. The "start" script enables webpack to watch for file changes, and the "heroku-prebuild" script installs development dependencies specifically for Heroku deployment.)

<p>&nbsp;</p>


### Server Folder: index.js
```js

if ('serviceWorker' in navigator) {
 const workboxSW = new Workbox('/src-sw.js');
 workboxSW.register();
} else {
 console.error('Service workers are not supported in this browser.');
}
```
(Above: This code checks to see if service workers are supported and also registers the workbox servive worker.)

<p>&nbsp;</p>


### Client Folder: database.js
```js
import { openDB } from 'idb';


const initdb = async () =>
 openDB('jate', 1, {
   upgrade(db) {
     if (db.objectStoreNames.contains('jate')) {
       console.log('jate database already exists');
       return;
     }
     db.createObjectStore('jate', { keyPath: 'id', autoIncrement: true });
     console.log('jate database created');
   },
 });

export const putDb = async (content) => {
 console.log('PUT to the database');
 const jateDb = await openDB('jate', 1);
 const tx = jateDb.transaction('jate', 'readwrite');
 const store = tx.objectStore('jate');
 const request = store.put({jate: content });
 const result = await request;
 console.log('Data saved to the database', result);
};

export const getDb = async () => {
 console.log('PUT to the database');
 const jateDb = await openDB('jate', 1);
 const tx = jateDb.transaction('jate', 'readonly');
 const store = tx.objectStore('jate');
 const request = store.getAll();
 const result = await request;
 console.log('Data saved to the database', result);
};
initdb();
```
(Above: This code imports the "openDB" function from the 'idb' library and initializes a database called 'jate' with a version of 1. It checks if the 'jate' object store already exists and creates it if it doesn't. The "putDb" function puts data into the 'jate' object store, while the "getDb" function retrieves all data from the same object store. The code initializes the database by calling the "initdb" function. )

<p>&nbsp;</p>

### Client Folder: webpack.config.js
```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const WebpackPwaManifest = require('webpack-pwa-manifest');
const { InjectManifest } = require('workbox-webpack-plugin');
const WorkboxPlugin = require('workbox-webpack-plugin');
const path = require('path');

module.exports = () => {
 return {
   mode: 'development',
   entry: {
     main: './src/js/index.js',
     install: './src/js/install.js'
   },
   output: {
     filename: '[name].bundle.js',
     path: path.resolve(__dirname, 'dist'),
   },
   plugins: [
     new HtmlWebpackPlugin({
       template: './index.html',
       title: 'Webpack Plugin',
     }),
     new InjectManifest({
       swSrc: './src-sw.js',
       swDest: 'src-sw.js',
     }),

     new WebpackPwaManifest({
       fingerprints: false,
       inject: true,
       name: 'Feather-Pad',
       short_name: 'Pad',
       description: 'Take notes with ease and on the go!',
       background_color: '#225ca3',
       theme_color: '#225ca3',
       start_url: './',
       publicPath: './',
       icons: [
         {
           src: path.resolve('src/images/feather-pad-icon.png'),
           sizes: [16, 96, 128, 192, 256, 384, 512],
           destination: path.join('assets', 'icons'),
         },
       ],
     }),
   ],
   module: {
     rules: [
       {
         test: /\.css$/i,
         use: ['style-loader', 'css-loader'],
       },
       {
         test: /\.m?js$/,
         exclude: /node_modules/,
         use: {
           loader: 'babel-loader',
           options: {
             presets: ['@babel/preset-env'],
             plugins: ['@babel/plugin-proposal-object-rest-spread', '@babel/transform-runtime'],
           }
         }
       }
      
     ],
   },
 };
 };
```
(Above: This code configures a webpack build for a development environment. It sets the entry points for two JavaScript files, 'index.js' and 'install.js', and specifies the output path for the bundled files. It uses several plugins, including HtmlWebpackPlugin for generating an HTML file, InjectManifest for injecting a service worker, and WebpackPwaManifest for generating a web app manifest. The generated manifest includes details such as the app's name, description, theme color, and icons. Additionally, the code defines module rules for handling CSS files and JavaScript files using Babel for transpiling and applying plugins such as '@babel/preset-env' and '@babel/plugin-proposal-object-rest-spread'.)

<p>&nbsp;</p>


### Client Folder: src-sw.js
```js
const { offlineFallback, warmStrategyCache } = require('workbox-recipes');
const { CacheFirst, StaleWhileRevalidate } = require('workbox-strategies');
const { registerRoute } = require('workbox-routing');
const { CacheableResponsePlugin } = require('workbox-cacheable-response');
const { ExpirationPlugin } = require('workbox-expiration');
const { precacheAndRoute } = require('workbox-precaching/precacheAndRoute');

precacheAndRoute(self.__WB_MANIFEST);

const pageCache = new CacheFirst({
 cacheName: 'page-cache',
 plugins: [
   new CacheableResponsePlugin({
     statuses: [0, 200],
   }),
   new ExpirationPlugin({
     maxAgeSeconds: 30 * 24 * 60 * 60,
   }),
 ],
});

warmStrategyCache({
 urls: ['/index.html', '/'],
 strategy: pageCache,
});

registerRoute(({ request }) => request.mode === 'navigate', pageCache);

registerRoute(
 ({ request }) => ['style', 'script', 'worker'].includes(request.destination),
 new StaleWhileRevalidate({
   cacheName: 'asset-cache',
   plugins: [
     new CacheableResponsePlugin({
       statuses: [0, 200],
     }),
   ],
 })
);
```
(Above: This code sets up caching strategies and registers routes using the Workbox library for service workers. It utilizes strategies like CacheFirst and StaleWhileRevalidate for different types of requests. It also configures plugins such as CacheableResponsePlugin and ExpirationPlugin to control caching behavior and expiration time. The code includes precaching and routing of assets based on the provided manifest file.)

<p>&nbsp;</p>


### Client Folder: install.js
```js
const butInstall = document.getElementById("buttonInstall");

window.addEventListener('beforeinstallprompt', (event) => {
   window.deferredPrompt = event;
   butInstall.classList.toggle('hidden', false);
 });

butInstall.addEventListener('click', async () => {
 const promptEvent = window.deferredPrompt;

 if (!promptEvent) {
  return;
 }
 promptEvent.prompt();
 window.deferredPrompt = null;
 butInstall.classList.toggle('hidden', true);
});

window.addEventListener('appinstalled', (event) => {
 window.deferredPrompt = null;
});
```
(Above: This code sets up an event listener for the "beforeinstallprompt" event, which is triggered when the browser prompts the user to install the web app. It stores the event object in the "deferredPrompt" variable and shows a hidden install button by removing the "hidden" class. When the install button is clicked, it prompts the user to install the app using the stored "deferredPrompt" event, then hides the install button. Finally, it listens for the "appinstalled" event to reset the "deferredPrompt" variable.)

<p>&nbsp;</p>


### Usage: 

 One of the core aspects of the implementation involves utilizing the IndexedDB database for storing and retrieving data. Feather Pad Text Editor is an incredibly useful application that offers a seamless and efficient experience for users looking for a powerful text editor. By leveraging IndeedDB, a robust database system, the application ensures reliable data storage and retrieval, providing a solid foundation for managing text-based content. The integration of JavaScript, Node.js, and Express.js allows for dynamic and responsive functionality, enabling users to create, edit, and save text documents effortlessly. With the power of webpack, the application bundles and optimizes its resources, resulting in faster load times and improved performance.The utilization of service workers and the InjectManifest approach in combination with Workbox enhances the offline capabilities of Feather Pad. Users can continue working on their text documents even without an internet connection, ensuring uninterrupted productivity.

Feather Pad's installable nature allows users to easily access the text editor as a standalone application, eliminating the need for a browser. This portability ensures convenience and availability across various devices and operating systems, empowering users to work on their text-based projects anytime, anywhere.

<p>&nbsp;</p>


## Credits

* Devtool (webpack): https://webpack.js.org/configuration/devtool/
* Mode (webpack): https://webpack.js.org/configuration/mode/
* Note Taking App Article: https://themeisle.com/blog/best-note-taking-apps/#gref
* Webpack Install: https://webpack.js.org/guides/getting-started/
* Asset Management (webpack): https://webpack.js.org/guides/asset-management/#loading-images
* HTML Webpack Plugin: https://webpack.js.org/plugins/html-webpack-plugin/
* Mini CSS Extract Plugin:https://webpack.js.org/plugins/mini-css-extract-plugin/#getting-started 
* Express: https://expressjs.com/en/starter/installing.html
* Concurrently: https://www.npmjs.com/package/concurrently
* Learn PWA: https://web.dev/learn/pwa/#interact_with_service_workers_in_the_browser
* API Reference Workbox: https://developer.chrome.com/docs/workbox/reference/
* Using a Bundler Workbox: https://developer.chrome.com/docs/workbox/the-ways-of-workbox/#using-a-bundler
* Inject Manifest Workbox: https://developer.chrome.com/docs/workbox/#injectmanifest_plugin
* IndexedDB NPM: https://www.npmjs.com/package/idb
* IndexedDB API: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
* PWA Manifest Webpack: https://www.npmjs.com/package/webpack-pwa-manifest 


<p>&nbsp;</p>


### License:
MIT License

Copyright (c) [2023] [Afi Nkhume-Crecy]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,


