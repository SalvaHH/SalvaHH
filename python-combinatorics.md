# Combinatorics with python

Combinatorics can be defined as the **science of counting**. 

The goals of combinatorics are:

* the **enumeration** of specified structures, sometimes referred to as arrangements or configurations in a very general sense, associated with finite systems.

* the **existence** of such structures that satisfy certain given criteria.
* the **construction** of these structures, perhaps in many ways.
* the **optimization**: finding the "best" structure or solution among several possibilities, be it the "largest", "smallest" or satisfying some other optimality criterion.

Reference: [Combinatorics|Wikipedia](https://https://en.wikipedia.org/wiki/Combinatorics)

We will use the python language to explore this field of mathematics.

# The Basic Principle of Counting

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
Result:

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
Result: 9

We could als have used the len() function directly on our new assignment list to get the same result:
```python
n_assignments = len(assignments)
```

Now that you know hoy to count assigments you want to try more difficult examples.

## 7-place licence plates

You want to know all possible assignments of 7-place license plates in which the first 2 places are occupied by letters and the last 5 by numbers:

The number of letters in english alphabet is 26. 

If you don't remember this number you can use the **ascii_lowercase** method from **string** module:

```python
import string
letters = string.ascii_lowercase
```
Result: 'abcdefghijklmnopqrstuvwxyz'

and then the **len(letters)** function to get 26.
 

```python
numbers = [1,2,3,4,5,6,7,8,9,0]
```

The possibile numbers are easier to calculate and are **len(numbers)=10**.

In this example you can't multiply 26 * 10 to arrive to the solution, but you have to think about all possible values each assignment in the license plate can get:

The first assigment and the second assignment are letters and have both 26 different values each. The last 5 numbers are numbers and have only 10 possible values each.

26 * 26 * 10 * 10 * 10 * 10 * 10 = 67.600.000 

The total of possible results is calculated as:

```python
import string
letters = string.ascii_lowercase
numbers = [1,2,3,4,5,6,7,8,9,0]

n_letters = len(letters)
n_numbers = len(numbers)

plate_letters = 2
plate_numbers = 5

n_assignments = n_letters**plate_letters * n_numbers**plate_numbers
```
Result: 67.600.000 possible assignments

In our first assigment the order of arrangements wasn't relevant:
*If the baby get the hammer, he can hurt himself and it doesn't matter if this happen before or after the dog get the bone or the father get the toy.* 

Sometimes the order of the assigments is really important! Imagine to run at the Olympics the 100m final.

# Permutations

Permutations represents all possible **ordered arrangements** in a list.

We will take as example the results of 100m Men Final in Tokyo 2020.
We have a list with 8 runners:

```python
runners = ["Enoch Adegoke","Zharnel Hughes","Fred Kerley","Marcell Jacobs","Ronnie Baker","Akani Simbine","Su Bingtian","Andre De Grasse"]
```
We want to know all possible arrangements of runner positions.

We use the **permutations()** function in the module itertools:

```python
all_possible_placements = list(it.permutations(runners))
```
We get a very long list with 40320 results:

[('Enoch Adegoke',  
  'Zharnel Hughes',  
  'Fred Kerley',  
  'Marcell Jacobs',  
  'Ronnie Baker',  
  'Akani Simbine',  
  'Su Bingtian',  
  'Andre De Grasse'),  

 ('Enoch Adegoke',  
  'Zharnel Hughes',  
  'Fred Kerley',  
  'Marcell Jacobs',  
  'Ronnie Baker',  
  'Akani Simbine',  
  'Andre De Grasse',  
  'Su Bingtian',  
   ...]

We can get the number of all possible permutions using like before:

```python 
n_possible_placements = len(all_possible_placements)
```
But we can use also use math to get the same result.

**Example:**   
Imagine just before the 100m Final begins, a journalist interviews each runner and ask in what position he wants to end the race to publish an hypothetical arrival order before the race start. 
 
The first runner to be interviewed is Enoch Adegoke and he says:"I want to  arrive 1st".   
Then is the turn of Akani Simbine and he also says:"1st! I'm sure!", but then the journalist says: "Wait, I cannot accept your answer as Enoch Adegoke took the 1st place", then Akani Simbine choose 2nd, Andre De Grasse 3rd etc.

We can imagine this problem as:   

Enoch Adegoke has 8 different choices, Akani Simbine has 7 different choices, Andre De Grasse has 6 different choices etc. till poor Ronnie Baker who cannot really choose and has to take the last possible option (maybe last place?).

If we want to get the number of all possible hypothetical placements of all runners we should multiply:

8 * 7 * 6 * 5 * 4 * 3 * 2 * 1

this number is **8!** or **eight factorial** and can be calculated in python with the function **factorial()** in math module:

```python 
import math
n_possible_placements = math.factorial(len(runners))
```

We get to the same result of 40320 possible arrangements.

## Only medals matter!

In our 100m Final we have considered all possible different position of 8 runners, but actually runners are mostly interested in getting a medal and really not so interested if they arrive 5th or 6th. 

So our goal is to discover the possible medal assignments instead of all possible race assignments.

The function **permutations()** give us the possibility to limit the assignments in this direction, adding in the second position the number of assignments we are looking for:

```python
all_possible_medals = list(it.permutations(runners,3))
```
Result:  
('Enoch Adegoke', 'Zharnel Hughes', 'Fred Kerley'),  
 ('Enoch Adegoke', 'Zharnel Hughes', 'Marcell Jacobs'),   
 ('Enoch Adegoke', 'Zharnel Hughes', 'Ronnie Baker'),  
 ('Enoch Adegoke', 'Zharnel Hughes', 'Akani Simbine'),  
 ('Enoch Adegoke', 'Zharnel Hughes', 'Su Bingtian'),  
 ('Enoch Adegoke', 'Zharnel Hughes', 'Andre De Grasse'),  
 ('Enoch Adegoke', 'Fred Kerley', 'Zharnel Hughes'),  
   ...]

We get in this case only 336 possible assignments.

## Put some PEPPER on it!

Let imagine that we want to get all possible permutations of the `string = "pepper"`.

If we use the **permutations()** function:
```python
string = "pepper"
pepper_perms = it.permutations(string)
```
Result: 720 

If we print the `list(pepper_perm)` we notice that this function doesn't consider that all *ps* are equal and give many duplicates.

One possible solutions to remove the duplicate is to transform our results in a **set**:

```python
pepper_perms = set(it.permutations(string))
```
We get only 60 results and no duplicate.

We can arrive to the same result with this math formula:

```python
string = "pepper"
ps = string.count("p")
es = string.count("e")

n_pepper_perms = math.factorial(len(string))/(math.factorial(ps)*math.factorial(es))
```
## All continental winners

For this task we are not interested in the winners of the race, but we want to have the permutations of the winners as they were running in continental leagues.

We create a dictionary with runners and continents:

```python
runners = {"Enoch Adegoke":"Africa",
           "Zharnel Hughes":"Europe",
           "Fred Kerley":"America",
           "Marcell Jacobs":"Europe",
           "Ronnie Baker":"America",
           "Akani Simbine":"Africa",
           "Su Bingtian":"Asia",
           "Andre De Grasse":"America"}
```
First we get the number of runners from each continent:

```python
from collections import Counter
continents = dict(Counter(list(runners.values())))
```
Result: {'Africa': 2, 'Europe': 2, 'America': 3, 'Asia': 1}

If we calculate only the continent of the runner, we can calculate with math the number of assignments:

```python
math.factorial(len(runners))/(
math.factorial(continents["Europe"])*math.factorial(continents["Asia"])*math.factorial(continents["America"])*math.factorial(continents["Africa"]))
```
Result 1680