# Model Settings

The following properties can be specified at the top level of your model definition to override the defaults for that particular model.  To override the default settings shared by all of your models, edit [`config/models.js`](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md).






### `migrate`

```javascript
migrate: 'safe'
```

In short, this setting controls whether/how Sails will attempt to automatically rebuild the tables/collections/sets/etc. in your schema.

In a production environment (NODE_ENV==="production") Sails always uses
`migrate:"safe"` to protect inadvertent deletion of your data. However during development, you have a few other options for convenience:

 1. safe  - never auto-migrate my database(s). I will do it myself (by hand)
 2. alter - auto-migrate, but attempt to keep my existing data (experimental)
 3. drop  - wipe/drop ALL my data and rebuild models every time I lift Sails

When your sails app lifts, waterline validates your all of the data in your database.  This flag tells waterline what to do with data when the data is corrupt.  You can set this flag to `safe` which will ignore the corrupt data and continue to lift.  You can also set it to `


| Auto-Migration Strategy  | Description |
|-------------|----------------------------------------------|
|`safe`       | never auto-migrate my database(s). I will do it myself, by hand.
|`alter`      | auto-migrate columns/fields, but attempt to keep my existing data (experimental)
|`drop`       | wipe/drop ALL my data and rebuild models every time I lift Sails


> Note, by using `drop`, or even `alter`, you risk losing your data.  Be careful.  Never use `drop` or `alter` with a production dataset.



### `schema`

```javascript
schema: true
```

A flag to toggle schemaless or schema mode in databases that support schemaless data structures. If turned off, this will allow you to store arbitrary data in a record. If turned on, only attributes defined in the model's `attributes` object will be stored.

For adapters that don't require a schema, such as Mongo or Redis, the default setting is `schema:false`.



### `connection`

```javascript
connection: 'my-local-postgresql'
```

The configured database [connection](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.connections.html) where this model will fetch and save its data.  Defaults to `localDiskDb`, the default connection that uses the `sails-disk` adapter.


### `identity`

```javascript
identity: 'purchase'
```

The lowercase unique key for this model, e.g. `user`.  By default, a model's `identity` is inferred automatically by lowercasing its filename.  You should never change this property on your models.

### `globalId`

```javascript
globalId: 'Purchase'
```

This flag changes the global name by which you can access your model (if the globalization of models is enabled).  You should never change this property on your models- to disable globals, see [`sails.config.globals`]().



### autoPK

```javascript
autoPK: true
```

A flag to toggle the automatic definition of a primary key in your model. The details of this default PK vary between adapters (e.g. MySQL uses an auto-incrementing integer primary key, whereas MongoDB uses a randomized string UUID).  In any case, the primary keys generated by autoPK will be unique. If turned off no primary key will be created by default, and you will need to define one manually, e.g.:

```js
attributes: {
  sku: {
    type: 'string',
    primaryKey: true,
    unique: true
  }
}
```

### `autoCreatedAt`

```javascript
autoCreatedAt: true
```

A flag to toggle the automatic definition of a `createdAt` attribute in your model.  By default, `createdAt` is an attribute which will be automatically set when a record is created with the current timestamp, e.g.:

```js
attributes: {
  createdAt: {
    type: 'datetime',
    defaultsTo: function (){ return new Date(); }
  }
}
```

### `autoUpdatedAt`

```javascript
autoUpdatedAt: true
```
A flag to toggle the automatic definition of a `updatedAt` attribute in your model.  By default, `updatedAt` is an attribute which will be automatically set with the current timestamp every time a record is updated, e.g.:

```js
attributes: {
  updatedAt: {
    type: 'datetime',
    defaultsTo: function (){ return new Date(); }
  }
}
```


### tableName

```javascript
tableName: 'some_preexisting_table'
```

You can define a custom name for the physical collection in your adapter by adding a `tableName` attribute. __This isn't just for tables__.  In MySQL, PostrgreSQL, Oracle, etc. this setting refers to the name of the table, but in MongoDB or Redis, it refers to the colelction, and so forth. If no tableName is specified, Waterline will use the model's `identity` as its `tableName`.

This is particularly useful for working with pre-existing/legacy databases.

<!-- in WL2, this is `cid` (but is backwards-compatible) -->



### `attributes`

```js
attributes: {
  name: { type: 'string' },
  email: { type: 'email' },
  age: { type: 'integer' }
}
```

See [Attributes]().



<docmeta name="uniqueID" value="Modelconfiguration960213">
<docmeta name="displayName" value="Model Settings">
