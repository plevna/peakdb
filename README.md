[String]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[Number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
[Boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[Function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function

<div align="center">
  <img src="https://i.ibb.co/mbJC8yX/unknown.png" width="512px"/>
  <br/>
  <img src="https://badgen.net/npm/v/peak.db"/>
  <img src="https://badgen.net/npm/license/peak.db"/>
  <img src="https://badgen.net/npm/node/peak.db"/>
  <img src="https://badgen.net/npm/dt/peak.db"/>
</div>

## Contents

  * [About](#about)
  * [Features](#features)
  * [Latest Updates](#latest-updates)
  * [Installation](#installation)
  * [Documentation](#documentation)

## About

Fast and advanced, document based and key-value based NoSQL database that able to work as it is installed.

## Features

  * NoSQL database
  * Can be run as it is installed
  * Can be used document based and key-value based
  * Customizable settings for collections
  * No need to use schema
  * Quick data reading and writing
  * Data can be kept in cache
  * Easy to find data
  * Automatically or manual backup

## Latest Updates

### v2.1.0 → v2.2.0

>  * Updates for System:
>    * **`<CollectionOptions>.Indicate_Archived_At` added.** If this is active, will be automatically specified date when documents are archived.
>    * **`<CollectionOptions>.Indicate_Archived_Timestamp` added.** If this is active, will be automatically specified timestamp when documents are archived.
>    * **`<CollectionOptions>.Indicate_Unarchived_At` added.** If this is active, will be automatically specified date when documents are unarchived.
>    * **`<CollectionOptions>.Indicate_Unarchived_Timestamp` added.** If this is active, will be automatically specified timestamp when documents are unarchived.
>  * Updates for Document Based Collections:
>    * **`<Collection>.Archive()` added.** By archiving a document, you can have it ignored by the system.
>    * **`<Collection>.Unarchive()` added.** You can extract the archived document from the archive.
>  * Updates for Key-Value Based Collections:
>    * **`<Collection>.Find()` added.** You can find the data in the array.
>    * **`<Collection>.Filter()` added.** You can filter the data in the array.

[*... see all*](CHANGELOG.md#change-log)

## Installation

> ```sh-session
> npm install peak.db
> ```

## Documentation

### Constructor

`new Collection(options)`

Create a collection where you can manage and host your data.

> | Parameter | Default | Description |
> | --- | --- | --- |
> | options | | [Object]<br/>Collection options. |
> | options.name | | [String]<br/>Name of collection. |
> | options.type | | [String]<br/>[IMPORTANT] Type of the collection, which cannot be changed again later.<br/><br/>Valid values: `DOCUMENT_BASED`, `KEY_VALUE_BASED` |
> | options.id_length | `32` | [Number] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>This determines the length of unique identities given to documents. |
> | options.indicate_created_at | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the creation date of documents. |
> | options.indicate_created_timestamp | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the creation timestamp of documents. |
> | options.indicate_edited_at | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the edited date of documents. |
> | options.indicate_edited_timestamp | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the edited timestamp of documents. |
> | options.indicate_archived_at | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the archived at of documents. |
> | options.indicate_archived_timestamp | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the archived timestamp of documents. |
> | options.indicate_unarchived_at | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the unarchived at of documents. |
> | options.indicate_unarchived_timestamp | `false` | [Boolean] (optional) **[DOCUMENT BASED COLLECTIONS]**<br/>Whether to specify the unarchived timestamp of documents. |
> | options.save_timeout | `1` | [Number] (optional)<br/>This specifies how many seconds after a document is inserted, the collection will be saved. This way it limits the successive saving of the collection when many data are inserted in succession, so the system is not slowed down. Data loss may occur if the system is turned off after repeatedly entering data. When the document is added 5 times in a row, the collection is saved so that the data does not remain unsaved for a long time. This can be edited with the 'save_directly_after' option. |
> | options.save_directly_after | `5` | [Number] (optional)<br/>This specifies that after how many documents have been inserted, the collection will be saved without the save timeout. |
> | options.cache_retention_time | `10` | [Number] (optional)<br/>[If this value is `-1`, the cache is kept indefinitely] This indicates how much the cache will be held if the caching is enabled. If there is no activity in the collection, the cache is deleted, this prevents the loss of unnecessary RAM. |
> | options.backup_retention_time | `3` | [Number] (optional)<br/>[If this value is `-1`, backups will never be deleted] This determines after how many days the backups will be deleted. |
> | options.caching | `false` | [Boolean] (optional)<br/>[IMPORTANT] If this is active, the data is kept in the cache. In this case, the data is processed quickly, but the size of the collection is the loss of RAM. Is not preferred for large collections. |
> | options.auto_backup | `false` | [Boolean] (optional)<br/>If this is active, this collection will receive automatic backups. |
> | options.detailed_debugger_logs | `false` | [Boolean] (optional)<br/>If this is active, it will print more events in the collection to the console. |
> | options.activate_destroy_function | `false` | [Boolean] (optional)<br/>[IMPORTANT] If this is active, the `<Collection>.Destroy()` function becomes operable. This command serves to destroy your collection completely. It is a dangerous command. |
> 
> Example:
> ```js
> const example_collection = new PeakDB.Collection({
>   "name": "EXAMPLE_COLLECTION",
>   "type": "DOCUMENT_BASED",
>   
>   /*
>     For document based collections
>   */
>   "id_length": 32,
>   "indicate_created_at": false,
>   "indicate_created_timestamp": false,
>   "indicate_updated_at": false,
>   "indicate_updated_timestamp": false,
>   "indicate_archived_at": false,
>   "indicate_archived_timestamp": false,
>   "indicate_unarchived_at": false,
>   "indicate_unarchived_timestamp": false,
>   
>   /*
>     Can be used on all collection types
>   */
>   "save_timeout": 1,
>   "save_directly_after": 5,
>   "cache_retention_time": 10,
>   "backup_retention_time": 3,
>   "caching": false,
>   "auto_backup": false,
>   "detailed_debugger_logs": false,
>   "activate_destroy_function": false
> });
> ```

### Methods

**For Document Based Collections**

`insert(data)`

Insert a document.

> | Parameter | Description |
> | --- | --- |
> | data | [Object]<br/>The data to be written to the collection. |
> 
> returns [Object]
> 
> Example:
> ```js
> accounts.insert({"email": "fir4tozden@gmail.com", "username": "fir4tozden", "password": "12345678", "region": "Muğla"});
> /*
>   {
>     "_id": "RMmXZVDfQrVLQwFlquMPb98XNUCxQ6MM",
>     "_updated": false,
>     "_archived": false,
>     "_created_at": 2022-03-20T00:00:00.000Z,
>     "_created_timestamp": 1647745200000,
>     "email": "fir4tozden@gmail.com",
>     "username": "fir4tozden",
>     "password": "12345678",
>     "region": "Muğla"
>   }
> */
> ```

<br/>

`find(params, options)`

Find a document.

> | Parameter | Description |
> | --- | --- |
> | params | [Function] \| [Object]<br/>The parameters you will use to find the data. |
> | options | [Object] (optional)<br/>Find options. |
> | options.cares_archived | [Boolean] (optional)<br/>Whether to find archived documents. |
> 
> returns [Object]
> 
> Example:
> ```js
> accounts.find(document => document.email === "fir4tozden@gmail.com", {"cares_archived": true});
> // or
> accounts.find({"email": "fir4tozden@gmail.com"}, {"cares_archived": true});
> /*
>   {
>     "_id": "RMmXZVDfQrVLQwFlquMPb98XNUCxQ6MM",
>     "_updated": false,
>     "_archived": false,
>     "_created_at": 2022-03-20T00:00:00.000Z,
>     "_created_timestamp": 1647745200000,
>     "email": "fir4tozden@gmail.com",
>     "username": "fir4tozden",
>     "password": "12345678",
>     "region": "Muğla"
>   }
> */
> ```

<br/>

`filter(params, options)`

Filter documents.

> | Parameter | Description |
> | --- | --- |
> | params | [Function] \| [Object]<br/>The parameters you will use to filter the data. |
> | options | [Object] (optional)<br/>Filter options. |
> | options.cares_archived | [Boolean] (optional)<br/>Whether to filter archived documents. |
> 
> returns [Object]
> 
> Example:
> ```js
> accounts.filter(document => document.region === "Muğla", {"cares_archived": true});
> // or
> accounts.filter({"region": "Muğla"}, {"cares_archived": true});
> /*
>   [
>     {
>       "_id": "RMmXZVDfQrVLQwFlquMPb98XNUCxQ6MM",
>       "_updated": false,
>       "_archived": false,
>       "_created_at": 2022-03-20T00:00:00.000Z,
>       "_created_timestamp": 1647745200000,
>       "email": "fir4tozden@gmail.com",
>       "username": "fir4tozden",
>       "password": "12345678",
>       "region": "Muğla"
>     },
>     {
>       "_id": "23ERK9fHqiH_n83fhzU7eOYtzz6tUl7S",
>       "_updated": false,
>       "_archived": false,
>       "_created_at": 2022-03-20T00:05:00.000Z,
>       "_created_timestamp": 1647734700000,
>       "email": "nehir@gmail.com",
>       "username": "nehir",
>       "password": "12345678",
>       "region": "Muğla"
>     }
>   ]
> */
> ```

<br/>

`has(params)`

Check if they have document.

> | Parameter | Description |
> | --- | --- |
> | params | [Function] \| [Object]<br/>The parameters you will use to find the data. |
> 
> returns [Object]
> 
> Example:
> ```js
> accounts.filter(document => document.region === "Muğla");
> // or
> accounts.filter({"region": "Muğla"});
> /*
>   [
>     {
>       "_id": "RMmXZVDfQrVLQwFlquMPb98XNUCxQ6MM",
>       "_updated": false,
>       "_archived": false,
>       "_created_at": 2022-03-20T00:00:00.000Z,
>       "_created_timestamp": 1647745200000,
>       "email": "fir4tozden@gmail.com",
>       "username": "fir4tozden",
>       "password": "12345678",
>       "region": "Muğla"
>     },
>     {
>       "_id": "23ERK9fHqiH_n83fhzU7eOYtzz6tUl7S",
>       "_updated": false,
>       "_archived": false,
>       "_created_at": 2022-03-20T00:05:00.000Z,
>       "_created_timestamp": 1647734700000,
>       "email": "nehir@gmail.com",
>       "username": "nehir",
>       "password": "12345678",
>       "region": "Muğla"
>     }
>   ]
> */
> ```

<br/>

`update(document_id, data)`

Update a document.

> | Parameter | Description |
> | --- | --- |
> | document_id | [String]<br/>The ID of the document to be updated. |
> | data | [Object]<br/>Data to be updated in the document. |
> 
> returns [Object]
> 
> Example:
> ```js
> let document = accounts.find(document => document.email === "fir4tozden@gmail.com");
> accounts.update(document._id, {"email": "fir4tozden@gmail.com", "username": "hey_im_fir4tozden", "password": "87654321", "region": "İstanbul"});
> /*
>   {
>     "_id: "23ERK9fHqiH_n83fhzU7eOYtzz6tUl7S",
>     "_updated": true,
>     "_archived": false,
>     "_created_at": 2022-03-20T00:00:00.000Z,
>     "_created_timestamp": 1647745200000,
>     "_updated_at": 2022-03-20T00:10:00.000Z,
>     "_updated_timestamp": 1647735000000,
>     "email": "fir4tozden@gmail.com",
>     "username": "hey_im_fir4tozden",
>     "password": "87654321",
>     "region": "İstanbul"
>   }
> */
> ```

<br/>

`archive(document_id)`

Archive a document.

> | Parameter | Description |
> | --- | --- |
> | document_id | [String]<br/>The ID of the document to be archived. |
> 
> returns [Boolean]
> 
> Example:
> ```js
> let document = accounts.find(document => document.email === "fir4tozden@gmail.com");
> accounts.archive(document._id);
> // true
> ```

<br/>

`unarchive(document_id)`

Unarchive a document.

> | Parameter | Description |
> | --- | --- |
> | document_id | [String]<br/>The ID of the document to be archived. |
> 
> returns [Boolean]
> 
> Example:
> ```js
> let document = accounts.find(document => document.email === "fir4tozden@gmail.com", {"cares_archived": true});
> accounts.unarchive(document._id);
> // true
> ```

<br/>

`delete(document_id)`

Delete a document.

> | Parameter | Description |
> | --- | --- |
> | document_id | [String]<br/>The ID of the document to be deleted. |
> 
> returns [Boolean]
> 
> Example:
> ```js
> let document = accounts.find(document => document.email === "fir4tozden@gmail.com");
> accounts.delete(document._id);
> // true
> ```

**For Key-Value Based Collections**

`set(key, value)`

Set a value.

> | Parameter | Description |
> | --- | --- |
> | key | [String] | [Number]<br/>Key to value. |
> | value | [String] |
>
> returns [Boolean]
>
> Example:
> ```js
> let document = accounts.find(document => document.email === "fir4tozden@gmail.com");
> accounts.delete(document._id);
> // true
> ```


## License

[MIT](LICENSE.md)
