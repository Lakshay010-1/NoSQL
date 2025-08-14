
<!-- Update Document(s) -->

1. db.<collection_name>.updateOne(filter,update);                       <!-- Updates a single document within the collection based on the filter  -->
    <!-- example:
    db.users.updateOne( { name:"ABC" }, {$set: {fName:"A"} } );
    update document with name "ABC", update/add field fName with value "A"
    %set is used to update specific fields of a document.If the field exists, it updates its value. 
    If the field doesn’t exist, it adds it to the document. -->

2. db.<collection_name>.updateMany(filter,update);                      <!-- Updates all documents that match the specified filter for a collection  -->


<!-- Replace Document(s) -->

3. db.<collection_name>.repeatOne(filter, replacement);                 <!-- Replace the whole document structure  -->