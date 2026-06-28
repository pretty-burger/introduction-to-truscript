The goal of this post is to help you understand what TruScript is, this is isn't really a tutorial on how to become the best programmer in the world but it should clear up some confusion :')

Everything here is not included in the docs

Just wanna let you know that to write comments you need to add "#" before
```py
# This is my comment
```

# Variables
Let's explain variables and their types rq
Defining a variable is as simple as doing 
```py
local fee = "foo"
```

Variables can have diff types such as string, number, boolean..
Im not gonna go far into the details here but defining them is also very simple
```py
local smart = "nicholas" # string
local isAlive = true # boolean (is either true which means yes or false which means no)
local timeLeft = 123 # number
```

Working with strings is very easy so im just going to go over the stuff that is not in the docs
https://create.truworlds.com/docs/modules/string

Putting two strings together is very simple
```py
local text1 = "fart"
local text2 = "smells"

local finalText = text1 + text2

print(finalText) # Prints "fartsmells"
```

Working with numbers is very simple and you def already know how to do everything here if you already used luau but im gonna go over that just incase
```py
local number1 = 15
local number2 = 5

local numberSubtracted = number1 - number2

print(numberSubtracted)
```

Now if you wanted to convert a number into a string and print it out together you can do it the following way
```py
local someNumber = 123

local numberToString = tostring(someNumber) # 123 -> "123"
local stringToNumber = tonumber(numberToString) # "123" -> 123
```

And converting to booleans is also possible incase you need it
```py
local booleanString = "true"
local stringToBoolean = tobool(booleanString) # "true" -> true
```

# Functions
Alr now that we got that out of the way let's just talk about functions

Basic function usage can go sum like this
```py
func nameOfFunction():
  print("The function has been called")

nameOfFunction()
```

You can also make anon functions, or in other words defining a function without a name
```py
local printSomething = func(text):
  print(text)

printSomething("Hello world")
```

Another way to define anon functions is by using no name at all! This can be used for things like spawn() or .Connect() which we are going to talk about in a second
```py
# Spawn allows us to run our function without forcing the entire script to wait for it to finish running
# In other words prevents our function from yielding
spawn(func():
  print("This is an anon function!")
  wait(1)
  print("Waited one second.")
)

SomeSignal.Connect(func():
  print("Signal has been fired!")
)

```
# Tables
Syntax for tables:
```py
local someTable = {}
```

List of functions:
- table.count(table) -> Retuns how many values are saved in our table (number)
- table.has(table, index) -> Checks if there is anything saved under said index, returns true | false (boolean)
- table.contains(table, value) -> Checks if our table has said value saved anywhere, also returns true | false (boolean)
- table.keys(table) -> Returns a list of all available keys in the table (array)
- table.values(table) -> Returns a list of all available values in the table (array)
- table.remove(table, index) -> Removes the value saved under said index from the table
- table.clear(table) -> Sets all of the values to nil, clearing the table to be empty

Their usage is pretty simple so im not going to explain each but they would be used sum like this:
```py
local someTable = {
	["Tru"] = "Worlds"
}

print(table.contains(someTable, "Worlds")) -> true
print(table.values(someTable)) -> ["Worlds"]
print(table.keys(someTable)) -> ["Tru"]
```

# Arrays
Example of an array:
```py
local someArray = []
```

Reading the value saved at x
```py
local someArray = ["Brixster", "Kyle", "Logan", "Star"]

print(someArray[0]) -> "Brixster"
```

You can also use this method to replace the value saved under said index of x
```py
local someArray = ["Brixster", "Kyle", "Logan", "Star"]

someArray[3] = "Nicholas" -> ["Brixster", "Kyle", "Logan", "Nicholas"]
```

Checking the length of an array
```py
local someArray = [1,2,3]

print(someArray.length) -> 3
```

Adding a value to the end of an array
```py
local someArray = [1,2,3]

someArray.push(4) -> 1,2,3,4
```

