# LordLyng's dev setup in docker compose

This smallr epo is primarily used by me to save my docker compose dev setup.

## Why?
Due to my job often requiring me to host databases on different types of servers, and each server would acquire background resources were it to be isntalled directly on my mahcine; I decided to find a better solution. Heavily inspired by a colleague who has a similar setup i ended up with this repo.  

The Observability was a later addon.

## Primary tools
* [Docker](https://www.docker.com/ "Docker | docker.com")
* [Docker Compose](https://docs.docker.com/compose/ "Docker compose overview | docs.docker.com")
* [dctl](https://github.com/FabienD/docker-stack "docker-stack | GitHub.com")
    * Works a bit lioke kubectl allowing you to control your compose setup centrally without navigating into the separate folders.

## Compose configuration
See the docker-compose files in repo.

## dctl configuration
https://github.com/LordLyng/compose/blob/main/config.toml

## Invoking docker commands in WSL from pwoershell in windows
In many cases I flip abck and fortyh between Windows and WSL. Because of that i often make my most used WSL commands available in powershell.  

To achieve this open your PowerShell profile in an Editor, e.g.
```powershell
code $PROFILE
```

Then add the following code to the file:
```powershell
function docker() {
    wsl docker $args
}

function dctl() {
    wsl dctl $args
}
```
The above functions enables the user to invoke docker and dctl from pwoershell - as seen it simple invokes wsl followed by the required command passing all arguments along. this effectively means that everytime the suer writes `docker` or `dctl` in PowerShell the command is forwarded to WSL where the command is executed.

### Completions for proxy commands in PowerShell
Both dsocker and dctl has compeltions available. Completions helps the user be mroe efficient and fast when interacting with the cli's as it makes it easy to access commands without having to look then up externally every time.

I managed to get completions for both `dcoker` and `dctl` in PowerShell depsite them being proxied to WSL.

#### docker completions in PowerShell
To get `dcoker` comletions i used the following repo [DockerCompletion](https://github.com/matt9ucci/DockerCompletion "DockerCompletion | GitHub.com").

It's rather easuy to achieve just run the following command in PowerShell
```powershell
Install-Module DockerCompletion -Scope CurrentUser
```
the open your profile in an editor
```powershell
code $PROFILE
```
Add the following line to your profile
```powershell
Import-Module DockerCompletion
```
restart pwoershell and enjoy docker completions.

#### dctl completions in PowerShell
The dctl cli has a command for generating completions.
Run the following
```powershell
dctil completion powershell
```
copy the output (rather large, might be useful to pipe it into some temporary file) and add it to your PowerShell profile.

You now have completions in both `dcoker` and `dctl` despite the commands being proxied to WSL!