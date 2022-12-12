Counting sort is [[Sorting Algorithms|sorting algorithm]] simular to [[Bucket sort]] good for sorting collections where an element has a fixed number of possible values. 

Counting sort counts the frequencey of a value as it iterates over the input. Because the frequencey collection is already in order, to now create the sorted output we just need to move elements to output collection in order.

Lets say we want to alphabetically sort the text `A big bright bat bit a bug and a brown cat chased it`, we can create a frequency for each character, and increase that as we see that character.  
```
A: 5
B: 3
C: 2
D: 1
E: 3
F: 1
G: 1
H: 1
I: 2
J: 0
K: 0
L: 0
M: 0
N: 0
O: 0
P: 0
Q: 0
R: 0
S: 0
T: 4
U: 0
V: 0
```
Then we can turn this into a string by taking items out of the buckets left to right
```
aaaa
bbb
cc
d
eee
f
g
h
ii
tttt
```
becoming
```
aaaabbbccdeeefghiitttt
```

## Complexity
Counting sort uses O(n) time and space. n being whats larger, the input or the possible number of possible values.

## Issues
Notice in the above example how many characters where not used, the time and space is bottle necked by the number of possibilities, the more possibilities the data can be the more inefficent it is.

Imagine I wanted to sort the word 'cait' alphabetically. To sort this using Counting sort I would have to allocate 26 spaces in memory, one for each letter. When building the output, I would have to also iterate through these 26 spaces in memory as well, meaning I would do 26 operations just to build the output, storing unessusary data and doing unessusary work.

## Implimentation
```kt
fun sortPlayingCards(cards : IntArray)  {
    if(cards.any{ card -> card > 13 }) throw Exception("invalid card value")
    
    val frequency = IntArray(13) { 0 }
    cards.forEach { card ->
        frequency[card]++
    }
    var x = 0
    for(i in 0 until cards.size) {
        while(frequency[x] == 0) x++
        cards[i] = x
        frequency[x]--
    }
}
```
[Kotlin playground](https://pl.kotl.in/277jnN8g8?theme=darcula)