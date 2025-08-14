
<!-- Read Document(s) -->

1. db.<collection_name>.findOne();                                          <!-- Shows the first document  -->

2. db.<collection_name>.findOne(query);                                     <!-- Shows the first document which matches query  -->

3. db.<collection_name>.find();                                             <!-- Show all documents  -->

4. db.<collection_name>.find(query);                                        <!-- Specifies selection filter using query operators  -->
   <!-- example: db.users.find({name:"ABC"})
            db.users.find({income:{$gt:10}}) -->

5. db.<collection_name>.find(query,projection);                             <!-- "projection" Specifies the fields to return in the documents that  match the query filter -->
   <!-- example: db.users.find({name:"ABC"},{name:1})   -->