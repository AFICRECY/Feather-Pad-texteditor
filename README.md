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

Deployed Application Link: 

Note-taking apps have become an essential tool in today's society as they offer convenience, organization, and accessibility for individuals across various domains. Whether it's capturing important ideas, creating to-do lists, or recording meeting minutes, these apps provide a digital space for efficient note-taking, eliminating the need for traditional pen and paper. Moreover, their synchronization capabilities enable seamless access to notes across multiple devices, ensuring information is readily available whenever and wherever it is needed. My task was to build a text editor that can both run in a browser as well as have the ability to be installable as an app. This application should also be accessible on a user’s device without internet connection. I created the Feather pad text editor application considering the criteria of a progressive web app (PWA). The key focus of this project is to ensure a seamless user experience with access to a note taker application that can be installed on a user's device and usable even offline. To create Feather Pad, I brought together many different kinds of software, plugins, and packages. The Feather Pad app can become an indispensable tool for students, researchers, and professionals, offering them the ability to store, organize, and collaborate on notes and research projects. Note taking applications that do not rely on the internet  play a crucial role in enhancing productivity and facilitating efficient information management in various domains. This digital notebook serves as a modern counterpart to traditional paper notebooks, enabling users to conveniently organize their notes and information and auto save on the go. 


Screenshot of Functioning Web Application:

![App In Use](/client/src/images/Screenshot-of-app.png)


## Table of Contents:
* Installation (HTML, CSS, JavaScript, Node.js, NPM Packages, Webpack, PWA Paradigm, Functions, IndexedDB, Express.js, Heroku, Manifest.json, Service Workers)
* Usage
* Credits
* License


<p>&nbsp;</p>


### Installation:

To install this project, a knowledge of HTML, CSS, JavaScript, Node.js, and Express.js, the Progressive Web Application Paradigm (PWAs), IndexedDB, Git, and Heroku  were required.  I had to first install Node.js to my computer and then install the Express and NPM packages. I installed the following dependencies with my npm install (express, manifest.json, webpack plugins, babel, workbox plugins, and nodemon).The Express package allowed me to use the express framework in Node.js. In order to create this application. The Feather Pad test editor application is designed as a single-page application, meeting the criteria of a Progressive Web App (PWA). Furthermore, it  incorporates various data persistence techniques, and functions within the browser as well as an installable app using the manifest dependency package. Additionally, the Feather Pad text editor has offline functionality, allowing users to continue using it even without an internet connection thanks to my usage of IndexedDB. This application extends beyond note-taking, offering versatile functionality for journaling, team tasks, work projects, programming, planning, and more. With its user-friendly interface and intuitive design, it seamlessly caters to both individual and team-based projects, ensuring a great user experience. The code below make this happen: 

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





### htmlRoutes.js
```js
const path = require('path');

module.exports = (app) =>
 app.get('/', (req, res) =>
   res.sendFile(path.join(__dirname, '../client/dist/index.html'))
 );
```
(Above: This code exports a function that takes an "app" parameter and defines a route for the root URL ("/") using the GET method. When this route is accessed, it sends the index.html file located in the "../client/dist" directory as the response. The "path" module is used to construct the file path in a platform-independent way.)



### webpack.config.js
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


### src-sw.js
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



### server package.json
```json
 "scripts": {
   "dev": "webpack-dev-server",
   "build": "webpack --mode production",
   "start": "webpack --watch",
   "heroku-prebuild": "npm install --dev"
 },
```


### client install.js
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


### server index.js
```js
// Check if service workers are supported
if ('serviceWorker' in navigator) {
 // register workbox service worker
 const workboxSW = new Workbox('/src-sw.js');
 workboxSW.register();
} else {
 console.error('Service workers are not supported in this browser.');
}
```

### client database.js
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
