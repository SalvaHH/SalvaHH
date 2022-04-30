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
numbers = string.digits 
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
## Continental leagues

For this task we are not interested in the winners of the race, but we want to have the permutations of the runners as they were running in continental leagues instead of olympics.

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
First we want to divide all runners by continent:

```python
from collections import defaultdict
runners_by_continent = defaultdict(list)
for key, val in sorted(runners.items()):
    runners_by_continent[val].append(key)
```
Result:    

 defaultdict(list,  
            {'Africa': ['Akani Simbine', 'Enoch Adegoke'],  
             'America': ['Andre De Grasse', 'Fred Kerley', 'Ronnie Baker'],  
             'Europe': ['Marcell Jacobs', 'Zharnel Hughes'],  
             'Asia': ['Su Bingtian']})  

Then we can find all assignments of different continental leagues:

```python
perm_by_continent = []
for key in runners_by_continent:
    perm_by_continent.append(list(it.permutations(runners_by_continent[key])    
```
Result:   

[[('Akani Simbine', 'Enoch Adegoke'), ('Enoch Adegoke', 'Akani Simbine')],   
 [('Andre De Grasse', 'Fred Kerley', 'Ronnie Baker'),   
  ('Andre De Grasse', 'Ronnie Baker', 'Fred Kerley'),   
  ('Fred Kerley', 'Andre De Grasse', 'Ronnie Baker'),   
  ('Fred Kerley', 'Ronnie Baker', 'Andre De Grasse'),   
  ('Ronnie Baker', 'Andre De Grasse', 'Fred Kerley'),   
  ('Ronnie Baker', 'Fred Kerley', 'Andre De Grasse')],   
 [('Marcell Jacobs', 'Zharnel Hughes'),   
  ('Zharnel Hughes', 'Marcell Jacobs')],   
 [('Su Bingtian',)]]

 Then we should make all possible assignments iterating all lists inside the list perm_by_continent :
 
 ```python
continent_perms = []
for african_runners in perm_by_continent[0]:
    for american_runners in perm_by_continent[1]:
        for european_runners in perm_by_continent[2]:
            for asian_runners in perm_by_continent[3]:
                continent_perms.append(african_runners + american_runners + european_runners + asian_runners)
```
Result:
we get all possible 24 different permutations from all continental leagues.

[('Akani Simbine',
  'Enoch Adegoke',
  'Andre De Grasse',
  'Fred Kerley',
  'Ronnie Baker',
  'Marcell Jacobs',
  'Zharnel Hughes',
  'Su Bingtian'),

 ('Akani Simbine',
  'Enoch Adegoke',
  'Andre De Grasse',
  'Fred Kerley',
  'Ronnie Baker',
  'Zharnel Hughes',
  'Marcell Jacobs',
  'Su Bingtian'),

 ('Akani Simbine',
  'Enoch Adegoke',
  'Andre De Grasse',
  'Ronnie Baker',
  'Fred Kerley',
  'Marcell Jacobs',
  'Zharnel Hughes',
  'Su Bingtian'),

 ('Akani Simbine',
  'Enoch Adegoke',
  'Andre De Grasse',
  'Ronnie Baker',
  'Fred Kerley',
  'Zharnel Hughes',
  'Marcell Jacobs',
  'Su Bingtian'),

 [...]

 We can calculate the number of possible permutations, just with simple math:
2! * 2! * 3! * 1! = 24

# Combinations

In combinations we are interested in determining the number of different groups of r objects that could be formed form a total of n objects.

We want to organize a 5 vs 5 football match and we want to know all possible teams.

```python
friends = ["John", "Mark", "Holly", "Benji", "Cristiano", "Leo", "Julian", "Robert", "Luis", "Dieter"]
```
if we want to know all possible combinations we can use the **combination()** function from module itertools:

```python
possible_teams = list(it.combinations(friends,5))
```
we get a list of 252 possible team combinations. 

If we want a randomizer we can pick-up a random team with **random.randint()** from numpy library.

```python
import numpy as np
random = np.random.randint(len(possible_teams))
team_one = possible_teams[random]
```
We can call this function everytime and try to get always different teams.

If we want to define also the opponent team we could delete from friend list all team_one players:

```python
for player in team_one:
    friends.remove(player)
team_two = friends
```
In our example we get teams:

Team One: ('Mark', 'Holly', 'Leo', 'Julian', 'Dieter')

Team Two: ['John', 'Benji', 'Cristiano', 'Robert', 'Luis']

We can get the number of possible combinations also with math:

```python
import math
player_each_team = 5
n_friends = 10
n_possible_teams = math.factorial(n_friends)/(math.factorial(n_friends-player_each_team)*math.factorial(player_each_team))
```
Now imagine that this football match was boring and we want to organise more balanced teams dividing our friends in good players and bad players:

```python
good_players = ["Holly","Benjy","Leo","Cristiano"]
bad_players = ["Mark","Julian","Dieter","John","Luis","Robert"]
```
We want to be sure that each team contain at least 2 good player and 3 bad players.

```python
good_players = ["Holly","Benjy","Leo","Cristiano"]
bad_players = ["Mark","Julian","Dieter","John","Luis","Robert"]
```
We iterate inside the two lists of friends and we get all possible balanced teams with two good players and three bad players:
```python
good_players_perms = list(it.combinations(good_players,2))
bad_players_perms = list(it.combinations(bad_players,3))
balanced_teams = []
for good_players in good_players_perms:
    for bad_players in bad_players_perms:
                  balanced_teams.append(good_players + bad_players)     
print(balanced_teams)             
```
We get a list of 120 possible balanced teams.

If we are not interested in the team composition but we want only to know the number of possible combinations, we can use Factorial calculations to get the possible teams:

```python
good_players_each_team = 2
good_players = 4

n_possible_good_players = math.factorial(good_players)/(math.factorial(good_players-good_players_each_team)*math.factorial(good_players_each_team))

bad_players_each_team = 3
bad_players = 6

n_possible_bad_players = 
math.factorial(bad_players)/(math.factorial(bad_players-bad_players_each_team)*math.factorial(bad_players_each_team))

n_possible_bad_players*n_possible_good_players         
```
We get the total of 120 different possible balanced teams.
