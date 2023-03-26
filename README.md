# Stand-Lua-Scripting-Tutorial
a quick and easy tutorial for making an lua script for stand mod.

# Setting you up.
So your interested in making a script for stand mod?
Lets set you up, first you will need an code editor personally i use Visual Studio Code you can choose alot others tho or even use the default text editor on your pc
you can find alot of editors on youtube and tutorials on how to install them.

Ill explain this vor visual studio code since i dont use an other editor,
Ones you have installed your editor you will need to add the lua extension to make it alot easyer for you.
You can do this by clicking the Extensions button on the left side of vsc and search "Lua" install the one that is on the top.

Then when your code editor is setup for making scripts you will need to open the Stand Launchpad and click "Open Stand Folder"
you will see an folder called Lua Scripts you open it and make an new txt file and name it to the name you want it to be this will also be the name it will display in stand when you got your name you just need to change from .txt to .lua to change the type of the file to a lua file.

# Simple idea
When you are getting started and are a beginner its the best you think of something simple to create like spawning in an vehilce or object.
Ill explain on how you can spawn in a vehicle.

# websites you will need for this.
You will need the stand api for the basic functions to make options for stand. (https://stand.gg/help/lua-api-documentation)
You will also need the Gta V Native data base, natives are functions used by the game that you can use to make stuff with. (https://nativedb.dotindustries.dev/natives)
For this option (spawning a vehicle) you will need to pick the vehicle you wanna spawn you can find the vehicles on alot of websites but i always use this one. (https://gtahash.ru/car/)

# The code
Here is the code and a quick explanation,
```lua
--this function is used to request is model of the vehicle so we can spawn it you will also need to use this for spawning objects--
function request_model(hash)
    --request the model of the hash--
    STREAMING.REQUEST_MODEL(hash)
    --while the model has not yet loaded of the hash we wait--
    while not STREAMING.HAS_MODEL_LOADED(hash) do util.yield(0) end
end

--menu.action makes an action button in "menu.my_root()" what this means is it makes an button in the default root you can make lists in the default root and then put this option in that list--
menu.action(menu.my_root(), "Spawn Vehicle", {}, "With the Gta V db (data base)", function()
    --get the position of an player in this case the user so yourself--
    local position = players.get_position(players.user())
    --setting the hash of the vehicle in this case it is an itali gto--
    local hash = util.joaat("italigto")
    --we request the model of the hash with the function above--
    request_model(hash)
    --then we create the vehicle with the gta native db (data base)--
    VEHICLE.CREATE_VEHICLE(hash, position.x ,position.y ,position.z, 0, true, false, true)
end)

--menu.action makes an action button in "menu.my_root()" what this means is it makes an button in the default root you can make lists in the default root and then put this option in that list--
menu.action(menu.my_root(), "Spawn Vehicle", {}, "With Stands api.", function()
    --get the position of an player in this case the user so yourself--
    local position = players.get_position(players.user())
    --setting the hash of the vehicle in this case it is an itali gto--
    local hash = util.joaat("italigto")
    --we request the model of the hash with the function above--
    request_model(hash)
    --then we create the vehicle with the stand api--
    entities.create_vehicle(hash, position, 0)
end)
```
In this code you have 2 action options in the menu.my_root() the first one uses the gta native db for creating the vehicle and the second uses the stand api to create the vehicle.

The functions you see that are written in CAPS means that they come from the gta native db since all the functions are written in caps the rest somes from the stand api look when they do read the stand api and look in the native db to see what you can all do and theres alot that you can do trust me.

Here is an example of the same option with the stand api but in a list.
```lua
--make a list in the default root--
local spawn_vehicle_list = menu.list(menu.my_root(), "Vehicle Spawn")

--menu.action makes an action button in spawn_vehicle_list what this means is it makes an button in the root of the list--
menu.action(spawn_vehicle_list, "Spawn Vehicle", {}, "With Stands api.", function()
    --get the position of an player in this case the user so yourself--
    local position = players.get_position(players.user())
    --setting the hash of the vehicle in this case it is an itali gto--
    local hash = util.joaat("italigto")
    --we request the model of the hash with the function above--
    request_model(hash)
    --then we create the vehicle with the stand api--
    entities.create_vehicle(hash, position, 0)
end)
```

# Other way you can set the root of the list
On the stand api website you see ":action(...) — shorthand for menu.action" and ":list(...) — shorthand for menu.list" as you see these are shorthand for the things we used these are shorter then u just learned this does the same but it shorter
```lua
--make a list in the default root--
local spawn_vehicle_list = menu.my_root():list("Vehicle Spawn")

--menu.action makes an action button in spawn_vehicle_list what this means is it makes an button in the root of the list--
spawn_vehicle_list:action("Spawn Vehicle", {}, "With Stands api.", function()
    --get the position of an player in this case the user so yourself--
    local position = players.get_position(players.user())
    --setting the hash of the vehicle in this case it is an itali gto--
    local hash = util.joaat("italigto")
    --we request the model of the hash with the function above--
    request_model(hash)
    --then we create the vehicle with the stand api--
    entities.create_vehicle(hash, position, 0)
end)
```
You dont need to do this but some will like it more then others.

# Final step
Now open stand in gta and go to Stand>Lua Scripts> your script name and open it.
I hope this helped and now you can go creazy in making stuff if you still dont understand it you can join my discord server (https://discord.gg/CNf6Y6Uw) and ask me there in the #programming channel.
