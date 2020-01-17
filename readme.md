# Tiddlypouch plugin for tiddlywiki
This is the repository of the tiddlypouch plugin for tiddlywiki.
This plugin adds a layer between pouchdb and tiddlywiki to store tiddlers as documents on a pouchdb database.
This plugin is a key and core part of the NoteSelf project.

## Development
This repository uses gulp to bundle the code and make it ready for tiddlywiki usage.
Due to the special requirements of tiddlywiki the development process is a little bit special.
Normal code lives under the `src` folder, but we compile it to `dist` and tell tiddlywiki to look for it there using `TIDDLYWIKI_PLUGIN_PATH`. When live-reload is active every change on `src` file will trigger a rebundle to `dist` folder.
We also use `tw-pouchdb` **npm package** as a direct dependency.

To start the dev process just run `yarn start` or `npm start`.
This will start the development wiki (take a look at "A talo of two wikis" section for more details)

### Structure of the code
All the code is under the `src/plugins/danielo515/tiddlypouch` folder.
This is how the build system was created a long time ago and works, so it will not be changed soon.

### Life-cycle code
Life-cycle related code is under `../startup`.
Here you will find configuration startup, sync methods declarations and initializations, splash screen removal, event listeners such as delete
database and so on.
This is required because this is quite a low level plugin and needs to hook up into several tiddlywiki internals.

## A tale of two wikis
The most comfortable of writing tiddlers is inside tiddlywiki itself but because we are developing a sync adaptor, if we include the plugin
our changes are not saved to the file-system system. To solve this we use two wikis:
- One for writting documentation tiddlers
- One for developing and testing the plugin

### Documentation wiki
The folder `documentationwiki` is used for write documentation tiddlers.

### Development wiki
The folder `tiddlypouchwiki` contains the configuration for the wiki where we test the plugin functionality.
