
Namespaces & Classes
- Namespaces are containers for classes
- classes are containers for variables and methods

E.G. - UnityEngine is a namespace and in that namespace we have our classes

Need to know bases
 - where possible Encapsulate our code
 - limit what our code can see/ be changed by or change
 - typically we aim for classes to do one main thing instead of multiple things, this is because it will make our code easier to read, easier to find and fix issues, easier to have multiple people collaborate on a project

existing classes
- unity has many built in classes however to access them we have to use the relevant Namespace
- a list of all Namespaces and their related classes can be found in the unity scripting documentation - https://docs.unity3d.com/6000.0/Documentation/ScriptReference
- we access a classes contents with the . operator, e.g. ClassName.MethodName()
- the term Class and Script can be used somewhat interchangeably

classes we create
- one class per script is ideal for better encapsulation and organisation
- said classes tend to only be responsible for one thing e.g. movement, Collison, score etc

children of empty game objects
- good practice is to use empty game objects for technical stuff like scripts and rigid body's while keeping visual and graphical elements constrained to prefabs and other physical game objects
- something to watch out for is that children's co-ordinates will always be relative to the parents, e.g. if you move the parents co-ordinates the child will follow however if you move the child alone the parent will not follow

Simplest Input System Approach
- this project teaches input using a system that has us define action bindings in the inspector
- input actions allow us to use multiple input systems to preform the same action e.g. keyboard, controller etc

steps in this approach
- use UnityEngine.InputSystem namespace
- create serialized Input Action variables 
- add bindings for each InputAction
- enable the InputActions
- use the value of InputAction for gameplay
- disable each InputAction as and when required

standard naming convention
- in unity the standard naming convention for Rigidbody's is to name them "rb"

difference between AddForcce and AddRelativeForce
- AddForce applies a force to a game object based on the global position of the object however AddRelativeForce will apply a force to the game object based upon its actual position and rotation
- e.g. if I were to turn a model 90 degrees to the left AddForce would apply an upwards force because of the global position of up however AddRelativeForce would apply a force to the left of the object because of its local position

audio in unity
- requires three things, audio file, audio source, and the audio listener

audio in classes
- requires the AudioSource component

switch statements
- are a conditional similar to if / if else statements
- allow us to compare a single variable to a series of constants 

switch syntax
```
switch (variableToCompare)
{
	case valueA:
		actionToTake();
		break;
	
	Case valueB:
		OtherAction();
		break;
	
	default:
	thirdAction();
	break;
}
```

invoke
- allows us to call a method to execute after a delay
- quick and easy to use however not as performant as using a Coroutine

syntax
```
Invoke("MethodName", delayPeriod)
```

Unity's Particle system
- formed of an emitter and the particles
- is a component attached to a game object
- we use modules to control behaviour 
- the particles themselves are not game objects

Post Processing
- post processing can be done through adding what are called overrides to the global volume if one is present in the scene
- different overrides all have different effects, its a case of playing about with the effects and finding what you like / what's right for your game