How to physically store the data

## Horizontal Partitioning

- Store rows of the same table in different machines
- example
	- store European users in one machine in Europe
	- store North American users in a machine in the US


### Horizontal Partitioning vs Sharding

????

## Vertical Partitioning

- store columns differently
- frequently used columns
	- in one partition on a fast expensive machine
- barely used columns
	- (possibly blob like profile pictures!) in a slower cheaper machine

### Vertical Partitioning vs Normalization

Partitioning is how to store the data

Normalization: logical

- remove repeated data
- have newly created tables reference/link with each other


