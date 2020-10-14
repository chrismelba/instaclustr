Instaclustr Technical interview


## 5. SQL Programming
```
SELECT movies.title, movies.release_year, movies.genre, movies.director from movies
WHERE movies.genre = 'action';
#under the current database schema we could simply select * from movies, but this will continue to work if additional columns are added in the future


SELECT DISTINCT actors.name, actors.birth_year
FROM actors
LEFT JOIN movie_cast
ON actors.name=movie_cast.actor
LEFT JOIN movies
ON movie_cast.movie=movies.title
WHERE movies.director = 'Wes Anderson';
#This actually ends up being all the actors


SELECT movies.title, movies.release_year, movies.genre, movies.director
FROM movie_cast #
RIGHT JOIN movies
ON movie_cast.movie=movies.title
WHERE NOT movie_cast.actor = 'Bruce Willis' AND movie_cast.actor = 'Jeff Goldblum';
```