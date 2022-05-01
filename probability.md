# Probability with Python

Probability is the branch of mathematics concerning numerical descriptions of how likely an event is to occur, or how likely it is that a proposition is true.

Reference: [Probability|Wikipedia](https://en.wikipedia.org/wiki/Probability)

To really understand Probability we need first to understand some key concepts as sample space and events.

### Sample space

The **sample space** is the set of all possible outcomes of an experiment.

```python
sex_newborn = ["girl","boy"]
```

for more complex sample spaces we use the combinatorics to get all possible results.

In a race beetween four cars the sample space is represented by all possible outcomes of ending positions:

```python
import itertools as it
cars = ["Ferrari","Lamborghini","Maserati","Porsche"]
sample_space = it.permutations(cars)
```
The sample space is:

[('Ferrari', 'Lamborghini', 'Maserati', 'Porsche'),   
 ('Ferrari', 'Lamborghini', 'Porsche', 'Maserati'),   
 ('Ferrari', 'Maserati', 'Lamborghini', 'Porsche'),   
 ('Ferrari', 'Maserati', 'Porsche', 'Lamborghini'),   
 ('Ferrari', 'Porsche', 'Lamborghini', 'Maserati'),   
 ('Ferrari', 'Porsche', 'Maserati', 'Lamborghini'),   
 ('Lamborghini', 'Ferrari', 'Maserati', 'Porsche'),   
 ('Lamborghini', 'Ferrari', 'Porsche', 'Maserati'),   
 ('Lamborghini', 'Maserati', 'Ferrari', 'Porsche'),   
 ('Lamborghini', 'Maserati', 'Porsche', 'Ferrari'),   
 ('Lamborghini', 'Porsche', 'Ferrari', 'Maserati'),   
 ('Lamborghini', 'Porsche', 'Maserati', 'Ferrari'),   
 ('Maserati', 'Ferrari', 'Lamborghini', 'Porsche'),   
 ('Maserati', 'Ferrari', 'Porsche', 'Lamborghini'),   
 ('Maserati', 'Lamborghini', 'Ferrari', 'Porsche'),   
 ('Maserati', 'Lamborghini', 'Porsche', 'Ferrari'),  
 ('Maserati', 'Porsche', 'Ferrari', 'Lamborghini'),  
 ('Maserati', 'Porsche', 'Lamborghini', 'Ferrari'),   
 ('Porsche', 'Ferrari', 'Lamborghini', 'Maserati'),   
 ('Porsche', 'Ferrari', 'Maserati', 'Lamborghini'),   
 ('Porsche', 'Lamborghini', 'Ferrari', 'Maserati'),  
 ('Porsche', 'Lamborghini', 'Maserati', 'Ferrari'),  
 ('Porsche', 'Maserati', 'Ferrari', 'Lamborghini'),  
 ('Porsche', 'Maserati', 'Lamborghini', 'Ferrari')]

 The outcome **sample_space[2]** ('Ferrari', 'Maserati', 'Lamborghini', 'Porsche') means that Ferrari arrived 1st, Maserati 2nd etc.

 ### Event
An event represents any subset of the sample space. Like **sample_space[2]**, but can also be **Porsche as first** and include more single elements in the sample space.

We can imagine the two events:
* Porsche first
* Maserati third

We can use logical operators **OR** and **AND** to get all possible occurrence of both events:

```python
porsche_first = []
for e in list(sample_space):
    if e[0] == "Porsche":
        porsche_first.append(e)
```

We get all possible events in sample space, in which Porsche arrives first:

[('Porsche', 'Ferrari', 'Lamborghini', 'Maserati'),   
 ('Porsche', 'Ferrari', 'Maserati', 'Lamborghini'),  
 ('Porsche', 'Lamborghini', 'Ferrari', 'Maserati'),  
 ('Porsche', 'Lamborghini', 'Maserati', 'Ferrari'),  
 ('Porsche', 'Maserati', 'Ferrari', 'Lamborghini'),  
 ('Porsche', 'Maserati', 'Lamborghini', 'Ferrari')]

 We can do the same to get maserati third:

 ```python
maserati_third = []
for e in list(sample_space):
    if e[2] == "Maserati":
        maserati_third .append(e)
```

[('Ferrari', 'Lamborghini', 'Maserati', 'Porsche'),   
 ('Ferrari', 'Porsche', 'Maserati', 'Lamborghini'),    
 ('Lamborghini', 'Ferrari', 'Maserati', 'Porsche'),  
 ('Lamborghini', 'Porsche', 'Maserati', 'Ferrari'),   
 ('Porsche', 'Ferrari', 'Maserati', 'Lamborghini'),  
 ('Porsche', 'Lamborghini', 'Maserati', 'Ferrari')]  

 We can use logical operators:

 This event will occurr if either Porsche arrives first OR Maserati arrives third.

 ```python
maserati_third_or_porsche_first = []
for e in list(sample_space):
    if e[2] == "Maserati" or e[0] == "Porsche":
        maserati_third_or_porsche_first.append(e)
```
[('Ferrari', 'Lamborghini', 'Maserati', 'Porsche'),   
 ('Ferrari', 'Porsche', 'Maserati', 'Lamborghini'),   
 ('Lamborghini', 'Ferrari', 'Maserati', 'Porsche'),   
 ('Lamborghini', 'Porsche', 'Maserati', 'Ferrari'),   
 ('Porsche', 'Ferrari', 'Lamborghini', 'Maserati'),   
 ('Porsche', 'Ferrari', 'Maserati', 'Lamborghini'),   
 ('Porsche', 'Lamborghini', 'Ferrari', 'Maserati'),   
 ('Porsche', 'Lamborghini', 'Maserati', 'Ferrari'),   
 ('Porsche', 'Maserati', 'Ferrari', 'Lamborghini'),  
 ('Porsche', 'Maserati', 'Lamborghini', 'Ferrari')]

 This other event will occur only if Porsche arrives first AND Maserati arrives third:
 ```python
 maserati_third_and_porsche_first = []
for e in list(sample_space):
    if e[2] == "Maserati" and e[0] == "Porsche":
        maserati_third_and_porsche_first.append(e)
```
[('Porsche', 'Ferrari', 'Maserati', 'Lamborghini'),   
 ('Porsche', 'Lamborghini', 'Maserati', 'Ferrari')]

 ## The three Axioms of Probability

* **Axiom 1:** The probability of an event is always beetween 0 and 1.

* **Axiom 2:** The probability of the sample space is always equal 1.

* **Axiom 3:** for any sequence of **mutually exclusive** events , the probability of at least one of them to occur is equal to the sum of all respective probabilities.

The first two axioms are really easy to understand. To explain the third axioms, we take a dice:

 ```python
sample_space = list(range(1,7))
```
[1, 2, 3, 4, 5, 6]

The probability to get in one throw 2 is equal:

 ```python
from fractions import Fraction
probability2 = str(Fraction(sample_space.count(2)/len(sample_space)).limit_denominator())
```
Result: "1/6"

*We imported the function **Fraction()** from fraction module to get 1/6 as result (we also converted it to a string). If we omit the **.limit_denominator()** method. We get a really weird fraction as result:* 

6004799503160661 / 36028797018963968  

*This is because 1/6 = 0.16666666666666666*

As dice results are mutually exclusive, if we want to know the probility of get 2 or 4 or 6 in a launch we can simply sum: 

1/6 + 1/6 + 1/6 = 3/6 = 1/2

We couldn't take our car race as example to explain the third axiom of probability, because the outcomes aren't mutually exclusive.

P(Porshe|first) = 1/4  
P(Maserati|third) = 1/4 

P(Maserati|third) + P(Porshe|first) <> 1/2 

But we watched in the OR example that is 5/12

## Simple proposition

As we know that:

P(sample_space) = 1

We can derive easily that the probability of an event happening is equal to:

P(event happening) = 1 - P(event not happening)

## More complex probabilities

### Team of five

We want to know what is the probability to get a committee of 5 person composed of 3 men and 2 women from our group of 6 men and 9 women.

 ```python
import itertools as it
men = ("Mark","John","Luis","Gordon","Andrew","George")
women = ("Martha","Aida","Isabel","Karen","Audrey","Abigail","Julia","Mia","Anne")
```
To solve this problem we want first to identify our sample space:
 ```python
sample_space = it.combinations(men + women,5)
```
 ('Mark', 'Audrey', 'Abigail', 'Julia', 'Clare'),   
 ('Mark', 'Audrey', 'Abigail', 'Julia', 'Anne'),   
 ('Mark', 'Audrey', 'Abigail', 'Clare', 'Anne'),  
 ('Mark', 'Audrey', 'Julia', 'Clare', 'Anne'),  
 ...]

