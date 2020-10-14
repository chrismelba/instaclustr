Instaclustr Technical interview

## 3. General Programming

Functional code and output can be found in the "fizzbuzz.ipynb" notebook. Code replicated here for ease of assessment

```
def fizzbuzz(*arg, length = 100):
    #A function to solve the classic Fizzbuzz problem in a flexible way for instaclustr technical interview
    #Inputs: unlimited tuples of divisor/replacement pairs, plus the length of the output (default 100)
    #Outputs: A heading detailing what our replacment keys are, followed by output to terminal of the solution to the problem.
    
    
    #Print the key pairs to console so that user can verify they're input in the correct order
    #TODO: Add error checking to ensure keypairs are input as tuples and that they are in the format [str, int]
    for pair in arg:
        print('replacing multiples of {} with {}'.format(pair[1], pair[0]))
    
    print('\n')
    
    #Main loop - python is single sided ranges, so need to add 1 to the length to get expected user result
    for i in range(1,length+1):
        
        #Initialize the output string to be blank
        output = ''
        
        #For each pair, if we are an exact multiple of the selected divisor, we add the given string to the output string
        for pair in arg:
            if i%pair[1] == 0:
                output += str(pair[0])
        
        #If the string is still blank after the previous step then we simply output the initial number
        if output == '':
            output = i
        
        #Print the output to console
        print(output)
        
fizzbuzz(['Insta', 3], ['clustr', 5])

```


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