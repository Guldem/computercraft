# MutsFM's Elevator Inc.

This readme will first explain shortly how the "MutsFM Elevator Inc" elevator system works in Minecraft and a quick guide to setting up your own system using "MutsFM Elevator Inc" software. Below that is an explanation on how the individual files in this repository work. 

Github repository files
=====

The following files should be in the repository:
  * startup-c
  * floorcontroller
  * activatefloor
  * deactivatefloor
  * startup-t
  * touchscreen
  * startup-d *to be added*
  * cartdispenser *to be added*

IMPORTANT
=====
Every floor uses two computers: a controller computer and a touchscreen computer. Each uses its own startup script, however for clarity, the names of these scripts have been amended slightly in this repository to indicate which script belongs to which computer. Additionally, several scripts provided in the respository apply to the same computer and it depends on the needs of your elevator system (e.g. number of floors or visual design for your touchscreen) which script you require.</br>
</br>
Therefore, several files in this repository need to be titled differently on your computer in Minecraft. Each section below will indicate if this is the case.</br>
</br>
**If you do not title the scripts correctly on the computer in minecraft, the system will not work!**</br>
</br>
Example: "startup-c" is the startup script for the controller computer and should be titled "startup" on your computer in minecraft.

# How the Elevator System Works
*General Principle*</br>
Using Railcraft, minecarts travel upwards on redstone powered elevator tracks and conversely travel downwards on unpowered elevator tracks. If an elevator track is powered by redstone, all other elevator tracks below it are powered as well. By selecting which elevator track to power, you determine how far the minecart travels upwards or downwards.</br>
</br>
*Elevator System*</br>
Every floor needs to have a controller computer and a 'touchscreen' connected to a computer. The player clicks on a floor number displayed on the touchscreen. The touchscreen computer registers this input, and sends out a corresponding message for the selected floor over the rednet network. Controller computers listen for these messages and once they receive a message, they act accordingly by either activating or deactivating their redstone output. The redstone output from the controller computer in turn influences the elevator track located at that level.</br>
</br>
Pictures of the elevator system's layout are available in the Wiki. (TO BE ADDED)</br>
</br>
If the floor is selected, the controller computer powers the elevator track at the floor and all elevator tracks below it, allowing for the cart to reach that floor - regardless if the cart is coming from a higher or lower floor.</br>
</br>
If the floor is unselected, the controller computer does not power the elevator track at the floor. It may however still be powered if a floor above the respective floor is selected. The power then however comes from the controller computer above.</br>
</br>
For aesthetic purposes, it is advised to reserve at least a floor space of 4 blocks wide by 6 blocks long. Smaller would be possible, at the cost of aesthetics. Due to the height of the touchscreen, every floor needs to be at least 3 blocks high.</br>
</br>
*Network*</br>
All computers (both controller and touchscreen) in a building's elevator system are connected via network wires. Although wireless connection is a possibility in ComputerCraft, it may result in unwanted interference from other computers broadcasting on the wireless communication channel used by the elevator system. In addition, elevator systems in two adjacent buildings would need to broadcast on different channels, in order for the systems to operate separately. This would however require a lot of small changes to the code on each computer in the system to be done in Minecraft itself. Therefore, a closed wired network has been chosen as the better solution, as this can be implemented without the risk of interference and without the need to make any changes to the network code from the computer in Minecraft.</br>
</br>
*Cart Dispenser*</br>
The software comes with a feature to request an empty Minecart to be delivered to your respective floor. You would need to set up a cart dispenser system in the basement of your building for this feature to work.</br>
</br>
Pictures of the cart dispenser system are available in the Wiki. (TO BE ADDED)</br>
</br>
The cart dispenser feature is however optional. Should you not wish to have such feature, you can comment out the button in the touchscreen programme (for more information, see the individual file on the cart dispenser below). In that case, you need to bring your own minecart with you.</br>
</br>
*NOTE:* The cart dispenser system as pictured on the Wiki can only supply three minecarts, due to the limited storage capacity of the cart dispenser. A cart dispenser system with more capacity is currently in development.</br>
</br>

# Quick Start Guide for Setting Up the Software
### Controller Computer
The back of your controller computer needs to be placed against a block against which in turn the elevator track is placed on at the other side. Alternatively, the elevator track can be placed against the back of the controller computer.</br>
</br>
On your controller computer, you need to install the startup-c and floorcontroller programmes. You need to title the startup-c programme as startup. You need to replace "Floor1" in the first line of the floorcontroller programme with the corresponding floor number, e.g. "Floor6". Note that groundfloor should be entered as "Floor0".</br>
### Touchscreen Computer
The touchscreen computer requires a 2 wide, 3 high construction of monitors, to be placed on the right side of the touchscreen computer.</br>
</br>
On your touchscreen computer, you need to install the startup-t and touchscreen programmes. You need to title the startup-t programme as startup. You need to replace "Floor1" in the first line of the touchscreen programme with the corresponding floor number, e.g. "Floor6". Note that the groundfloor should be entered as "Floor0".</br>
</br>
**NOTE:** The touchscreen programme in this repository is for a 7 floor building, however in the folder "ts" you can find additional touchscreen programmes for buildings with more floors. The number behind "touchscreen" indicates for how many floors that programme is designed. For example, touchscreen20n is designed for a building with 20 floors with a numpad design rather than the original design. You however need to title these programmes as **touchscreen** on your computer in Minecraft, in order for the system to work. If the exact amount of floors for your building is not covered, it is advised to select the first higher numbered touchscreen, and then delete the non-required floors from both the screen and listen functions, using the computer in Minecraft.</br>
</br>
**NOTE:** In the original design, touchscreen programmes for up to 10 floors display all available floors on the screen. Touchscreen programmes for more than 10 floors use multiple pages to display all floors. In the numpad design, a maximum of 25 floors is displayed at one page, with the possiblity to display more than 25 floors by using multiple pages. </br>
### Cart Dispenser Computer
To be added</br>

