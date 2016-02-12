# docknet-docker
A Docker image for using the dotnet CLI and CoreRT on any(?) Linux

## TL;DR

1. Copy the `docknet` script to somewhere on your path (and make sure it's executable).
2. Create a directory (on the host) for your app and `cd` into it
3. `docknet start` to start a **docknet** container watching the current directory
4. Use `docknet` instead of `dotnet` for the CLI - the arguments will be passed to `dotnet` in the container
5. When you're finished, `docknet stop` to kill and remove the container

## Why is this?

Right now, [CoreRT](https://github.com/dotnet/corert) and [the .NET CLI](https://github.com/dotnet/cli) only work on a limited range of Linux distros.
I tried running an Ubuntu 14.04 as my main OS for a week and it was awful, so I went back to Manjaro, but I still want to play with .NET Core.
This combination of a Docker image based on `ubuntu:trusty` with `dotnet-nightly` installed, and a little shell script that communicates with containers
running that image, means all the goodness with none of the pain.

## Is it finished?

No. This is at PoC level right now. I want to fiddle with the `docknet` script some more to make it better, but my Bash-fu is rusty.
In particular, I want to make it so `docknet start` looks for a stopped container matching the current directory and starts it if it exists,
and split the kill-and-remove behaviour of `docknet stop` so that you can stop the container without removing it, and use `docknet rm` to
delete it. That way restored packages will last between runs.
