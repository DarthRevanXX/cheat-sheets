A common method to distribute data as evenly as possible among service is simple hashing.

key hash has4 % amount of servers(when size is fixed)

	Consisten hashing = Object Keys + Server names

- With simpke hashing, when a new server is added, almost all the keys need to remapped
- With consistent hashing, adding a new server only requires redistribution of a fraction of the keys
- 
Uneven data distribution:
	Virtual node are used to fix this problem. The idea is to have each server appear at multiple location on the ring. Each location is a virtual node representing a server. 
	Having more virtual node means taking more space to store the metadata about the virtual nodes
