##
```shell
$ CREATE KEYSPACE essentials with replication = {'class': 'SimpleStrategy', 'replication_factor':1};

$ CREATE TABLE movies_by_actor (
  actor TEXT,
  release_year INT,
  movie_id UUID,
  title TEXT,
  genres SET<TEXT>,
  rating FLOAT,
  PRIMARY KEY ((actor), release_year, movie_id)
) WITH CLUSTERING ORDER BY (release_year DESC, movie_id ASC);

actor : partition key (in parenthesis)
  - a group of rows with common partition key
Other columns in the primary key fields are cluster key
  - provide ordering 
  - enable range querying
Only the columns in the primary key can be appear in the where clauses.

$ insert into movies_by_actor (actor, release_year, movie_id, title, genres, rating) values
  ('Brad Pitt', 2011, uuid(), 'Tree of Life', {'drama'}, 10);

$ insert into movies_by_actor (actor, release_year, movie_id, title, genres, rating) values
  ('Emma Stone', 2016, uuid(), 'La La Land', {'musical', 'drama'}, 10);

$ insert into movies_by_actor (actor, release_year, movie_id, title, genres, rating) values
  ('Michael Keaton', 2014, uuid(), 'Birdman', {'drama'}, 9);
```

### more examples
#### https://gist.github.com/jeffreyscarpenter/761ddcd1c125dfb194dc02d753d31733
 
