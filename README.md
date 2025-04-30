# 5Skyes Shownet
A collection of scripts for [Bitfocus Companion](https://bitfocus.io/) and Open Stage Control for synchronizing several live events control systems via OSC, REST, and more. 
It is a two part system, with Open Stage Control generating a webserver with a GUI and issuing generic OSC messages and Bitfocus Companion interperating these OSC calls. Companion then leverages it's module library to ubdate outboard systems, such as media servers (Resolume) , Lighting desks (MA2/MA3) , and Lasers (Beyond).

## NOTES

 - These tools require some familiarity with IP systems, and a reasonable knowledge of the various communication methods live event tools tend to use for remote control. If you're a little iffy, now's a great time to brush up. [TODO: HELPFUL RESOURCES]
 - This repository draws directly from our live build of this tool as we use it in production. Therefore, it will have features and components which are not applicable to your usecase, and may be broken, unstable, or nonfunctional. We will largely only be updating it when we tweak it for our own gigs, and have no plans to create a generic version at this time (which wouldn't help you anyway). Support is _unlikely._ If you want to fork it, give it a shot, let us know how it goes.
 - While my work in the scripts I've written is under MIT license, the programs that run them aren't. They have their own licenses and their own requirements. The files here have been generated using those tools, so may not even be MIT in their own right - therefore, these scripts are licensed under whatever the least permissive license is, falling back to MIT.

## INSTALLATION

 - [Download and Install Bitfocus Companion](https://bitfocus.io/) (Free account required). These scripts use a version of the [Generic OSC module (v2.6.0)](https://github.com/bitfocus/companion-module-generic-osc/releases/tag/v2.6.0) which is not in the mainline build, [so you'll have to install that yourself.](https://github.com/bitfocus/companion/wiki/How-to-use-a-module-that-is-not-included-in-Companion-build) When that's done, launch the GUI and head to the `import / export` tab. Import `5s_shownet_companion_v1.companionconfig` from the `./configs/` directory.

- [Download and Install Open Stage Control.](https://openstagecontrol.ammd.net/) This is the GUI for the system, stylized here as osControl to avoid confusion with the OSC protocol. From the three-dot menu next to the play / stop button (stop it if it boots running), open `5s_shownet_OSC_config_v1.config`, then make sure the `load` dialogue in the interface has found `5s_shownet_OSC_UI_v1.json`. 

- configure you IP and port settings in osControl and Companion. These vary by machine and usecase, and will need to be tweaked to use the correct settings for your network, the clients on it, and to avoid port collisions if these scripts aren't sandboxed to a separate machine. If that's the case, you'll definitely need to move around ports - the default is 8080, but every piece of gear needs unique ports - one in and one out minimum depending on the Companion module implementation for your system. Some other common tools can also bork things easily - NDI & Synergy KVM, for example. 8080 and 8000 are the default ports for a good range of applications, so when in doubt, change it (but netstat that sh1t)

 - Roll your own ! This is a great platform for adding your own tooling. It's not a full boilerplate, but if you look at how we've implemented the Resolume, MA3, and Beyond module triggers you'll get a good idea of what's possible. Companion isn't really designed to be used as a middleman like this - it much prefers to be a shotcaller, so you'll run into issues and have to work around them. Same thing with certain modules - the resolume module has inconsistent implementation in some of its variable handling. The OSC module is literally not in the public release. It's stable, but. A Bit Beta in places.

 - Good Luck ! 5s <3