# Docker  

## Executing Docker Commands

```
docker run -u $(id -u):$(id -g) -v $(pwd):/data nextflow/rnaseq-nf:latest salmon -h

```   

interactive run:  
```
docker run -it -u $(id -u):$(id -g) -v $(pwd):/data nextflow/rnaseq-nf:latest 
```  



## Troubleshoot  

**Docker file remove error** : 
```
Error response from daemon: conflict: unable to delete e930629320ae (must be forced) - image is being used by stopped container  
```  

Solution:
The error "Error response from daemon: conflict: unable to delete e930629320ae (must be forced) - image is being used by stopped container" indicates that you are attempting to remove a Docker image (identified by ID e930629320ae) that is still referenced by one or more stopped containers. Docker prevents the deletion of an image if any container, even a stopped one, is still linked to it. 
To resolve this issue, the containers referencing the image must be removed first.  

**Identify the stopped containers using the image**:  
```
docker ps -a --filter "ancestor=e930629320ae" 
```  
The above command lists all containers including the stopped ones, that were created from the image id `e930629320ae`  , Then remove the stopped containers.  
``` 
docker rm <container_id_1> <container_id_2>  

or 

docker rm $(docker ps -a -q --filter "ancestor=e930629320ae")
```  

**remove the image**:
```
docker rmi e930629320ae
```  


