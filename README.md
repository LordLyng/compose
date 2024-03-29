# LordLyng's dev setup in docker compose

This small repo is primarily used by me to save my docker compose dev setup.

## Why?
Due to my job often requiring me to host databases on different types of servers, and each server would require background resources were it to be isntalled directly on my mahcine; I decided to find a better solution. Heavily inspired by a colleague who has a similar setup i ended up with this repo.  

The Observability was a later addon.

## Primary tools
* [Docker](https://www.docker.com/ "Docker | docker.com")
* [Docker Compose](https://docs.docker.com/compose/ "Docker compose overview | docs.docker.com")
* [dctl](https://github.com/FabienD/docker-stack "docker-stack | GitHub.com")
    * Works a bit lioke kubectl allowing you to control your compose setup centrally without navigating into the separate folders.

## Compose configuration
See the docker-compose files in repo.

## dctl configuration

https://github.com/LordLyng/compose/blob/f9507bb21c2042148331da777db07f2f819d450b/config.toml#L1-L29

## Invoking docker commands in WSL from pwoershell in windows
In many cases I flip back and forth between Windows and WSL. Because of that I often make my most used WSL commands available in powershell.  

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
The above functions enables the user to invoke docker and dctl from pwoershell - as seen it simply invokes `wsl` followed by the required command passing all arguments along. this effectively means that everytime the user writes `docker` or `dctl` in PowerShell the command is forwarded to WSL where the command is executed.

### Completions for proxy commands in PowerShell
Both dsocker and dctl has completions available. Completions helps the user be more efficient and fast when interacting with the cli's as it makes it easy to access commands without having to look them up externally every time.

I managed to get completions for both `dcoker` and `dctl` in PowerShell despite them being proxied to WSL.

#### docker completions in PowerShell
To get `dcoker` completions I used the following repo [DockerCompletion](https://github.com/matt9ucci/DockerCompletion "DockerCompletion | GitHub.com").

It's rather easy to achieve just run the following command in PowerShell
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
dctl completion powershell
```
copy the output (rather large, might be useful to pipe it into some temporary file) and add it to your PowerShell profile.

You now have completions in both `dcoker` and `dctl` despite the commands being proxied to WSL!
