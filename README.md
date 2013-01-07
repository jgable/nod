Nod
=====

Fast, generic, simple access control system for node.js.

## Installation

	$ npm install nod

## Quick start

nod is used by consuming applications to manage a map of permissions that let you later check or enforce that certain subjects have permissions on specific objects.
It does not try and enforce a particular storage paradigm on your application, nor does it presume anything about the hierarchy of your stuff.  You simply grant, revoke, check, or enforce as appropriate.

#grant#
_grant(subjectId, resourceId, permission)_
```js
var nod = require('nod');

// assuming some object named article
nod.grant('peter', article.id, 'read');
```

#check or enforce#

At this point, nod's permissions map will record that the subject identified as 'peter' will have the permission to 'read' the article.
Note that all the parameters are pretty arbitrary; nod attaches no semantic meaning to your permission names, nor does it assume any kind of inheritance in this release.
You can, however, check peter's rights as follows:

```javascript
nod.check('peter', article.id, 'read'); // returns true
nod.check('peter', article.id, 'write'); // returns false
nod.enforce('peter', article.id', write'); // throws an AccessDeniedError
```

#revoke#

If you later change your mind, you can always `revoke` permissions as well

```javascript
nod.revoke('peter', article.id, 'read');
```

#getPermissions#

You can also view a copy of the permissions map through `getPermissions`

```javascript
nod.grant('peter', '102029192', 'read');
nod.getPermissions();
// returns { '102029192' : { read : ['peter'] }}
```

#setPermissions

And finally, you can set permissions as well

```javascript
nod.setPermissions({'102029192' : {read : ['peter','stewie']}});
nod.check('stewie', '102029192', 'read'); // returns true
```
