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

Start by right clicking on the empty space and hovering over "New" -> "Script" click it and then you should see a small popup asking you to give your script a name and then clicking "Create"
Find your newly created script in the asset browser and make sure it's open by double clicking on it

You can change the script type from here by right clicking on the script and changing the type to whatever you need, you can also rename your script or delete it from here

# Example Usage (Attaching & Using our script)
On the left top, locate the "New Part" button to create a new part. The name doesn't matter, if you wish to rename it you can. Find the part in the Explorer and then make your way down to the Properties Widget

Once you can see the Part's properties, scroll down until you see "Add Script Component" -> "Existing Script"

Now select your script and click the "Attach" button
Open your script, you can also open the script that's attached to your part by clicking the little script icon next to the name in the Explorer

Your script should look something like this:
```py
extends Instance

print("Hello, TruWorlds!")
```

Click the little play button on the top right and check if you can see the "Hello, TruWorlds!" message print out in your console

If you can see the message then that means your script works!
If you can't see your message, make sure that the console filter is set to "All" and not "Editor" or anything else. (If it still won't show up try reattaching your script)

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
