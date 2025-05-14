- HashMap
- Stacks
- QuickSort
- MergeSort
- Graph
- Priority Queue
- Dynamic Lists

Hash Map
--
Similar to just an array but instead of doing myArray[index] = value,

it uses a hash function to convert the key in {key:value} to the actual index to find the correct value.
e.g. so for 
dictionary = {
	"name": Hanad;
	"lastName": Abdiazizali;
}
so if hash(name) = 1234, and the hash map is size 1000 then you can do 1234 % 1000 = 234 so in element 234, you can place the element.

for hash function, i'm tempted to just convert each character into an ascii value and just multiply it together, and then just add each character and do the sum for both. That should be good enough. And then modular against the list size.

so for hash map the structure should just an array of elements.

typedef Hashmap = {
	int array [1000]; 
}
