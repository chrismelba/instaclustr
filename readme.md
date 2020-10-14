#Instaclustr Technical interview

## 3. General Programming

Functional code and output can be found in the "fizzbuzz.ipynb" notebook. Code replicated here for ease of assessment. Code written in Python 3

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

## 7. Cloud Computing Theory

### A. What is the difference between container based virtualization and hypervisor based virtualization?
In a nutshell hypervisor virtualization will emulate a full OS, creating virtual hardware for it to run on. A container system will run on top of a single OS and run only the application, without the overhead of virtualising an OS. This makes containers much more efficient. A fully tuned container system should see 4 to 6 times as many server instances on the same hardware than a hypervisor VM [<sup>1</sup>](https://smartbear.com/blog/test-and-monitor/why-containers-instead-of-hypervisors/). The development of containers has lead to 'microservices'. Since each container contains only the binaries and libraries required, rather than an entire OS they can be extremely lightweight, allowing a traditional large app to be split into multiple microservices that all communicate with each other[<sup>2</sup>](https://www.cbtnuggets.com/blog/certifications/cloud/container-v-hypervisor-whats-the-difference).

### B. Explain the idea of Immutable Servers and discuss the pros and cons.
Immutable servers are, as they sound, servers that are never changed or updated. Instead of making a config change on a live server a new image is built and a new server stood up to enact the change. This allows for server testing before go-live[<sup>3</sup>](https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure), and ensures that there won't be errors during the upgrade process that mean our server is in a partial state, with some componants upgraded but some failed. Immutable servers do raise challenges in the deployment and testing process[<sup>4</sup>](https://techbeacon.com/enterprise-it/how-build-immutable-servers-fast). Since a new server image needs to be stood up in test, automated test run, then assuming the tests pass, it must be stood up again in production. This can be a time consuming process, particularly when the automated testing becomes heavy. It also requires that data be externalized, as in most instances it is no good to replace an immutable one with a new one that doesn't have any of the existing data.

### C. In Amazon Web Services, explain the difference between a Region, Availability Zone and Instance in relation to fault domains.

1. AWS Regions are distributed around the world and will have different latency depending where the region is being accessed from. Different regions also have different pricing structures and different services available.
2. AWS Availability Zones (AZ) are the building block that makes up the region. Each AZ is an isolated data centre, which allows servers running in a single region to have backups in other AZs[<sup>5</sup>](https://cloudacademy.com/blog/aws-regions-and-availability-zones-the-simplest-explanation-you-will-ever-find-around/)
3. Instance is a specific node of for example a cassandra cluster. This is the individual machine (or more likely VM or container) that the app is running in.

Fault domains are a way of understanding the redundancy in a server architecture built on AWS. A fault domain is a single point of failure, for example a fault domain at the AZ would fail if the entire AZ goes out, but not if one of it's constituant instances fails. If an application is running only on a single instance, then if that instance fails, either independantly or because of an AZ or Region failure, then the app itself will fail. By building nodes out across different AZs or even over different regions, higher resilliance and reliability can be achieved through redundancy.[<sup>6</sup>](https://lethain.com/fault-domains/)