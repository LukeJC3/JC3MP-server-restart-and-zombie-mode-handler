# JC3MP-server-restart-and-zombie-mode-handler
Bash files to automatically restart your server and handle the "zombie" mode failed restart

#Intruduction
Just Cause 3 Multiplayer servers have an issue where, after a restart, they start without loading any packages but still go online and act quite weirdly. This state was name zombie mode
What's gonna happen is, you can still join the server, but without any packages loaded, there's not a whole lot you can do, and if you leave the server and try to join again, it won't let you join again
This can only be fixed by another server restart, but since the server actually runs and appears online, simple restart scripts won't be able to notice that it's in this weird state

![zombiemode](https://user-images.githubusercontent.com/78240158/148134157-7046ee8d-a1d4-471b-be82-ab83f3847671.png)

#The solution
Now, since the developers of the multiplayer mod stopped work on it, there's no way this will get fixed, so it's up to my insane dedication to this game to do it!

What I've done basically is made a simple restart script for the server (autorestart) and another one to detect zombie mode (zombiehandler)
There's probably better ways to make these if you know your way around better, but I do not so 🤷

autorestart will constantly check if the server is running, and if not, restart it using nohup (you don't need to know the details for this, just that this creates a log file with the server window's outputs next to the server executable). This will take care of regular crashes where the server simply stops running

zombiehandler will constantly scan the server log file (nohup.out) and if it notices the message "Loaded 0 package" appears in the logs file, which it will if the server starts in zombie mode, it will restart the server and delete the logs file

#Setup

Create two files in a directory of your choosing
Name them autorestart and zombiehandler or whatever you want to name them

Copy the code of the two files on here into yours and save them
Now change the details I marked in capital letters, i.e. the path to your server executable and the name of your server executable
Save them both

Now you need to set their permissions
If you are using a gui application like winscp, set them like this

![perms](https://user-images.githubusercontent.com/78240158/148135220-c02cef83-808c-46ff-81fe-1e150d5bb602.png)

Next, if you try to run them, you might get an error like "/bin/bash^M: bad interpreter: No such file or directory"
To fix this, run cd to the directory these two files are in and run "sed -i -e 's/\r$//' FILENAME"
Do this for both files and they should now be executable perfectly fine!

Now you can run both of them (for example "screen -d -m FILENAME", so they will keep running when you disconnect from the terminal) and they will check on your server and restart in any circumstances!

#Hope these help you! For any questions, feel free to contact me on Discord!