Adding a value to any index in an array
```py
local someArray = ["Meat", "Eggs", "Apples"]

someArray.insert(1, "Milk") -> "Meat", "Milk", "Eggs", "Apples"
```

Removing the last saved value on the end of an array
```py
local someArray = [1,2,3]

someArray.pop() -> 1,2
```

Removing a specific value in an array
```py
local someArray = [1,2,3]

someArray.remove(2) -> 1,3
```

# Loops (While & For)

While loops allow you to keep repeating the same block of code forever until the conditions have been met, the syntax for a while loop will look something like this:
```py
# The condition here is the "true" part, to avoid crashing we need to add a wait() inside of the loop
while true:
	print("Hello, TruWorlds!")
	wait()
```

The condition can be anything you might need, for an example if you want your loop to run while your player is still alive you could do something like this:
```py
local player = game.Players.LocalPlayer

while player.Character.Health > 0:
	print("We are alive!")
	wait()
```
Remember that loops actually yield which means that the rest of the script is going to wait for them to finish running
You can actually break any of the loops using the keyworld "break" even if the conditions for it were not met yet
```py
# In this example, we are going to be using this "i" variable, increasing it by +1 each time and once it goes above 5+ our loop is going to break (stop running further)
local i = 0

# The condition can also be just wait(), this means that the loop is going to run forever until we break it while also waiting a bit before running the block again
while wait():
	i+=1
	if i > 5:
		break
```
Okay now let's go to For Loops
For loops will run x times, they are very simple and have 2 required and one optional parameter

```py
# The "x" in this case can be named anything you wish, it's going to be our number telling us how many times the loop has ran already
for x in range(start, end, increment):
	# Your code goes here
```

So now that you understood how they work, let me show you an example
Let's say you wanna have a round timer that goes from 20 to 0 with the increment being -1 because the timer is supposed to be decreasing the time now adding onto it

```py
local timeLeft = 20

# The first param is the current time left, the second one is -1 because we want it to end at 0 (Think of it this way, if you want your timer to end at 1 you will always put one number less as the end so that means 0), and finally we want the timer going down so the incrmenet is -1
for x in range(timeLeft, -1, -1):
	print(x)
	# In the console you will get 20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10... all the way to 0 and including it
```

# Signals
Signals are very important obviously, for an example if you wanna detect when a part is touched you are gonna be listening to the Part.Touched signal
In TruScript signals can be used very very simply
```py
func onTouched(hit):
  print(hit.Name + " touched us!")

this.Touched.Connect(onTouched)
```

# Basic Scripting (Creating a script & Basic Explanation of how they work)
Since you are probably confused about what "this" means, let me explain how scripting works on TruWorlds

We have 3 Script Types:
- Client Script
- Server Script
- Multi Script

