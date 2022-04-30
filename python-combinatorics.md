# Combinatorics with python

Combinatorics can be defined as the **science of counting**. 

The goals of combinatorics are:

* the **enumeration** of specified structures, sometimes referred to as arrangements or configurations in a very general sense, associated with finite systems.

* the **existence** of such structures that satisfy certain given criteria.
* the **construction** of these structures, perhaps in many ways.
* the **optimization**: finding the "best" structure or solution among several possibilities, be it the "largest", "smallest" or satisfying some other optimality criterion.

Reference: [Combinatorics|Wikipedia](https://https://en.wikipedia.org/wiki/Combinatorics)

We will use the python language to explore this field of mathematics.

## The Basic Principle of Counting

First of all we have to import the module **itertools**:

```python 
import itertools as it
```

Then we create have two list of items:

```python 
tools = ["Hammer", "Toy","Bone"]
persons = ["Father","Baby","Dog"] 
```   

We want to assign one tool to one right person/pet. *Of course we know what is the right object for each* person but before doing that, we want to know all possible assignments. 

We use the **product()** method from itertools:

```python
assignments = list(it.product(tools,persons))
```
Results:

[('Hammer', 'Father'),  
 ('Hammer', 'Baby'),  
 ('Hammer', 'Dog'),  
 ('Toy', 'Father'),  
 ('Toy', 'Baby'),  
 ('Toy', 'Dog'),  
 ('Bone', 'Father'),  
 ('Bone', 'Baby'),  
 ('Bone', 'Dog')]

To know just how many assignments are possible without showing all possible assignments, we have just to count all elements in each list and then multiply them.

In python we use the len() function:

```python
n_assignments = len(tools) * len(persons)
```
and we get the right result: 9

We could als have used the len() function directly on our new assignment list to get the same result:
```python
n_assignments = len(assignments)
```


