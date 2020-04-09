# IndexedDB API

**IndexedDB** is a low-level API for client-side storage of significant amounts of structured data, including files/blobs. This API uses indexes to enable high-performance searches of this data. While Web Storage is useful for storing smaller amounts of data, it is less useful for storing larger amounts of structured data. **IndexedDB** provides a solution. This is the main landing page for MDN's **IndexedDB** coverage — here we provide links to the full API reference and usage guides, browser support details, and some explanation of key concepts.

**IndexedDB** is a transactional database system, like an SQL-based RDBMS. However, unlike SQL-based RDBMSes, which use fixed-column tables, **IndexedDB** is a JavaScript-based object-oriented database. **IndexedDB** lets you store and retrieve objects that are indexed with a key; any objects supported by the structured clone algorithm can be stored. You need to specify the database schema, open a connection to your database, and then retrieve and update data within a series of transactions.

Operations performed using IndexedDB are done asynchronously, so as not to block applications. IndexedDB originally included both synchronous and asynchronous APIs. The synchronous API was intended for use only with Web Workers but was removed from the spec because it was unclear whether it was needed.

## Main elements

### Database
Each origin has an associated set of databases. A database has zero or more **object stores** which hold the data stored in the database.

A database has a name which identifies it within a specific origin. The name is a name, and stays constant for the lifetime of the database.

A database has a version. When a database is first created, its version is 0 (zero).

### Connection
Script does not interact with databases directly. Instead, script has indirect access via a connection. A connection object can be used to manipulate the objects of that database. It is also the only way to obtain a transaction for that database.

The act of opening a database creates a connection. There may be multiple connections to a given database at any given time.

A connection can only access databases associated with the origin of the global scope from which the connection is opened.

### Object Store
An object store is the primary storage mechanism for storing data in a database.

Each database has a set of object stores. The set of object stores can be changed, but only using an upgrade transaction, i.e. in response to an upgradeneeded event. When a new database is created it doesn’t contain any object stores.

An object store has a list of records which hold the data stored in the object store. Each record consists of a key and a value. 

### Transactions
A Transaction is used to interact with the data in a database. Whenever data is read or written to the database it is done by using a transaction.

Transactions offer some protection from application and system failures. A transaction may be used to store multiple data records or to conditionally modify certain data records. A transaction represents an atomic and durable set of data access and data mutation operations.

All transactions are created through a connection, which is the transaction’s connection.

A transaction has a scope that determines the object stores with which the transaction may interact. A transaction’s scope remains fixed for the lifetime of that transaction.

A transaction has a mode that determines which types of interactions can be performed upon that transaction.

### Requests
Each asynchronous operation on a database is done using a request. Every request represents one operation.

### Cursor
A cursor is used to iterate over a range of records in an index or an object store in a specific direction.

### Key Generators
When a object store is created it can be specified to use a key generator. A key generator is used to generate keys for records inserted into an object store if not otherwise specified.

Inserting an item with an explicit key affects the key generator if, and only if, the key is numeric and higher than the last generated key.
```js
store = db.createObjectStore("store1", { autoIncrement: true });
store.put("a"); // Will get key 1
store.put("b", 3); // Will use key 3
store.put("c"); // Will get key 4
store.put("d", -10); // Will use key -10
store.put("e"); // Will get key 5
store.put("f", 6.00001); // Will use key 6.0001
store.put("g"); // Will get key 7
store.put("f", 8.9999); // Will use key 8.9999
store.put("g"); // Will get key 9
store.put("h", "foo"); // Will use key "foo"
store.put("i"); // Will get key 10
store.put("j", [1000]); // Will use key [1000]
store.put("k"); // Will get key 11
```

## Interfaces
To get access to a database, call open() on the indexedDB attribute of a window object. This method returns an IDBRequest object; asynchronous operations communicate to the calling application by firing events on IDBRequest objects.

### Connecting to a database
#### IDBEnvironment
Provides access to IndexedDB functionality. It is implemented by the window and worker objects. This interface isn't part of the 2.0 specification.
#### IDBFactory
Provides access to a database. This is the interface implemented by the global object indexedDB and is therefore the entry point for the API.
#### IDBOpenDBRequest
Represents a request to open a database.
#### IDBDatabase
Represents a connection to a database. It's the only way to get a transaction on the database.
Retrieving and modifying data
#### IDBTransaction
Represents a transaction. You create a transaction on a database, specify the scope (such as which object stores you want to access), and determine the kind of access (read only or readwrite) that you want.
#### IDBRequest
Generic interface that handles database requests and provides access to results.
#### IDBObjectStore
Represents an object store that allows access to a set of data in an IndexedDB database, looked up via primary key.
#### IDBIndex
Also allows access to a subset of data in an IndexedDB database, but uses an index to retrieve the record(s) rather than the primary key. This is sometimes faster than using IDBObjectStore.
#### IDBCursor
Iterates over object stores and indexes.
#### IDBCursorWithValue
Iterates over object stores and indexes and returns the cursor's current value.
#### IDBKeyRange
Defines a key range that can be used to retrieve data from a database in a certain range.
#### IDBLocaleAwareKeyRange 
Defines a key range that can be used to retrieve data from a database in a certain range, sorted according to the rules of the locale specified for a certain index (see createIndex()'s optionalParameters.). This interface isn't part of the 2.0 specification.
### Custom event interfaces
This specification fires events with the following custom interface:

#### IDBVersionChangeEvent
The IDBVersionChangeEvent interface indicates that the version of the database has changed, as the result of an IDBOpenDBRequest.onupgradeneeded event handler function.

## Examples

#### Open and creating the db

```js
var DBOpenRequest = window.indexedDB.open("toDoList", 4);

// these two event handlers act on the database being opened
// successfully, or not
DBOpenRequest.onerror = function(event) {
  console.log('Error loading database');
};
 
DBOpenRequest.onsuccess = function(event) {
  console.log('Database initialised.');
    
  // store the result of opening the database in the db
  // variable. This is used a lot later on, for opening
  // transactions and suchlike.
  db = DBOpenRequest.result;
};
```

#### Use a cursor to iterate through all the records in the object store

```js
function displayData() {
  var transaction = db.transaction(['delcaBooks'], "readonly");
  var objectStore = transaction.objectStore('delcaBooks');

  objectStore.openCursor().onsuccess = function(event) {
    var cursor = event.target.result;
    if(cursor) {
      console.log(`${cursor.value.bookTitle} , ${cursor.value.year}`); // logs bookTitle and year of each book in object store

      cursor.continue();
    } else {
      console.log('Entries all displayed.');
    }
  };
}
```

#### Create a todo list with IndexedDB

[<img width="428" alt="Captura de Pantalla 2020-04-10 a la(s) 10 00 07" src="https://user-images.githubusercontent.com/20034230/78944515-30687000-7b12-11ea-88fc-a9740abb2ec1.png">](http://jsfiddle.net/46hjmtq0/)