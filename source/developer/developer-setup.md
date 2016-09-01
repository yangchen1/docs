Developer Machine Setup
-----------------------------

### Mac OS X ###

1. Download and set up Docker Toolbox
	1. Follow the instructions at [http://docs.docker.com/installation/mac/](http://docs.docker.com/installation/mac/)
	2. Start a new docker host  
		`docker-machine create -d virtualbox dev`
	2. Get the IP address of your docker host  
		`docker-machine ip dev`
	3. Add a line to your /etc/hosts that goes `<Docker IP> dockerhost`
	4. Run `docker-machine env dev` and copy the export statements to your ~/.bash_profile
2. Download Go 1.6 and Node.js using Homebrew
	1. Download Homebrew from [http://brew.sh/](http://brew.sh/)
	2. `brew install go`
	3. `brew install node`
3. Set up your Go workspace
	1. `mkdir ~/go`
	2. Add the following to your `~/.bash_profile`  
		- `export GOPATH=$HOME/go`  
		- `export PATH=$PATH:$GOPATH/bin`  
		- `ulimit -n 8096`  
		- If you don't increase the file handle limit you may see some weird build issues with browserify or npm.  
	3. Reload your bash profile  
		`source ~/.bash_profile`
	4. Set GOROOT (optional) in your `~/.bash_profile`
		- `export GOROOT=/usr/local/go/`
4. Fork Mattermost on GitHub.com from [https://github.com/mattermost/platform](https://github.com/mattermost/platform), then:
	1. `cd ~/go`  
	2. `mkdir -p src/github.com/mattermost`  
	3. `cd src/github.com/mattermost`  
	4. `git clone https://github.com/<username>/platform.git`  
	5. `cd platform`

5. Run unit tests on Mattermost using `make test` to make sure the installation was successful
6. If the tests passed, you can run Mattermost using `make run`
7. You need to create a team and admin account. You can choose a team name, email and password:
	- Note: Make sure your team name does not contain any spaces
	- `go run mattermost.go  -create_team -team_name="name" -email="user@example.com"`
	- `go run mattermost.go  -create_user -team_name="name" -email="user@example.com" -password="mypassword"`
	- `go run mattermost.go  -assign_role -team_name="name" -email="user@example.com" -role="system_admin"`

8. Now you can log into Mattermost as the user you created in step 7
9. You can stop Mattermost using `make stop`
10. If you want to setup for cross compilation (required for the `make package` and dependant targets) run:
    - Note: You can skip the platform you are on because you have that target installed by default.
    - `env GOOS=windows GOARCH=amd64 go install std`
    - `env GOOS=darwin GOARCH=amd64 go install std`
    - `env GOOS=linux GOARCH=amd64 go install std`

Any issues? Please let us know on our forums at: https://forum.mattermost.org/

### Ubuntu ###

1. Download Docker, follow the instructions at [https://docs.docker.com/installation/ubuntulinux/](https://docs.docker.com/installation/ubuntulinux/)
2. Set up your dockerhost address
	1. Edit your `/etc/hosts` file to include the following line  
		- `127.0.0.1 dockerhost`
3. Install build essentials
	1. `apt-get install build-essential`
4. Download Go 1.5.1 from [http://golang.org/dl/](http://golang.org/dl/)
5. Set up your Go workspace and add Go to the PATH
	1. `mkdir ~/go`
	2. Add the following to your `~/.bashrc`
		- `export GOPATH=$HOME/go`  
		- `export PATH=$PATH:$GOPATH/bin`  
		- `ulimit -n 8096`  
		- If you don't increase the file handle limit you may see some weird build issues with browserify or npm.  
	3. Reload your bashrc  
		- `source ~/.bashrc`
	4. Set GOROOT (optional) in your `~/.bash_profile`
		- `export GOROOT=/usr/local/go/`
6. Install Node.js  
	- `curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -`  
	- `sudo apt-get install -y nodejs`
7. Fork Mattermost on GitHub.com from [https://github.com/mattermost/platform](https://github.com/mattermost/platform), then:
	1. `cd ~/go`  
	2. `mkdir -p src/github.com/mattermost`  
	3. `cd src/github.com/mattermost`  
	4. `git clone https://github.com/<username>/platform.git`  
	5. `cd platform`
8. Run unit tests on Mattermost using `make test` to make sure the installation was successful
9. If the tests passed, you can run Mattermost using `make run`
10. You need to create a team and admin account. You can choose a team name, email and password:
	- Note: Make sure your team name does not contain any spaces
	- `go run mattermost.go  -create_team -team_name="name" -email="user@example.com"`
	- `go run mattermost.go  -create_user -team_name="name" -email="user@example.com" -password="mypassword"`
	- `go run mattermost.go  -assign_role -team_name="name" -email="user@example.com" -role="system_admin"`

11. Now you can log into Mattermost as the user you created in step 10
12. You can stop Mattermost using `make stop`
13. If you want to setup for cross compilation (required for the `make package` and dependant targets) run:
    - Note: You can skip the platform you are on because you have that target installed by default.
    - `env GOOS=windows GOARCH=amd64 go install std`
    - `env GOOS=darwin GOARCH=amd64 go install std`
    - `env GOOS=linux GOARCH=amd64 go install std`

Any issues? Please let us know on our forums at: http://forum.mattermost.org

### Archlinux ###

1. Install Docker
	1. `pacman -S docker`
	2. `gpasswd -a user docker`
	3. `systemctl enable docker.service`
	4. `systemctl start docker.service`
	5. `newgrp docker`
2. Set up your dockerhost address
	1. Edit your /etc/hosts file to include the following line
		`127.0.0.1 dockerhost`
3. Install Go
	1. `pacman -S go`
4. Set up your Go workspace and add Go to the PATH
	1. `mkdir ~/go`
	2. Add the following to your ~/.bashrc
		- `export GOPATH=$HOME/go`
		- `export GOROOT=/usr/lib/go`
		- `export PATH=$PATH:$GOROOT/bin`
	3. Reload your bashrc
		- `source ~/.bashrc`
	4. Set GOROOT (optional) in your `~/.bash_profile`
		- `export GOROOT=/usr/local/go/`
4. Edit /etc/security/limits.conf and add the following lines (replace *username* with your user):

	```
		username	soft	nofile	8096  
		username	hard	nofile	8096  
	```

	You will need to reboot after changing this. If you don't increase the file handle limit you may see some weird build issues with browserify or npm.
5. Install Node.js
	`pacman -S nodejs npm`
6. Fork Mattermost on GitHub.com from [https://github.com/mattermost/platform](https://github.com/mattermost/platform), then:
	1. `cd ~/go`  
	2. `mkdir -p src/github.com/mattermost`  
	3. `cd src/github.com/mattermost`  
	4. `git clone https://github.com/<username>/platform.git`  
	5. `cd platform`
7. Run unit tests on Mattermost using `make test` to make sure the installation was successful
8. If the tests passed, you can run Mattermost using `make run`
9. You need to create a team and admin account. You can choose a team name, email and password:
	- Note: Make sure your team name does not contain any spaces
	- `go run mattermost.go  -create_team -team_name="name" -email="user@example.com"`
	- `go run mattermost.go  -create_user -team_name="name" -email="user@example.com" -password="mypassword"`
	- `go run mattermost.go  -assign_role -team_name="name" -email="user@example.com" -role="system_admin"`

10. Now you can log into Mattermost as the user you created in step 9
11. You can stop Mattermost using `make stop`
12. If you want to setup for cross compilation (required for the `make package` and dependant targets) run:
    - Note: You can skip the platform you are on because you have that target installed by default.
    - `env GOOS=windows GOARCH=amd64 go install std`
    - `env GOOS=darwin GOARCH=amd64 go install std`
    - `env GOOS=linux GOARCH=amd64 go install std`

Any issues? Please let us know on our forums at: http://forum.mattermost.org

### Windows ###

1. Install and setup Docker Toolbox
    1. Install [Docker Toolbox](https://www.docker.com/products/docker-toolbox)
    2. Run the `Docker Quickstart Terminal` and let it configure `default` machine
    3. Get `default` IP by run `docker-machine ip default` in the terminal
    4. Add the line `<Docker-IP> dockerhost` to `C:\Windows\System32\drivers\etc\hosts` using editor with administrator privilege
2. Install and setup Node.Js
    1. Download and install from [https://nodejs.org/](https://nodejs.org/)
    2. Open `Node.js command prompt` and run `npm config set cache <short-path>` to set npm global cache to shorter path, the default path will likely cause path over 255 characters.
3. Download and install Go from [https://golang.org/dl/](https://golang.org/dl/) 
4. Install and setup MSYS2
    1. Download and install from [https://msys2.github.io/](https://msys2.github.io/)
    2. Following the page's instruction to update MSYS2 packages
5. Fork Mattermost on GitHub.com from [https://github.com/mattermost/platform](https://github.com/mattermost/platform), then do the following in Git Bash:
    1. `cd ~/go`  
    2. `mkdir -p src/github.com/mattermost`  
    3. `cd src/github.com/mattermost`  
    4. `git clone https://github.com/<username>/platform.git`  
    5. `cd platform`
    6. `git config core.eol lf`
    7. `git config core.autocrlf input`
    8. `git reset --hard HEAD`
4. Run `MinGW-w64 Win64 Shell` of `MSYS2` to open shell
5. Setup the following environment variable (change the path accordingly):
      
    ```
    export GOROOT="/c/Program Files/go"
    export PATH=$GOROOT/bin:$PATH
    export PATH="/c/Program Files/nodejs":$PATH
    export PATH="/c/Program Files/Git/bin":$PATH
    export PATH="/c/Program Files/Docker Toolbox":$PATH
    export GOPATH=$HOME/go
    eval $(docker-machine env default)
    ```

6. Patch make files:
    1. In Ldap part of `start-docker` section of root Makefile, change all `docker exec -it ...` to `docker exec -i ...` as docker in windows can't deal with tty.
    2. In `webapp/package.json`, `build` and `run` of `scripts` are beginning with `NODE_ENV=production`, remove it as Node.Js in windows are not using unix shell, it does not understand tne environment variable synax.
    3. In windows part of `package` section of root Makefile, change `cp $(GOPATH)/bin/windows_amd64/platform.exe` to `cp $(GOPATH)/bin/platform.exe`, for some reason go in windows does not produce binary under architecture folder.
7. Run unit tests on Mattermost using `make test` to make sure the installation was successful
8. If the tests passed, you can run Mattermost by following: (very different from linux/mac due to the binary files are *windows* execs, we cannot simply using `ps` and `kill` in MSYS2 to stop processes)
    1. Open two more MSYS2 shells and setup the same environment variable
    2. Remove the `&` of last command of `run-server` of root Makefile and run `make run-server`
    3. Using another shell and go to `~/go/src/github.com/mattermost/platform/webapp/`, run `npm run run`.
9. You need to create a team and admin account. You can choose a team name, email and password in third shell:
	- Note: Make sure your team name does not contain any spaces
	- `go run mattermost.go  -create_team -team_name="name" -email="user@example.com"`
	- `go run mattermost.go  -create_user -team_name="name" -email="user@example.com" -password="mypassword"`
	- `go run mattermost.go  -assign_role -team_name="name" -email="user@example.com" -role="system_admin"`

10. Now you can log into Mattermost as the user you created in step 9
11. You can stop Mattermost by stoping shell of step 8-1 and 8-3
12. If you want to setup for cross compilation (required for the `make package` and dependant targets) run:
    - Note: You can skip the platform you are on because you have that target installed by default.
    - `env GOOS=windows GOARCH=amd64 go install std`
    - `env GOOS=darwin GOARCH=amd64 go install std`
    - `env GOOS=linux GOARCH=amd64 go install std`

## Developing Using PostgreSQL

By default, development is done using a MySQL database. To switch your developement instance to use a PostgreSQL database, update the following settings in the `SqlSettings` section of your `config/config.json`
```
    "DriverName": "mysql",
    "DataSource": "mmuser:mostest@tcp(dockerhost:3306)/mattermost_test?charset=utf8mb4,utf8",
```
to
```
    "DriverName": "postgres",
    "DataSource": "postgres://mmuser:mostest@dockerhost:5432?sslmode=disable&connect_timeout=10",
```
