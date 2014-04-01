ocdp-adapters
=============

This is a document explaining how to develop an adapter for importing a bespoke file format into the OCDP system.

Introduction
---

OCDP has a plug-in architecture that allows custom file formats to be imported into the data store.

Files are imported from disk and stored in the given mongodb collection.

OCDP adapter interface
---

The OCDP adapter interface is pretty straightforward. Adapter modules must expose a single API:

```sh
/*
 @collection - an empty mongodb collection into which the file data is stored.
 @filePath - the path to the file to be imported.
 @callback - a function that is called once the import is complete (see below).
*/
import(collection, filePath, callback) {
    // Import document into collection and then callback.
    callback(err, header);
}

/*
 @err - error object, null if no error occurred.
 @metadata - the importer can optionally return metadata describing the fields present in the newly imported dataset. The format should be an array of field objects:
 metadata = [
        {
            name: "first name",
            description: "customer's first name",
            type: "string"
        },
        {
            name: "last name",
            description: "customer's last name",
            type: "string"
        }
    ]    
*/
importComplete(err, metadata) {
    if (err === null) {
        // No error occurred.        
    } else {
        // Handle error.
    }
}
```

Related
---

For details of existing OCDP adapters, see [ocdp CSV adapter] and [ocdp XLS adapter].

[ocdp CSV adapter]:http://github.com/TobyEalden/ocdp-fileImporter-csv
[ocdp XLS adapter]:http://github.com/TobyEalden/ocdp-fileImporter-xls