# Individual Files
The explanations below are ordered by the type of computer that uses them.

## Controller Computer
The Controller Computer activates and deactivates the redstone signal as required for your minecart to reach the selected floor. The back of your controller computer needs to be placed against a block against which in turn the elevator track is placed on at the other side. Alternatively, the elevator track can be placed against the back of the controller computer.</br> 
It requires the following scripts:
- startup-c
- floorcontroller
- activatefloor (optional)
- deactivatefloor (optional)

### startup-c
**Important!** This file should be titled as followed on your controller computer in Minecraft: **startup** </br>
This file will be automatically loaded when your controller computer in Minecraft boots.</br>
It has two main purposes:
* To connect your computer to the rednet network. (Make sure you connect the wired modem on the left side of the monitor.)
* To automatically start the floorcontroller programme.
</br>
In addition, this file will replicate a computer booting - which sole purpose is immersion only, with no real function.

### floorcontroller
**Important!** You need to enter the corresponding floor number in the first line, on the floor's controller computer in Mincraft, for the system to work! Ground Floor should be entered as "Floor0"</br>
This file controls whether or not your floor is activated or deactivated.</br>
The programme automatically listens for rednet messages (via the wired connection).</br>
* If the message corresponds to the floor number, it will activate the redstone signal at the back of the computer and then start to listen for messages again.</br>
* If the message concerns the request for a cart, it will ignore the message and starts to listen for messages again. </br>
* If the message does not correspond to the floor number, it will deactivate the redstone signal and then start to listen for messages again. </br>
It uses the restart function to start to listen for messages again. This function is therefore called when the programme is started.</br>

### activatefloor & deactivatefloor (optional)
Both files are optional, and do not need to be present on the controller computer.</br>
They are useful for testing whether the redstone and tracks have been correctly installed, as they allow you to activate and deactivate the redstone signal, without having to run the full programme and using a touchscreen monitor to send the messages.</br>


## Touchscreen Computer
The Touchscreen Computer allows the players to select the floor they wish to activate via the touchscreen. It requires the following scripts:
- startup-t
- touchscreen

### startup-t
**Important!** This file should be titled as followed on your controller computer in Minecraft: **startup** </br>
It has two main purposes:
* To connect your computer to the rednet network. (Make sure you connect the wired modem on the left side of the monitor.)
* To automatically start the touchscreen programme.
</br>
In addition, this file will replicate a computer booting - which sole purpose is immersion only, with no real function.

### touchscreen
**Important!** You need to enter the corresponding floor number in the first line, on the floor's touchscreen computer in Mincraft, for the system to work! Ground Floor should be entered as "Floor0"</br>
This file allows your players to select a floor for the elevator.</br> 
It has two main purposes:
* It connects to the screen. (Make sure the monitor is placed on the right side of the computer!),
* It registers the input from the player on the touchscreen, and 
* If the player selects a floor, it sends out a corresponding rednet message to controller computers.</br>
The touchscreen also has a feature that displays the corresponding floor number differently from the other floors, allowing players to identify on which floor they are.</br>
</br>
The touchscreen programme in this repository is for a 7 floor building, however in the folder "ts" you can find additional touchscreen programmes for buildings with more floors and with different designs. The number behind "touchscreen" indicates for how many floors that programme is designed. For example, touchscreen20n is designed for a building with 20 floors with a numpad design rather than the original design. </br> 
</br>
**IMPORTANT!** You however need to title these programmes as **touchscreen** on your computer in Minecraft, in order for the system to work. If the exact amount of floors for your building is not covered, it is advised to select the first higher numbered touchscreen, and delete the non-required floors from both the screen and listen functions, using the computer in Minecraft.</br>
</br>
The code for the touchscreen programme differs significantly, depending on whether you are running a programme for 10 floors or less, or a programme for more than 10 floors. In case of the latter, it also depends on whether you are running a programme for the original design or the numpad design. This readme will therefore first set out the touchscreen programme for the original design, then for touchscreen programmes for more than 10 floors with the original design, and then for touchscreen programmes for more than 10 floors running the numpad design.</br>
</br>
**NOTE:** In all versions, you need to replace "Floor1" in the first line of the touchscreen programme with the corresponding floor number, e.g. "Floor6". Note that the groundfloor should be entered as "Floor0".</br>
</br>
*Original Design*</br>
The screen function is used to draw the touchscreen, presenting the floors which the players can choose by hitting them on the screen.</br>
The listen function waits for the player to hit the screen, and if a player hits a floor number, then sends the accompanying message over rednet to the controller computers.</br>
</br>
*Original Design 10+*</br>
To be added.</br>
</br>
*Numpad Design*</br>
Code is similar to the original design, with the major differences being that the floors are displayed as numerical buttons (e.g. "1", "2") rather than buttons including the word floor (e.g. "Floor 1", "Floor2"), and that a maximum of 25 floors can be displayed on the screen.</br>
</br>
*Numpad Design 10+*</br>
To be added</br>
</br>
## Cart Dispenser
To be added</br>
Add text on commenting out the function</br>
