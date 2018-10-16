# My Dotfiles.

![Archlinux Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Archlinux-vert-dark.svg/1280px-Archlinux-vert-dark.svg.png)

This repository contains all the things [Antoine Neveux](https://github.com/aneveux) is using in order to set up his development environment. This is just a fork of his main repo in order to get this working on ARM machines.

This branch is dedicated to the fabulous [XU4](https://www.hardkernel.com/main/products/prdt_info.php) machine.

A few packages were not available, so that I had to rebuild them (even if some of them are not ARM specific. Go figure. I know nothing about [ArchLinux](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu4), just in case you were wondering).

Just clone the repo, issue `makepkg` and then `pacman -U resulting-package.tar.xz`.

To be totally honest, I had to tweak here and there to allow the build to happen (because armv7h is not planned for these packages). If you were ever lost at that, just create an issue in this repo.

|Name                                  |Version                       | URL                        |
|--------------------------------------|------------------------------|----------------------------|
|ttf-font-awesome                      |4-4.7.0                       |https://aur.archlinux.org/ttf-font-awesome-4.git|
|ttf-font-icons                        |1.1-1-any                     |https://aur.archlinux.org/ttf-font-icons.git|
|nerd-fonts-complete                   |2.0.0-5-any                   |https://aur.archlinux.org/nerd-fonts-complete.git|
|ttf-unifont                           |11.0.02-1-any                 |https://aur.archlinux.org/ttf-unifont.git|
|dropbox                               |58.4.92-1-armv7h              |https://aur.archlinux.org/dropbox.git|
|xflux                                 |20130901-5-armv7h             |https://aur.archlinux.org/xflux.git|
|cower                                 |18-1-aarch64                  |https://aur.archlinux.org/cower.git|


## Operating System.

I've no yet been converted to [Archlinux](https://www.archlinux.org/) by [@ThomasFerreira](https://github.com/ThomasFerreira/), but I'm working on it.

This repository doesn't intend to deal with the whole Operating System installation, so I'll instead let you rely on the [awesome installation guide from Arch Linux ARM website](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu4)!

But as soon as you have a running system (by the end of the wiki page actually), you'll be able to use this repository! There is a small playbook provided in the `playbooks` directory allowing to let you deal with the *locale* and *user* creation. If you never played with Ansible, have a look at the `install.sh` script to get examples of how to use the `ansible-playbook` command.

Once your user is created, you can directly run the installation script :)

## Customizing the dotfiles.

I'm using a particular variables loader allowing you to override some properties of the playbooks! All you have to do is create a `local` folder at the root of the repository, and put a `local.yml` file in it. You can then customize values used to provision the system!

Here's an example of a `local/local.yml` file you could be using:

```yml
---
usr:
  id: john_doe
  name: John Doe
  mail: john@doe.org
  gpg_key: ABCDEFXXXXX
  preferences:
    shell: /usr/bin/zsh
    xsession: i3
    keymap: fr
    locales:
      - "en_US.UTF-8"

sys:
  proxy:
    enabled: False
    host: none
    port: 0
    noproxy: none
  preferences:
    sudo_nopassword: yes
```

Basically, it allows you to customize your user's information, as well as the shell you'd like to use, or the keymap and locales to use.

Please note that it is a bit linked to what's in the playbooks though. For example, I'm only provisioning i3 as a window manager, so if you put gnome or kde here, it won't work instead you actually install and configure it yourself ;)

Do not hesitate to have a look at `inventory/localhost.yml` as well. It is the main inventory for these playbooks, and contains all the information used to provision the environment.

## Provisioning the environment.

This repository comes with a small shell script allowing to easily run the Ansible playbooks! Simply run `./install.sh all` to provision everything in one command line!

If you'd like to only provision a particular tool, you can simply name it like this: `./install.sh git` for example.

The provided shell script allows to dry run the execution as well so you can have a look at the changes it would cause on your environment.

## Updating some files.

These playbooks are idempotent. Which means you can run them again and again and they won't do anything if nothing has changed on your system.

To update anything, simply do the modifications in this repository, and run the provisioning again, it'll simply modify the things which changed ;)

## Resources I use.

- [Archlinux](https://www.archlinux.org/) - My favorite Linux distribution for a development environment!
   - Note that you could have a look at [Manjaro](https://manjaro.org/) if you struggle with Arch installation ;)
- [zsh](http://www.zsh.org/) - The shell I'm using, even though I'm still switching to fish once in a while.
- [oh-my-zsh](http://ohmyz.sh/) - Making zsh a bit easier to extend :)
- [fish shell](http://fishshell.com/) - A really friendly shell I'm sometimes using.
- [oh-my-fish](https://github.com/oh-my-fish/oh-my-fish) - Kinda similar to *oh-my-zsh* but for fish.
- [git](https://git-scm.com/) - I love Git.
- [i3-gaps](https://github.com/Airblader/i3) - A fork of *i3wm* which I love. I never found a better window manager ever.
- [atom](https://atom.io/) - I'd like to use vim more but I'm still kinda bad with it.
- [terminal sexy](http://terminal.sexy/) - For nice terminal color schemes
- [rofi](https://davedavenport.github.io/rofi/) - A powerful window switcher!
- [IntelliJ IDEA](https://www.jetbrains.com/idea/) - my favourite IDE,

And some useless, but absolutely necessary resources:

- [Table flipping emoticons](http://japaneseemoticons.me/table-flipping-emoticons/) - cause commit messages,
- [Shields](http://shields.io/) - cause opensource projects are all doing it,
- [Commit Message](http://whatthecommit.com/) - when you lack inspiration,

## Thanks!

I really wanted to thank a lot all those really nice people/projects for the great inspiration:

- [Jean-Marc Desprez](https://github.com/jmdesprez)
- [Thomas Ferreira](https://github.com/ThomasFerreira)
- [GitHub does dotfiles](https://dotfiles.github.io/)
- [Mathias Bynens' dotfiles](https://github.com/mathiasbynens/dotfiles)
- [dotbot](https://github.com/anishathalye/dotbot)
- [Airblader's dotfiles](https://github.com/Airblader/dotfiles-manjaro)
- [eoli3n](https://github.com/eoli3n/dotfiles)
