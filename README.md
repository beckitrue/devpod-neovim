# devpod-neovim

This is a devpod for neovim Proof of Concept. It's using the open source [DevPod](https://devpod.sh) development environment 
running on Docker. There are other provider options for running DevPod, such as using Kubernetes, or cloud providers 
but I'm using Docker for this PoC.

This is a great way to try Neovim without having to install it on your local machine. 

I can definitely see the value of having a standard development environment that is portable. This would also be great 
for use in training courses or for onboarding new developers, no matter which IDE you use.

You can read more about the approach I took to create this devpod [here](https://beckitrue.github.io/devpod-neovim/), or just get started building it by following the instructions below.

## Demo

You can see the demo of the devpod-neovim in action by clicking on the image below:

[![Watch the video demo](https://img.youtube.com/vi/6vzl7Ba2uRE/0.jpg)](https://youtu.be/6vzl7Ba2uRE)

## The DevPod

I'm testing using the same [dotfiles](https://beckitrue/dotfiles) that I use on my local machine.
I didn't make any changes since this is a PoC but, for a real use case I would have dotfiles
for the specific environment needed. 

For example, this devpod is using a `go` image, but in my neovim configration files I load Python 
and Node LSPs. This results in a (non-fatal) error message when running neovim on this devpod.

## Try It Out

You can try out the same configuration that I have by following the instructions below (assumes you have `docker` installed):

### Initial Setup

1. Optional if you want a GUI:
[Install DevPod](https://devpod.sh/docs/getting-started/install) for your environment
1. [Install the DevPod CLI](https://devpod.sh/docs/getting-started/install#optional-install-devpod-cli)
1. Set your devpod provider to docker: 
```
devpod provider use docker
```
1. Verify your provider setting: 
```
devpod provider list
```
1. Clone this repo
1. Start Docker
1. From the repo directory, run: 
```
devpod up devpod-neovim . --provider docker --dotfiles https://github.com/beckitrue/dotfiles
```

### Initial Run of Neovim

1. Login to the devpod (no password needed): 
```
ssh devpod-neovim.devpod
```
1. Run `nvim` to start neovim. The first run will install the plugins, so it may take a minute. 
1. From the main menu select `Lazy` or type `L`
1. `Update` to update the plugins
1. 'q' to quit `Lazy` and return to the main menu
1. 'c' to view the list of config files. You can scroll through the list with the arrow keys and select one to open by pressing enter.
1. You can [checkhealth](https://neovim.io/doc/user/health.html) by running `:checkhealth`
1. Logout by typing `exit`
1. Stop the devpod after logging out by running: 
```
devpod stop devpod-neovim
```

## Post Build Usage 

After you've built the devpod once, you can start it again and reconnect to it without having to rebuild it. 
```
devpod start devpod-neovim
ssh devpod-neovim.devpod
```

## Configuration Changes

You can change the `.devpod/devcontainer.json` file to add or remove packages. Run 
```
devpod up devpod-neovim --recreate
``` 
after making changes to the `devcontainer.json` file.

