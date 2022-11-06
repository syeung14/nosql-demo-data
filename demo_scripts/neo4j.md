```shell
// Hello World!
CREATE (database:Database {name:"Neo4j"})-[r:SAYS]->(message:Message {name:"Hello World!"}) RETURN database, message, r;
match (n) return n;

// create simple nodes
CREATE (p:Person)-[:LIKES]->(t:Technology);

CREATE (:student);

MATCH (s:student)
RETURN s;

match (st:student) 
where st.name = 'John' and st.birth_year = 1990
return st;

// update
MATCH (p:Person {name: 'Jennifer'})
SET p.birthdate = date('1980-01-01')
RETURN p;

MATCH (:Person {name: 'Jennifer'})-[rel:WORKS_FOR]-(:Company {name: 'Neo4j'})
SET rel.startYear = date({year: 2018})
RETURN rel;

MATCH (j:Person {name: 'Jennifer'})-[r:IS_FRIENDS_WITH]->(m:Person {name: 'Mark'})
DELETE r;

MATCH (m:Person {name: 'Mark'})
DELETE m;
```

```shell
show databases;
show users;
show current user;

## enterprise version only
create database student
```

### Capabilities of the Neo4j Graph Database with Real-life Examples
* https://rubygarage.org/blog/neo4j-database-guide-with-use-cases