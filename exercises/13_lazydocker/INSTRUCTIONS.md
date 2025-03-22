# Description

This exercise shall demonstrate how to use lazydocker for better navigation

# Exercises

## Task 1

Use lazydocker to see details of running containers and images.

* Run `docker run -d nginx`
* Run `docker run -e MYSQL_ALLOW_EMPTY_PASSWORD=true -d mysql`
* Run `lazydocker`
* Navigate between menu points with `h` and `l` or use the number to jump directly to a menu point (like `4` for Images)
* Within a menu point, navigate with `j` and `k` between entries
* Go to `Standalone Containers` or `Containers`
* To go to the details on the right of a container, press <ENTER>
* Navigate between Tabs with `[` and `]` to see Logs, Stats, Env, Config or Top
* Press <ESC> to go back to the menu on the right
* Go to `Images`
* Select any image to see the history on the right
* Press <ENTER> to navigate within the history if it is very long
* For further supported shortcuts, press `?` or `x` to open the help menu
* Press `q` to close lazydocker

## Task 2

Start an interactive shell

* Run `lazydocker`
* Go to the containers menu point
* select any container and press `E`
* An interactive shell is open within the selected container
* Navigate around in the container and if you are finished type `exit` to leave the interactive shell to go back to lazydocker
* Press `q` to close lazydocker

## Task 3

Run bulk commands

* Run `lazydocker`
* Go to the containers menu point
* Press `b` to open the bulk menu
* Select `stop all containers` to stop the nginx and mysql container
* Select another bulk command to delete all exited containers
* Press `q` to close lazydocker

## Task 4

Manage composed containers

* Run `lazydocker` (be sure to run from within the 13_lazydocker directory containing the compose.yaml file)
* Go to the `Services` menu point
* Open the bulk menu and select `up` to start both containers from the compose.yaml file
* Container should be up and running
* Navigation in the `Services` menu point is similar to standalone container
* Play around and at the end, call the bulk menu and shutdown all services form the compose.yaml file 
* Press `q` to close lazydocker