# Storage-JS

Storage-JS is a database menagement for localStorage. You can store data on local storage easily and APIs like Yii Framework AR.

## Install

Bower

```JavaScript
bower install storage-js --save
```

NPM

```JavaScript
npm install storage-js --save
```

or download [here](https://github.com/dida/storage-js/archive/master.zip)

```HTML
<script type="text/javascript" src="path/to/storage-js/storage.js"></script>
```

## Define

NodeJS

```JavaScript
var storagejs = require('storage-js');
```

RequireJS

```JavaScript
define([
    '/bower_components/storage-js/storage.js'
], function(storagejs) {
    // your code
});
```

or global variable name '*storagejs*'

## Callback
Callback Async

```JavaScript
storagejs('tableName').yourMethod(your_arguments, function(err, result) {
    // all method use this callback format (err, result)
    // for check error
    if (err === null) {
        // not error
    } else {
        console.log(err) // error message
    }
});
```
Callback Sync

* all method for Reading Record, return result data
* all method for Create, Update, Delete Record, return error message

```JavaScript
var result = storagejs('tableName').all();
console.log(result)

var error = storagejs('tableName').insert({_id: 1, name: 'Storage JS'});
if (error === null) {
    alert('success')
} else {
    alert(error);
}

```
## Quick Start
All method support Sync and Async. for example, this use Async method.

*table require id for primary key, default attribute name '_id'*

## Creating Record

* insert(id, object)
* insert(object)
* batchInsert(object)

Insert record

```JavaScript
var attr = {
    name: 'Dida Nurwanda',
    age: 23,
    city: 'Pandeglang'
}
storagejs('tableName').insert('dida', attr, function(err, result) {
    if (err === null) {
        // your code
    }
});
``` 
or

```JavaScript
var attr = {
    _id: 'dida',
    name: 'Dida Nurwanda',
    age: 23,
    city: 'Pandeglang'
}
storagejs('tableName').insert(attr, function(err, result) {
    if (err === null) {
        // your code
    }
});
``` 
Insert multiple record

```JavaScript
var attrs = [
    {
        _id: 'dida',
        name: 'Dida Nurwanda',
        age: 23,
        city: 'Pandeglang'
    },
    {
        _id: 'septi',
        name: 'Siwi Septi Hastuti',
        age: 11,
        city: 'Pandeglang'
    }
]
storagejs('tableName').batchInsert(attrs, function(err, result) {
    if (err === null) {
        // your code
    }
});
``` 


##  Reading Record

* all()
* findById(id)
* findIndexById(id)
* findByAttribute(key, value)
* findByAttributes(object)
* findAllByAttribute(key, value)
* findAllByAttributes(object)
* findAll(object)

Get all record

```JavaScript
storagejs('tableName').all(function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

Find record by ID

```JavaScript
storagejs('tableName').findById('dida', function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

Find the first row satisfying the specified condition

```JavaScript
storagejs('tableName').findByAttribute('_id', 'dida', function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

Find the row with the specified attribute values

```JavaScript
storagejs('tableName').findByAttributes({age: '23', city: 'Pandeglang'}, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

Find all rows satisfying the specified condition

```JavaScript
storagejs('tableName').findAllByAttribute('id', 'dida', function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

Find all row with the specified attribute values

```JavaScript
storagejs('tableName').findAllByAttributes({age: '23', city: 'Pandeglang'}, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

or

```JavaScript
storagejs('tableName').findAll({age: '23', city: 'Pandeglang'}, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

Find position index row by id

```JavaScript
storagejs('tableName').findIndexById('dida', function(err, result) {
    if (err === null) {
        console.log(result)
    }
});
```

## Limit and Offset
Limit and offset work on method :

* all()
* findAll()
* findAllByAttribute()
* findAllByAttributes()

to use it, limit or a limit and offset inserted after attribute condition.

```JavaScript
// limit only
storagejs('tableName').findAll({city: 'Pandeglang'}, 5, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});

storagejs('tableName').all(5, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});

// limit and offset
storagejs('tableName').findAll({city: 'Pandeglang'}, 5, 3, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});

storagejs('tableName').all(5, 3, function(err, result) {
    if (err === null) {
        console.log(result)
    }
});

```

## Update Record

* updateById(id, object)
* updateAllByAttributes(objectFinder, objectAttr)


Update the rows matching the specified condition

```JavaScript
var attr = {
    city: 'Serang'
}
storagejs('tableName').updateById('dida', attr, function(err, result) {
    if (err === null) {
        // your code
    }
});
```

Update all rows matching the specified condition

```JavaScript
var findAttr = {
    city: 'Pandeglang'
}
var newDataAttr = {
    city: 'Serang'
}

storagejs('tableName').updateAllByAttributes(findAttr, newDataAttr, function(err, result) {
    if (err === null) {
        // your code
    }
});
```

## Delete Record

* deleteById(id)
* deleteAllByAttribute(key, val)
* deleteAllByAttributes(object)
* deleteAll()

Delete the rows matchin ID 

```JavaScript
storagejs('tableName').deleteById('dida', function(err, result) {
    if (err === null) {
        // your code
    }
});
```
Delete all rows matching the specified condition

```JavaScript
storagejs('tableName').deleteAllByAttribute('city', 'Pandeglang', function(err, result) {
    if (err === null) {
        // your code
    }
});
```
Delete all row with the specified attribute values

```JavaScript
var attr = {
    city: 'Pandeglang'
}
storagejs('tableName').deleteAllByAttributes(attr, function(err, result) {
    if (err === null) {
        // your code
    }
});
```
Delete all record

```JavaScript
storagejs('tableName').deleteAll(function(err, result) {
    if (err === null) {
        // your code
    }
});
```

## Remove Table

```JavaScript
storagejs('tableName').remove(function(err, result) {
    if (err === null) {
        // your code
    }
});
```

## Contributor
* [Dida Nurwanda](http://www.dida.com)