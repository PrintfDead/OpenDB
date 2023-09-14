# @OpenDB

> Documentation: [OpenDB Docs](https://printfdead.github.io/opendb/index.html)

![Typescript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Node](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![NPM](https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm&logoColor=white)

## Information:
- :wrench: Efficient and fast database using BSON.
- :butterfly: Simple and easy to use
- :smile: Version 1.3

### ?? Installation
```sh
npm i @printfdead/open.db --save
```

## Why use OpenDB

### ?? Developer experience
> `OpenDB` offers a new, fast and secure experience for storing your data, using a simple structure.
> Given its speed, it allows you to save multiple data, it also allows you to have several databases in use at the same time, such as working with several containers on the same pointer.

### ?? Structure
<img height="300" src="assets/Structure.png" alt="OpenDB Structure">

### ? Flexibility & Scalability
> This database is flexible. 
> But it is not scalable since it is designed for fast, small/medium environments and where not much data needs to be saved since it is not scalable (Example: discord bots, web pages where not much data needs to be saved, bots in other applications, other environments that have these characteristics)

### ?? Cache
> It saves the data in a `Map` which makes it easier to search and use the database, making it much faster, making the time it takes to execute a method no more than **10ms**

### ?? Important Notes:
> **BSON Error: bson size must be >= 5, is 0** This is solved by deleting the `OpenDB` folder and restarting the app, it is because the containers and pointers were not saved correctly.

> The errors and/or warnings shown in this documentation are errors/warns that can occur when running `OpenDB`, they are only informative, a solution can be reached by reading the description of each error/warn.

### ?? Examples:
> `Create Database & Start Client Instance:`
```ts
import { Client } from '@printfdead/open.db';

/**
 * @param {object} options - Put database name and path
 * @new Client({ Path: string });
 * @description Instance new Client for create new database or use a database.
 */
const OpenDB = new Client({ Path: "path/to/root/folder" });

/** 
 * @param {string} event - Event name
 * @param {function} callback - Callback function
 * @description The event is emitted when the Client class is instantiated.
*/
OpenDB.on('start', () => {
  console.log("OpenDB start!");
});

/** 
 * @param {string} event- Event name
 * @param {function} callback - Callback error.
 * @type {error} ErrorClient interface
 * @description The event is emitted on some conditions of the Database class.
*/
OpenDB.on('error', (error) => {
  console.error(error);  
});

// Other conditions instantiate the Error clas and stop the database
```
#### Note:
- **Path:** must not start with dot (".", except two dots, EJ: "..") or slashes (/, \) or end in slash
---
> `Start`
```ts
/**
 * @description Create the root folder (database container)
 * @return Promise<this>
 */

await OpenDB.Start();
```
---
> `CreateDatabase`
```ts
/**
 * @param {string} Name - Database name
 * @description Create the database
 * @return Promise<this>
 */

await OpenDB.CreateDatabase("DatabaseName");
```
---
> `SetDatabase`
```ts
/**
 * @param {string} Name - Database name
 * @param {boolean} Force - (optional) Force change
 * @param {boolean} NotLoad - (optional) Don't preload pointers and containers, defaults to false.
 * @description Select the database
 * @return this
 */

OpenDB.SetDatabase("DatabaseName");
```
---
> `CreatePointer`
```ts
/**
 * @param {String | Number} Reference - A reference to search faster
 * @description Create Pointer
 * @return this
 */

await OpenDB.CreatePointer("PointerReference");
```
---
> `GetPointer`
```ts
/**
 * @param {String | Number} Reference - A reference to search faster
 * @description Get Pointer
 * @return BSON.Document | Undefined
 */

OpenDB.GetPointer("PointerReference");
```
---
> `GetContainer`
```ts
/**
 * @param {string} Container - Container ID
 * @description Get Container
 * @returns BSON.Document | Undefined
 */

OpenDB.GetContainer("ContainerID");
```
---
> `Push`
```ts
/**
 * @param {String | Number | Object | Array} Content - Content push
 * @param {String | Number} Reference - A reference to search faster
 * @param {String | Number} id (optional) - Table ID
 * @param {String} Container (optional) - Container ID
 * @generic {String | Number | Object | Array} T 
 * @description Get Pointer
 * @return Promise<this>
 */

await OpenDB.Push<string>("This content can be object, string, number and array", "Pointer Reference", 1, "Container ID");
```
---
> `AddContainer`
```ts
/**
 * @param {Reference} Reference - Reference to find the pointer easier
 * @param {string} Container (optional) - Container ID
 * @description Add an existing container or not, to a pointer
 * @returns Promise<void>
 */

await OpenDB.AddContainer("Pointer reference", "Container ID");
```
---
> `Edit`
```ts
/**
 * @param {Reference} Reference - Reference to find the pointer easier
 * @param {number | string | null} KeyName - Key name to search the container
 * @param {Push} KeyValue - Key value to search the container
 * @param {Push} Value - Value to define
 * @param {number} TableId (optional) - Table ID
 * @param {string} Container (optional) - Container ID
 * @description Edit a key in the container
 * @returns Promise<void>
 */

await OpenDB.Edit<string>("Pointer Reference", null, "Test1", "Test2", 1, "Container ID");
```
#### Note:
- **KeyName:** If your KeyName is not an object just put null.
---
> `Find`
```ts
/**
 * @param {(string|number)} Reference - Reference to find the pointer easier
 * @param {string | number | null} KeyName - Key name to search the container
 * @param {Push} KeyValue - Key value to search the container
 * @param {string} Container (optional) - Container ID
 * @description Search table by a key
 * @returns ContainerTable | undefined
 */

OpenDB.Find<string>("Pointer Reference", null, "Test1", "Container ID");
```
#### Note:
- **KeyName:** If your KeyName is not an object just put null.
---
> `Get`
```ts
/**
 * @param {(string|number)} Reference - Reference to find the pointer easier
 * @param {number} TableId - TableId ID
 * @param {string} Container (optional) - Container ID
 * @description Get table by a table id
 * @returns ContainerTable | undefined
 */

OpenDB.Get("Pointer Reference", 1, "Container ID");
```
---
> `DeleteTable`
```ts
/**
	* @param {Reference} Reference - Reference to find the pointer easier
	* @param {number} TableId - Table ID
	* @param {string} Container (optional) - Container ID
	* @description Delete Table
	* @returns Promise<void>
  */

await OpenDB.DeleteTable("Pointer Reference", 1, "Container ID");
```
---
> `DeleteTableByKey`
```ts
/** 
 * @param {Reference} Reference - Reference to find the pointer easier
 * @param {string | number | null} KeyName - Key name to search the container
 * @param {Push} KeyValue - Key value to search the container
 * @param {string} Container (optional) - Container ID
 * @description Delete Table by Key
 * @returns Promise<void>
 */

await OpenDB.DeleteTableByKey<string>("Pointer Reference", null, "Test1", "Container ID");
```
#### Note:
- **KeyName:** If your KeyName is not an object just put null.
---
> `DeleteKey`
```ts
/**
 * @param {Reference} Reference - Reference to find the pointer easier
 * @param {number | string | null} KeyName - Key name to search the container
 * @param {Push} KeyValue - Key value to search the container
 * @param {string} Container (optional) - Container ID
 * @description Delete Key
 * @returns Promise<void>
 */

await OpenDB.DeleteKey<string>("Pointer Reference", null, "Test1", "Container ID");
```
#### Note:
- **KeyName:** If your KeyName is not an object just put null.
---
> `Encrypt`
```ts
/**
 * @param {String | Number} Content - Content encrypt data
 * @param {number} Salt - (Optional) salt number
 * @description Encrypt string data
 * @output {key_encrypted: string, secret_key: string}
 */
const encryptData = OpenDB.Encrypt<string | number>("Content"); // Salt: number (optional)
```
---
> `Decrypt`
```ts
/** 
 * @param {DecryptOptions} options - Options decrypt data
 * @description Decrypt string
 * @output <Crypto-JS>.lib.CipherParams
 */
const decryptedData = OpenDB.decrypt({ EncryptKey: encryptData.key_encrypted.toString(), SecretKey: encryptData.secret_key});
```

#### :exclamation: Possible Errors:
- (ODB-01) **The path you specified was not found.** This error is due to the specified path not being found or misplaced.
- (ODB-02) **The database root folder not exists.** This error is due to the root folder (OpenDB/) not being found.
- (ODB-03) **This database does not exist, read https://github.com/PrintfDead/OpenDB#readme to know how to fix this error.** This error is because the database is not created.
- (ODB-04) **If force is not activated, the name of the database cannot be changed.** This is because the database name is already specified, and 'Force' must be set to true to be able to change it.
- (ODB-05) **Pointer not found.** This error is because the pointer not found.
- (ODB-06) **Container not found.** This error is because the container not found.
- (ODB-07) **The id is already in use.** This happens when the table id is already in use.
- (ODB-08) **Key not found.** This happens when the key was not found.
- (ODB-09) **This ID is not correct.** This error is because the container id is not correct.
- (ODB-99) **An error occurred and the path was not specified.** This error can occured because the path could not be defined automatically or for other internal reasons.

#### :interrobang: Possible Warns:
- (Warn-01) **The root folder already exists, nothing will be created and this function will be skipped.** This warn is because the root folder already exists, it will not affect the code but it will warn that it already exists, so you can delete the 'Start()' function from the code.
- (Warn-02) **The database already exists.** This is because the database already exists, it will not do anything, the function will be skipped.
- (Warn-03) **This can cause loading times to increase significantly.** it is because 'NotLoad' is true
- (Warn-04) **A pointer with this reference already exists, the pointer will not be created.** This is because the pointer with the same reference already exists, it will not give an error, the function will be skipped.

## See more
[![Discord](https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/ZdMqhEWhUN)
[![Documentation](https://img.shields.io/badge/Documentation-00386F?style=for-the-badge&logo=gitbook&logoColor=white)](https://printfdead.github.io/opendb)
