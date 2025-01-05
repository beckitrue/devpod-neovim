# Devcontainer with DevPod PoC

This is a proof of concept for using DevPods with Devcontainers.

This is a devpod for neovim Proof of Concept. It's using the open source DevPod development environment running on Docker. There are other provider options for running DevPod, such as using Kubernetes, or cloud providers but I'm using Docker for this PoC.

I can definitely see the value of having a standard development environment that is portable. This would be great for use in training courses or for onboarding new developers.

## The Goal of the PoC

I want to see if configuring a devpod is worth the time it takes to configure one or more environments. Worst case is that I'll learn something new about configuring development environments. Best case is that I'll have a consistent development environment that I can use on any machine.


## Approach

I orginally tried configuring the devpod by loading the packages after the devpod was created and started. 
That seemed rather useless since I wasn't really saving any time. I didn't know anything about the `devcontainer.json`
spec at the time, and that's the key to getting the efficiency and consistency that I want. IDE as Code basically.

Then, I saw this [video](https://youtu.be/9YG6QlzuNwM?si=oyDiFDQBx5LgIX-F) on how to use the `devcontainer.json` spec with DevPod 
and realized that I could create a custom devpod using [Features](https://devpod.sh/docs/features) to install the packages.
Features aren't available for all the packages that I wanted to use and there are some other configuration settings that need to be done, so I wrote an [install.sh](https://github.com/beckitrue/dotfiles/blob/main/install.sh) script to make those changes. Now, everything I need to get `nvim` up and running is done when the devpod is created.

There are some issues that surfaced here, such as using `apt install neovim` Feature installs an old version of 
neovim that doesn't work with my Lazy configuration. However, there is a Feature that uses the source 
code instead of `apt`, and that one works. 

Using these Features makes me wonder how secure they are, which is always a question about community-supported software. 
Probably best to check out the source code before using them in a production environment.

## The DevPod

I'm testing using the same [dotfiles](https://beckitrue/dotfiles) that I use on my local machine.
I didn't make any changes since this is a PoC. But, for a real use case I would have dotfiles
for the specific environment. 

For example, this devpod is using a `go` image, but in my neovim configration files I load Python 
and Node LSPs. This results in a (non-fatal) error message when running neovim on this devpod.

## What I've Learned

- I liked working with the `devcontainer.json` file and the devpod cli better than the DevPod UI. I found it easier to understand.
- Neovim in the DevPod was just like running from my local machine. I didn't notice any difference.
- I can see the value of having a standard development environment that is portable. This would be great for use in training 
  courses or for onboarding new developers.
- I need to do a bit more to complete the configuration like installing the dotfiles and setting up the environment variables.
- I would like to experiment some more with the `devcontainer.json` file to see if I can get the devpod to load all the 
  packages that I need.
- I suspect that I would need to write a custom Feature to install some of the packages that I need.
- I'd like to experiment with some other DevPod providers, such as Kubernetes, and AWS.
