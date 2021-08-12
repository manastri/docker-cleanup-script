#Docker Cleanup script:
================================================================================

1. Delete docker Images with "<none>" as a tag name.
	- Command : ```docker rmi -f $(docker images | grep -w "<none>" | awk {print $3})```

2. Delete "Dead" or "Exited" containers.
	- Command : ```docker rm $(docker ps -a | grep "Dead\|Exited" | awk '{print $1}')```

3. Delete dangling docker images.
	- Command : ``docker rmi -f $(docker images -qf dangling=true)```

4. Deletion of old images which are more than two months old
	- Command : ```docker rmi -f $(docker images | awk '{print $3,$4,$5}' | grep '[9]\{1\}\ weeks\|years\|months' | awk '{print $1}')```
	
5. Delete or clean up unused docker volumes. 
	- Command : ```docker volume rm -f $(docker volume ls -qf dangling=true)```
