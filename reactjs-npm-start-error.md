# Error
```
Starting the development server...

events.js:183
      throw er; // Unhandled 'error' event
      ^

Error: watch /home/li/lmppd/public ENOSPC
    at _errnoException (util.js:992:11)
    at FSWatcher.start (fs.js:1382:19)
    at Object.fs.watch (fs.js:1408:11)
    at createFsWatchInstance (/home/li/lmppd/node_modules/webpack-dev-server/node_modules/chokidar/lib/nodefs-handler.js:37:15)
    at setFsWatchListener (/home/li/lmppd/node_modules/webpack-dev-server/node_modules/chokidar/lib/nodefs-handler.js:80:15)
    at FSWatcher.NodeFsHandler._watchWithNodeFs (/home/li/lmppd/node_modules/webpack-dev-server/node_modules/chokidar/lib/nodefs-handler.js:228:14)
    at FSWatcher.NodeFsHandler._handleDir (/home/li/lmppd/node_modules/webpack-dev-server/node_modules/chokidar/lib/nodefs-handler.js:407:19)
    at FSWatcher.<anonymous> (/home/li/lmppd/node_modules/webpack-dev-server/node_modules/chokidar/lib/nodefs-handler.js:455:19)
    at FSWatcher.<anonymous> (/home/li/lmppd/node_modules/webpack-dev-server/node_modules/chokidar/lib/nodefs-handler.js:460:16)
    at FSReqWrap.oncomplete (fs.js:153:5)
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! lmppd@0.1.1 start: `react-scripts start`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the lmppd@0.1.1 start script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/li/.npm/_logs/2018-07-28T22_26_51_284Z-debug.log

```
# Solution
```
$ npm cache clear --force
$ rm -fr node_modules/
$ npm install

```
The issue was solved after I had closed Atom application or restarted my ubuntu. maybe caused by limited resources.

Increase the fs.inotify.max_user_watches to solve the issue
```
　　echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```
