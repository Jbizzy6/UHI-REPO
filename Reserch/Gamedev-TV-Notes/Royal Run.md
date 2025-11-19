
### game design
- dodge physics based objects on a procedurally generated level with the goal of lasting as long as possible with powerups and checkpoints

### what this section covers
- procedural generation
- rigid body physics
- physics materials
- handling collision
- animator transitions
- inspector attributes
- C# concepts such as Lists, inheritance, dependency injection, new keywords

### Level Generation using for loops

- level will progress around the player rather than the player progressing around the level
- we will generate it so that the level loads in chucks that move towards the player and once those chunks are past the player they will be destroyed
- we will achieve this using for loops
- for loops give us the opportunity to repeat a section of code a certain amount of times
- useful when we know exactly how many times we want to execute a block of code
```c# 
//for loop syntax
for (int i = 0; i < amount; i++)
{
	//do something
} 
```
-  we start by initialising `i` which is our integer - `int i = 0`
- we then have our condition, in this case we want to run the loop for as long as i is less than amount - `i < amount` we then increment i at the end of our loop and the loop runs again until i >= amount, e.g. if amount was = 10, we would run the loop 10 times

- we can child instantiated game objects to another game object by adding an override to the end of our instantiation line - `Instantiate(chunkPrefab, transform.position, quaternion.identity, chunkParent);`

### Lists vs Arrays
- both are considered collections
- an array has a fixed collection size while a list has a variable collection size
- the performance of an array is always fast while a list varies
- both are easy to use
- a list has a lot more flexibility than an array
- most of the time its easier to use a list instead of an array "when in doubt list it out"

the syntax for writing a list is as follows

```c#
//we start with 
List<>

//inside our angle brackets we state what type of list were trying to create `List<GameObject>;

//we then write the name of our list 
List<GameObject> chunks;

//we don't have to instantiable our list immediately however we cannot use a list until we do so, typically we instantiate our list in the same line we declare it - 
List<GameObject> chunks = new List<GameObject>;
```

instead of using `chunks.Length` like we would if we were using an array we can use `chunks.Count` which will count how many items are in the list and use only those items, if we used an array it will return all objects in the array even empty ones

```c#
void moveChunks()
    {
        for (int i = 0; i < chunks.Count; i++)
        {
            GameObject chunk = chunks[i];
            chunk.transform.Translate(-transform.forward * chunkMoveSpeed * Time.deltaTime);
            if (chunk.transform.position.z <= Camera.main.transform.position.z - chunkLength)
            {
                chunks.Remove(chunk);
                Destroy(chunk);
            }
        }
    }
}
```

this is the code we have written for moving our chunks backwards towards the player

the for loop runs the code for as long as there is chunks in the count
we cache each chunk as a game object reference 