We get a really long list of 3003 possible combinations.

Then we get the 20 possible men combinations:

 ```python
men_combinations = list(it.combinations(men,3))
```
and the 36 women combinations:

 ```python
women_combinations = list(it.combinations(women,2))
```
To get all list of possibile teams of 3 women und 2 men:
 ```python
good_teams = []
for man_comb in men_combinations:
    for woman_comb in women_combinations:
        good_teams.append(man_comb + woman_comb)
```
We get a list of possible 720 teams of 3 men and 2 women. We can again extract a random one:
 ```python
import numpy as np
good_teams[np.random.randint(720)]
```
Result:
('John', 'Luis', 'Andrew', 'Isabel', 'Anne')

If we want to know only the number of possible combinations we can use:
 ```python
import math
from fractions import Fraction

P_good_teams = str(Fraction(math.comb(6,3)*math.comb(9,2)/math.comb(15,5)).limit_denominator())
```
Result: 240/1001

### Married couples

In a group of 5 couples we want to know the probability to make a group of 3 people all unrelated.

We have to imagine this experiment like a different stages decisions:

```python
married_couples = [["Mary","John"],["Homer","Marge"],["Beauty","Beast"],["Abigail","George"],["Marco","Luisa"]]

all_persons = []
for couples in married_couples:
    for person in couples:
        all_persons.append(person)

# You can use in alternative a generator:
all_persons = [list(it.product(*t)) for t in it.combinations(married_couples, 3)]


sample_space = list(it.combinations(all_persons,3))
```
We get a list of 120 possibile results

[('Mary', 'John', 'Homer'),   
 ('Mary', 'John', 'Marge'),   
 ('Mary', 'John', 'Beauty'),   
 ('Mary', 'John', 'Beast'),   
 ('Mary', 'John', 'Abigail'),   
 ('Mary', 'John', 'George'),   
 ('Mary', 'John', 'Marco'),  
 ('Mary', 'John', 'Luisa'),   
...]

Now we want to exclude all possible combination that contains two persons from the same couple.

```python
correct_results = sample_space.copy()
for couple in married_couples:
    for res in sample_space:
        if couple[0] in res and couple[1] in res:
                if res in correct_results:
                    correct_results.remove(res)
```
Then we get all possible 80 results. 

Result: The probability is **80/120** 

In Stack Overflow I got a much quicker answer:
```python
import itertools as it

married_couples = [["Mary","John"],["Homer","Marge"],["Beauty","Beast"],["Abigail","George"],["Marco","Luisa"]]

result = [list(it.product(*t)) for t in it.combinations(married_couples, 3)]

```