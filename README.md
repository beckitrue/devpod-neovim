# devpod-neovim

This is a devpod for neovim Proof of Concept. It's using the open source [DevPod](https://devpod.sh) development environment 
running on Docker. There are other provider options for running DevPod, such as using Kubernetes, or cloud providers 
but I'm using Docker for this PoC.

Neovim is not a built-in IDE option in DevPod, so I'm building a custom devpod that includes neovim and plugins that I use. I'm also installing packages needed for my neovim configuration. You can try this as is, or use your own dotfiles and install script to suit your needs.

## Demo

You can see the demo of the devpod-neovim in action by clicking on the image below:

[![Watch the video demo](https://img.youtube.com/vi/6vzl7Ba2uRE/0.jpg)](https://youtu.be/6vzl7Ba2uRE)

## The DevPod

I'm testing using the same [dotfiles](https://beckitrue/dotfiles) that I use on my local machine.
I didn't make any changes since this is a PoC. But, for a real use case I would have dotfiles
for the specific environment. 

For example, this devpod is using a `go` image, but in my neovim configration files I load Python 
and Node LSPs. This results in a (non-fatal) error message when running neovim on this devpod.

## Try It Out

You can try out the same configuration that I have by following the instructions below (assumes that you have `docker` installed):

1. Optional if you want a GUI:
[Install DevPod](https://devpod.sh/docs/getting-started/install) for your environment
1. [Install the DevPod CLI](https://devpod.sh/docs/getting-started/install#optional-install-devpod-cli)
1. Set your devpod provider to docker: `devpod provider use docker`
1. Verify your provider setting: `devpod provider list`
1. Clone this repo
1. Start Docker
1. From the repo directory, run `devpod up devpod-neovim . --provider docker --dotfiles https://github.com/beckitrue/dotfiles`
1. Log into the devpod `ssh devpod-neovim.devpod` (no password required)

### Packages Installed

These packages are installed as `features` using the `devcontainer.json` file:

- neovim - using the Feature that uses the source code
- stow - for managing dotfiles
- fzf - fuzzy finder
- ripgrep - faster than grep 
- starship - shell prompt
- tmux - terminal multiplexer

These binaries are installed by the `install.sh` script:

- fd-find
- bat
- lazygit

The `install.sh` script uses `stow` to create the symlinks from the dotfiles to the `.config` directory

## Usage

1. Login to the devpd `ssh devpod-neovim.devpod`
1. Run `nvim` to start neovim and use it as you would on your local machine
1. From the main menu select `Lazy` or type `L`
1. `Update` to update the plugins
1. Logout by typing `exit`
1. Stop the devpod after logging out by running `devpod stop devpod-neovim`

## Configuration Changes

You can change the `.devpod/devcontainer.json` file to add or remove packages. Run `devpod up devpod-neovim --recreate` after 
making changes to the `devcontainer.json` file.

