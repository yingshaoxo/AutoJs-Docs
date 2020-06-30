# Storages

> Stability: 2 - Stable

It's like a store. The store would be emptied only when you uninstall this app.

It support `number`, `boolean`, `string`.

For `Object` and `Array`, we use `JSON.stringify` to save it.

Data in storages can be shared across scripts.

## storages.create(name)
* `name` {string} the name of a new store

Create a new store.

Example:
```
var storage = storages.create("ABC");
storage.put("a", 123);
log("a = " + storage.get("a"));
```

The name should be unique to each other, like:
```
var storage = storages.create("2732014414@qq.com:ABC");
//or
var storage = storages.create("yingshaoxo@gmail.com:ABC");
```

## storages.remove(name)
* `name` {string} the name of a existed store

Delete a store.

# Storages

## Storage.get(key[, defaultValue])
* `key` {string}
* `defaultValue` {any}

Read a value from store by key.

## Storage.put(key, value)
* `key` {string}
* `value` {any}

Save a value to store by key.

if value == undefined, we raise TypeError.

## Storage.remove(key)
* `key` {string}

Remove a key from store.

## Storage.contains(key)
* `key` {string}

Check if the store has a key.

If so, return true, else return false.

## Storage.clear()

Clear the store.
