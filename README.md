# await-to-js

[![NPM version][npm-image]][npm-url]
[![Downloads][download-badge]][npm-url]

> Async await wrapper for easy error handling

## Install

```sh
npm i await-to-js --save
```

## Usage

```js
import to from "await-to-js"

import to from './to.js';

async function asyncTask(cb) {
     const [ user ] = await to(UserModel.findById(1));
     if(!user) return cb('No user found');

     const [ savedTask, err ] = await to(TaskModel({userId: user.id, name: 'Demo Task'}));
     if(err) return cb('Error occurred while saving task');

    if(user.notificationsEnabled) {
       const [ , err ] = await to(NotificationService.sendNotification(user.id, 'Task Created'));
        if(err) return cb('Error while sending notification');
    }

    if(savedTask.assignedUser.id !== user.id) {
       const [ notification, err ] = await to(NotificationService.sendNotification(savedTask.assignedUser.id, 'Task was created for you'));
       if(err) return cb('Error while sending notification');
    }

    cb(null, savedTask);
}
```

## License

MIT © [Dima Grossman](http://blog.grossman.io) && Tomer Barnea

[npm-url]: https://npmjs.org/package/await-to-js
[npm-image]: https://img.shields.io/npm/v/await-to-js.svg?style=flat-square

[travis-url]: https://travis-ci.org/scopsy/await-to-js
[travis-image]: https://img.shields.io/travis/scopsy/await-to-js.svg?style=flat-square

[coveralls-url]: https://coveralls.io/r/scopsy/await-to-js
[coveralls-image]: https://img.shields.io/coveralls/scopsy/await-to-js.svg?style=flat-square

[depstat-url]: https://david-dm.org/scopsy/await-to-js
[depstat-image]: https://david-dm.org/scopsy/await-to-js.svg?style=flat-square

[download-badge]: http://img.shields.io/npm/dm/await-to-js.svg?style=flat-square