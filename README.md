# Codd's Relational Model

## Background

Codd's relational model forms the basis of SQL databases and is one of the most commonly used data models.

In this model, a database is composed of relations. A relation can be thought of as a table, but to be more precise, it has a schema, which is a set of attributes, and an instance, which is a set of tuples corresponding to the attributes.  
For example, let <b><i>R</i></b> be

|<i>A</i>|<i>B</i>|
|---|---|
|1|2|
|3|4|

and let <b><i>S</i></b> be

|<i>B</i>|<i>C</i>|
|---|---|
|2|1|
|6|8|

The schema of <b><i>R</i></b> is <b>\{ A, B \}</b>, and the instance of <b><i>R</i></b> is <b>\{ (1,2), (3,4) \}</b>. The schema of <b><i>S</i></b> is <b>\{ B, C \}</b>, and the instance of <b><i>S</i></b> is <b>\{ (2,1), (6,8) \}</b>. Although the schema is a set, its order should be consistent with the tuples in the instance. If we change the order in the schema, we also have to change the order of the tuples in the instance. The following is another representation of <b><i>R</i></b>.

|<i>B</i>|<i>A</i>|
|---|---|
|2|1|
|4|3|

Since the set of tuples is a set, the order of the "rows" is not important, and there are no "duplicate rows".

## Operations

The relational algebra has the following operations:

1. Selection ( <b>&sigma;</b> )
2. Projection ( <b>&pi;</b> )
3. Rename ( <b>&rho;</b> )
4. Union ( <b>&cup;</b> )
5. Difference ( <b>&minus;</b> )
6. Cartesian product ( <b>&times;</b> )

The first three are unary operations (requiring one operand), and the others are binary operations (requiring two operands). Each operand is a relation, and the result of each operation is also a relation.

### 1. Selection ( &sigma; )

Selection picks tuples satisfying a condition. For example, <b><i>&sigma;<sub>A>1</sub>R</i></b> results in

|<i>A</i>|<i>B</i>|
|---|---|
|3|4|

### 2. Projection ( &pi; )

Projection picks attributes. For example, <b><i>&pi;<sub>A</sub>R</i></b> results in

|<i>A</i>|
|---|
|1|
|3|

### 3. Rename ( &rho; )

Rename changes the names of the attributes in the schema. For example, <b><i>&rho;<sub>C&rarr;A</sub>S</i></b> results in

|<i>B</i>|<i>A</i>|
|---|---|
|2|1|
|6|8|

### 4. Union ( &cup; )

Union gives tuples that are in any of its operands, but it requires that the schemata of the operands match. For example, <b><i>R</i> &cup; <i>S</i></b> is not allowed because the schema of <b><i>R </i>({ A, B \})</b> is different from that of <b><i>S </i>({ B, C \})</b>. However, we can apply rename to <b><i>S</i></b> and then apply union: <b><i>R &cup; (&rho;<sub>C&rarr;A</sub>S)</i></b> results in

|<i>A</i>|<i>B</i>|
|---|---|
|1|2|
|3|4|
|8|6|

### 5. Difference ( &minus; )

Difference gives tuples that are in the first operand but not in the second operand. As with union, it requires that the schemata of the operands match. For example, <b><i>R &minus; S</i></b> is not allowed because the schema of <b><i>R </i>({ A, B \})</b> is different from that of <b><i>S </i>({ B, C \})</b>. However, we can apply rename to <b><i>S</i></b> and then apply difference: <b><i>R &minus; (&rho;<sub>C&rarr;A</sub>S)</i></b> results in

|<i>A</i>|<i>B</i>|
|---|---|
|3|4|

### 6. Cartesian product ( &times; )

Cartesian product gives tuples resulting from concatenation of two tuples, one from each operand. If there are common attributes, the attribute is prefixed with the name of the relation it comes from followed by a dot. For example, <b><i>R &times; S</i></b> results in

|<i>A</i>|<i>R.B</i>|<i>S.B</i>|<i>C</i>|
|---|---|---|---|
|1|2|2|1|
|1|2|6|8|
|3|4|2|1|
|3|4|6|8|
