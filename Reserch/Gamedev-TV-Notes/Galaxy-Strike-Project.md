what does this project aim to create
- this section of the course aims to build a tactical rail shooter similar to games like Starfox

what is covered in this section
- terrain tools
- Timeline
- Audio
- Input action map
- Camera Stacking
- Vector arithmetic
- Particle collision
- Prefab variants
- C# - clamp, lerp, arrays, loops

terrain game object
- terrain can be added simply as a game object
- tools are built in for raising, lowering, texturing etc
- additional terrain packages exist and can be downloaded from the asset store

Textures - Height Map & Normal Map
- Height map: uses white to black grey scale to show height in a texture
- Normal map: uses RGB values to indicate X, Y, Z, facing directions

Timeliness
- a timeline is composed of key frames, the timeline then animates the moments between these key frames

![[Rail_Shooter_Path.png]]
for the sake of reminding myself the path I want to animate I created a little diagram outlining said path with my terrain as a reference

### unity action map

- each input action assets allows you to create as many actions maps as you want (an action map being a way of mapping actions to a controller or keyboard)
- it makes it easier to map actions for multiple different controllers
- actions can have different action types those being, value, button, and passthrough and can have a range of different control types. for the purposes of this course we want to return an action type of a value and a control type of a vector 2 (we want a vector 2 instead of a vector 3 because we don't want to move forward and backwards because our animation is controlling our forward and backwards movement meaning a vector 2 is sufficient because it will allow for only left and right inputs)
- in our inspector we can add a player input component to the object we want to move our ship with and add our controls
- there are numerous different ways to interact with the behaviour of the input however for our case we want to have our behaviour set to "Send Messages" to simply send and receive messages and inputs from our scripts (Send Messages will only work with scripts that are attached to the same game objects that the player input component is attached too)
- the Send Messages behaviour will automatically create functions connected to our action maps, for example, if we have an action map called "move" the send messages behaviour will create a function called "OnMove" so we can interact with that action map directly
- in order to use the input system in our code we need to import its namespace "UnityEngine.InputSystem"
- we can then access the method the input system created for us however the method has to be PUBLIC
- we then access our input value as a parameter of OnMove

during this task I was having a problem printing the vector 2 values to the console, upon diving into the comments of this lecture I found a post by user "Slime" who stated that using the Player Input component was actually slower than accessing the input Actions directly in the script itself because "it relies on Unity's legacy message-passing system instead of a direct method call, leading to extra overhead and unnecessary allocations"  the user attached some code showing their solution 
```
using UnityEngine; 
using UnityEngine.InputSystem; 
public class PlayerMovement : MonoBehaviour { 
[SerializeField] InputActionAsset inputActions; 

private InputActionMap playerMap; 
private InputAction moveAction; 

void Awake() { 
playerMap = inputActions.FindActionMap("Player"); 
playerMap.Enable(); 

moveAction = playerMap["Move"]; 
} 

void Update() { 
print( moveAction.ReadValue<Vector2>() ); 
} 
}
```
using this code solved the problem which leads me to believe that this is a faster and better solution so as such I will attempt similar solutions in my future code.

### Mathf.Clamp

unity function we can use to ensure our ship does not move off screen

takes in three parameters - value, min, max - more simply it takes in the value we want to restrict and the min and the max values, as long as our value falls outside of the min and max values itll be restricted to that range

### rotations, quaternions, and lerping

- quaternions on a deep level are extremally complex however we can basically understand them as a way of encoding rotations
- x, y, z, directly corollate to pitch, yaw, and roll
- the order in which we manage our rotations matter as rotations are interlinked
- "Lerp" has a range of use cases like colours and mathf, but for our purposes we want to use it to more visually represent the roll of our ship instead of just watching our ship snap back and forth
- lerp requires a starting point, an end point, and a time frame to complete the lerp over


### Particle system
- composed of different modules that can all be modified to create unique particles 

### C# arrays and foreach loops
- arrays allow us to store multiple objects in one variable
- we can only store the same type of objects in the array variable

- a foreach loop is a control flow statement for traversing a collection
- its a way of saying "do this to everything in our collection"

how to iterate over a collection
```
GameObject[] things;

foreach (Gamobject item in things) {
	item.doSomething();
	//etc
} 
```

### Vector Arithmetic
- vector subtraction is most often used to get the direction and distance from one object to another
- one of the most common things we must do in game dev is calculate a distance between two vectors, this could be used for aiming at targets etc
- to do this we take our starting position(point A) and our ending position(Point B) and subtract point A from point B to give us a new vector3 that we can use to get the direction and distance were looking for
- unity has several built in methods to help with this such as Quaternion, dot look, direction or vector three dot distance

``` C#
void aimLasers()
    {
        foreach (GameObject laser in lasers)
        {
//Step 1: subtract laser position from target position to return a vector between both points
Vector3 firDirection = targetPoint.position - laser.transform.position;
            
//Step 2: use Quaternion.LookRotation to calulate a rotation for each laser to align it to the new vector 3 we calculated
Quaternion rotationToTarget = Quaternion.LookRotation(firDirection);
            
//Step 3: move the lasers rotation towards the Quaternion we calulated
laser.transform.rotation = rotationToTarget;
        }
    }
}
```

(I didn't take not of this however in earlier lectures we created a new game object called Target Point to act as our link to the world that the lasers should be tracking towards)

### Collison and Triggers
![[Collision_Cheat_Sheet.png]]

### Instantiation at runtime

- used to instantiate a game object while the game is running, in our example we will be using it to instantiate a particle system whenever ourselves or an enemy is destroyed
- we can declare the instantiate method in multiple ways in unity, this is what's known as method overloading
- https://docs.unity3d.com/ScriptReference/Object.Instantiate.html
- the method we will use is this one "public static Object Instantiate([Object](https://docs.unity3d.com/ScriptReference/Object.html) original, [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html) position, [Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html) rotation);"
- a shortcut we can use when it comes to rotations is if we don't care about the specific rotation of an object were instantiating then we can write "Quaternion.identity" as a shorthand for 0, 0, 0


### SOLID programming principles
- S - Single Responsibility
- O - Open/Closed
- L - Liskov Substitution (need more research)
- I - Interface Segregation (need more research)
- D - Dependency Inversion (need more research)

### Public Methods

the way to gain access to a method from another class is by changing the access modifier
![[Public Access Modifiers.png]]

``` c#
Scoreboard scoreboard;

    void Start()
    {
        scoreboard = FindFirstObjectByType<Scoreboard>();
    }
```

the code above will look through our entire project until it finds the game object in the scene called scoreboard and then will set the reference in the code as equal to that object. since we know that there is only one scoreboard in our scene it will stop looking for other references once it finds it. this method is very computationally expensive and as such should only be ran when the class is initialised as apposed to in update

### Unity's UI Canvas - TMP Pro text

- for our text we are using TMP_Pro which requires us to import a new asset pack (Unity will offer us the choice to install it automatically when attempting to create a TMP text object)
- we then need to use the `TMPro` namespace in our class to access the object
- we can then serialize the field as a `TMP_Text` object (an object accessible because we imported the `TMPro` namespace)
- from there we can access the text element itself and add our score variable - `scoreboardText.text = "Score: " + score;`

### Timelines and control tracks - adding enemy waves
- on our master timeline we can add a control track that will host other timelines or more specifically `.playbale` files
- we can prefab timelines and re use them at later intervals
- its not necessary to have multiple control tracks however if we want to have animations and waves that overlap each other we will need to use multiple 

the rest of this course goes on to focus on other unity side aspects such as more cameras and timelines however for the sake of completing this course with a relative level of speed I am opting to move onto the next section entitled "Royal Run" which will hopefully focus on more code sided issues



