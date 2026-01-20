# UE5-LockingTraget-System
Basic Souls-Like TargetLock system implementaion using blueprints in Unreal Engine 5

Note: These methods may be suitable only for small indie projects and may not be appropriate for large-scale or professional projects.

# Basic Structure

### Some basic variables that we need:
- <b>IsActiveTracking (bool)</b> to check if tracking is active;
- <b>ClosestEnemy</b> to store current closest enemy to the player;
- <b>Locking In</b> to store current Scene Component (target that is visible on the screen).

### Scene Component
On your Enemy's blueprint create a SceneComponent. It must be attached to CharacterMesh. To add an actual visible Target, create a WidgetComponent, and attach it to the SceneComponent. For the target I'm using a .png image. 

<img width="433" height="220" alt="Screenshot_677" src="https://github.com/user-attachments/assets/f5136e43-011c-4a74-b666-75b9fdab2a96" />

By deafault SceneComponent must be:
- <b>Hidden In Game</b> - True;
- <b>Two-Sided</b> - True

### Scene Component's Functions

<img width="424" height="132" alt="Screenshot_678" src="https://github.com/user-attachments/assets/b40b71ed-43b2-445f-b0bc-cde489010ab8" />

We need 2 functions to change the visibility state of the Target:
- <b>Show Target</b> - Changes the "Hidden In Game" parameter to true;

<img width="688" height="369" alt="Screenshot_679" src="https://github.com/user-attachments/assets/47b9bd90-1077-47c8-97d1-ac70bdcc2518" />

- <b>Hide Target</b> - Changes the "Hidden In Game" parameter to false;

<img width="526" height="321" alt="Screenshot_680" src="https://github.com/user-attachments/assets/178c51a5-ca1a-4682-8b0f-56b4536111e2" />

These 2 functions are going to be called in the main function.

# Main function

<img width="1498" height="657" alt="Screenshot_671" src="https://github.com/user-attachments/assets/ca294253-3088-43ec-8888-0c31ebe38675" />

## Flip Flop
In your Player's Blueprint create a Button event (in my case Middle Mouse Button).
Using Flip Flop we can bind actions when the button is pressed the first time (A) and when it is pressed after the first time (B).

### On A

When it is Flip Flop's <b>A</b>:
- IsActiveTracking is set to True;
- Using Sphere Overlap Actors we can detect all the Actors with the Object type "Pawn" that are located in the given Radius (1500 in my case), ignoring the Self Actor (player);
  
<img width="653" height="600" alt="image" src="https://github.com/user-attachments/assets/68e45a04-12a8-4ebb-83ad-65883929e426" />


- If there are any pawns, in return we got an Array in which we are finding the closest to the Player using "Find Nearest Actor". The result is going to be our ClosestEnemy;


<img width="739" height="259" alt="image" src="https://github.com/user-attachments/assets/92d13ec4-ac4c-46cf-a8b9-821a38f9c467" />

### On B

When it is Flip Flop's <b>B</b>:
- IsActiveTracking is set to False;
- By casting to Enemy's blueprint we call the Hide Target function (the object is ClosestEnemy).

<img width="437" height="218" alt="image" src="https://github.com/user-attachments/assets/56660974-fb38-46a7-8aef-9e89776141cb" />

## Showing a Target

<img width="1035" height="622" alt="Screenshot_672" src="https://github.com/user-attachments/assets/725bd414-5d19-4067-9b1b-9fe05b1a4e47" />

After getting our ClosestEnemy, we need to cast to is blueprint class in order to call a ShowTarget function. After that it is important to set Locking In by getting Target Point.

## Main Loop

<img width="1321" height="605" alt="Screenshot_673" src="https://github.com/user-attachments/assets/26b3e7e1-8153-4fda-bb13-1f796d2185e9" />
