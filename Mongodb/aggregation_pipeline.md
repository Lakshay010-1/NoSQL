<!-- Aggregation Structure -->
db.<collection>.aggregate(
    [
        <!-- Stage 1 -->
        {
            { <operator> : <argument> }                                  <!-- single arguments -->
        },
        <!-- Stage 2 -->
        {
            { <operator> : [ <argument1>, <argument2> ... ] }            <!-- array of arguments -->
        },
        <!-- Stage 3 -->
        {
            { <operator> : <argument> }
        },
        <!-- Stage n -->
        <!-- ... -->
    ]
)

<!-- Stages -->

1.  $match                                  <!-- Filters documents based on query expressions. (Uses standard query operators) -->
                                            <!-- Example: { $match: { status: "active", age: { $gte: 18 } } }  -->

2.  $count                                  <!-- Counts documents in the pipeline. (Single output field name)  -->
                                            <!-- Example: { $count: "totalDocs" } -->

3.  $group                                  <!-- Groups documents and applies aggregate functions. (Must have _id (group key))  -->
                                            <!-- Example: { $group: { _id: "$category", total: { $sum: "$amount" } } } -->

4.  $sum                                    <!-- Returns the sum of numeric values. (In $group: {$sum: <expression>},
                                                                                     In other stages: {$sum: [<expr1>, <expr2>, ...]} to sum multiple expressions. 
                                                                                     Only numeric values are summed; non-numeric are ignored)  -->
                                            <!-- Example: { $group: { _id: "$category", total: { $sum: "$amount" } } } -->

5.  $avg                                    <!-- Returns the average of numeric values.	({$avg: <expression>} inside $group or $project,                                        Ignores non-numeric values. Returns null if no valid numbers)	  -->
                                            <!-- Example: { $group: { _id: "$category", avgPrice: { $avg: "$price" } } } -->

6.  $sort                                   <!-- Orders documents by specified fields. (Values must be 1 (asc) or -1 (desc))  -->
                                            <!-- Example: { $sort: { age: -1, name: 1 } } -->

7.  $limit                                  <!-- Limits documents passed on. (Positive integer)	  -->
                                            <!-- Example: { $limit: 10 } -->

8.  $unwind                                 <!-- Splits array elements into separate documents.	(Path required, optional preserveNullAndEmptyArrays)  -->
                                            <!-- Example: { $unwind: "$tags" } -->

9.  $addFields/ $set                        <!-- Adds or modifies fields. ({ $addFields: { newField: expression } })  -->    
                                            <!-- Example: { $addFields: { fullName: { $concat: ["$firstName", " ", "$lastName"] } } } -->    

10. $unset                                  <!-- Removes fields. (Field names array or single string)  -->
                                            <!-- Example: { $unset: ["password", "ssn"] } -->

11. $ifNull                                 <!-- Returns the first non-null expression; if all are null, returns last element as default. ({$ifNull: [<expression>, <replacementIfNull>]}). 
                                                Array must have exactly two elements.  -->
                                            <!-- Example: { $project: { displayName: { $ifNull: ["$name", "N/A"] } } } -->

12. $project                                <!-- Selects, excludes, or computes fields. (Include with 1 or exclude with 0)  -->    
                                            <!-- Example: { $project: { name: 1, age: 1, _id: 0 } } -->    

13. $push                                   <!-- Returns an array of values for each group.	(Used only inside $group: {$push: <expression>})	  -->
                                            <!-- Example: { $group: { _id: "$category", items: { $push: "$name" } } } -->

14. $all                                    <!-- selects documents where the array field contains all the elements specified in the query, in any order. ({ <arrayField>: { $all: [ <value1>, <value2>, ... ] } } )  -->
                                            <!-- Example: { $all: ["red", "blue"] } -->

15. $lookup                                 <!-- Joins data from another collection. (Needs from, localField, foreignField, as)  -->
                                            <!-- Example: { $lookup: { from: "orders", localField: "_id", foreignField: "custId", as: "ordersList" } } -->

16. $arrayElemAt                            <!-- Returns array element at specific zero-based index. ({$arrayElemAt: [<arrayExpression>, <index>]}, Negative index counts from end)  -->        
                                            <!-- Example: { $project: { firstItem: { $arrayElemAt: ["$items", 0] } } } -->        

17. $first                                  <!-- Returns first value from group or array. (In $group: {$first: <expression>} requires sorted pipeline if you want a specific first. In $project/$arrayElemAt context, works on arrays directly)	  -->
                                            <!-- Example: { $group: { _id: "$category", firstSale: { $first: "$date" } } } -->

18. $size                                   <!--Returns number of elements in array. Expression must resolve to an array; errors if not an array. ({$size: <arrayExpression>})	   -->
                                            <!-- Example:{ $project: { numTags: { $size: "$tags" } } } -->