The client script only runs on the client and will have access to the LocalPlayer or aka the player currently playing the game (More about the player class https://create.truworlds.com/docs/classes/Player)
The server script does not replicate to the client and will only run on the server, keep in mind that stuff like Players.LocalPlayer can not be access from a server script
The multi script is a script that will run on both the client AND the server, which means that it will replicate to the client so for obvious reasons do not put anything important in them

On the bottom of your screen you will see an "Asset Browser"
On the left side you should see a folder named "Assets" that is the root folder, it can not be deleted or changed and that's where we are going to keep all of your scripts inside

<img width="2559" height="1383" alt="asset_browser" src="https://github.com/user-attachments/assets/5eca7948-b02b-4212-b638-e792f4397629" />

Start by right clicking on the empty space and hovering over "New" -> "Script" click it and then you should see a small popup asking you to give your script a name and then clicking "Create"

<img width="336" height="215" alt="create_script" src="https://github.com/user-attachments/assets/3d807d28-d2ae-40ba-a76a-aecaca858ce1" />

Find your newly created script in the asset browser and make sure it's open by double clicking on it

<img width="360" height="228" alt="found_script" src="https://github.com/user-attachments/assets/226280a8-53b1-46d0-b643-796828bd2037" />

You can change the script type from here by right clicking on the script and changing the type to whatever you need, you can also rename your script or delete it from here

<img width="477" height="196" alt="changing_type" src="https://github.com/user-attachments/assets/08ec5967-2c7a-48bb-9578-89f4a9caf33a" />

# Example Usage (Attaching & Using our script)
On the left top, locate the "New Part" button to create a new part. The name doesn't matter, if you wish to rename it you can. Find the part in the Explorer and then make your way down to the Properties Widget

<img width="523" height="337" alt="create_part" src="https://github.com/user-attachments/assets/e50e29d1-1bea-4dd7-85a9-e905b7f18c95" />

Once you can see the Part's properties, scroll down until you see "Add Script Component" -> "Existing Script"

<img width="377" height="547" alt="attach_script" src="https://github.com/user-attachments/assets/587b159c-3b89-4bc6-b22f-0d530f769d87" />

<img width="200" height="111" alt="existing_script" src="https://github.com/user-attachments/assets/8e70d57a-6ee9-453e-857e-d0acebd0c849" />

Now select your script and click the "Attach" button
<img width="342" height="453" alt="attaching_script" src="https://github.com/user-attachments/assets/e5671f71-7fe6-40a4-a2e7-09dd36ee5480" />

Open your script, you can also open the script that's attached to your part by clicking the little script icon next to the name in the Explorer

<img width="360" height="228" alt="found_script" src="https://github.com/user-attachments/assets/491b707b-c146-4c07-abd1-58023fc1611e" />

Your script should look something like this:
```py
extends Instance

print("Hello, TruWorlds!")
```

Click the little play button on the top right and check if you can see the "Hello, TruWorlds!" message print out in your console

<img width="322" height="146" alt="play_test" src="https://github.com/user-attachments/assets/39aa642f-ecc8-49cb-962b-c7c7e1ee1716" />

If you can see the message then that means your script works!
If you can't see your message, make sure that the console filter is set to "All" and not "Editor" or anything else. (If it still won't show up try reattaching your script)

<img width="147" height="210" alt="console_filter" src="https://github.com/user-attachments/assets/ed9deb0c-48d7-4d69-aaa4-9b59ac5db57d" />

<img width="416" height="128" alt="console_result" src="https://github.com/user-attachments/assets/fcf98717-9cdc-4539-b4b1-dd447da8e28d" />


Alright now let's understand the confusing "extends Instance" part, this simply says that your script is attached to an Instance which is your part and allows you to use the keyword "this" to identify it

What do i mean by identifying the part by using the keyword "this" you might ask?
Well, it's simple!
The "this" keyword allows you to reference the part that the script is attached to and use it for whatever you need

An example can be this, we can spawn a chat bubble above our part for 5 seconds
```py
extends Instance

this.Speak("Hello, TruWorlds!", 5)
```

In the game your part should have a small chat bubble that will despawn in around 5 seconds after first play testing the game

<img width="214" height="159" alt="proof_of_working" src="https://github.com/user-attachments/assets/81e55259-c180-4181-bb0a-baedbb9dcfee" />


# Kill Part Example
To understand how to kill a player i recommend reading https://create.truworlds.com/docs/classes/CharacterController

Alright so let's use all of the knowledge we got from this to make a simple kill script

```py
extends Instance

# Function that will run as soon as our part comes in contact with another physical instance
# The param "hit" is the other instance touching our part
func onTouched(hit):
    # Checking if the instance touching us is a Character or not
	if hit.Parent.IsA("CharacterController") != true: 
        return
    
    # Killing the character that came in contact with our part
    hit.Parent.Kill()
    
# Connecting to the .Touched event which is going to fire whenever something touches our part
this.Touched.Connect(onTouched)
```

Click play and check if everything works fine, when you touch the part your character should end up dying

<img width="609" height="438" alt="death" src="https://github.com/user-attachments/assets/380c5789-0b32-45f3-854a-068dc834795f" />
