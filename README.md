# Standard Ruby Server Stack Installer
This is the repository to store my scripted ruby runner server installer.  

This stack of ruby servers runner was made to ease the install of ruby private cloud servers.  

# How to install
Clone this repository, run `make` under a terminal and inspect the generated file (`./install_me.sh`): after checking the generated script, if you agree with its content and it fits your policies of server configurations, run it in a clean install debian-based server you want to use to run your rails applications.  

# What is going to be installed
The script is going to install RVM (https://rvm.io/) and NVM (https://nvm.sh/), creating an `application_users` unix group and a special `ruby-manager` unix user used for maintenance operations or deploy.  
Installed and configured are the Apache2 web server (https://httpd.apache.org/) and the Memcache server (https://memcached.org/) with some predefined configurations and tuning.  
Others softwares are installed by default using `apt`, please check the generated code before running it in your instances.  

# How it works
Some helper scripts are installed in the bash shell environment, allowing to automate the administrations steps.  
The helpers will create default settings for users to be used as deamons to run Rails applications.  
Every users will have a memcached private instance, an Apache2 entry for the static pages and the assets plus the ability to create gemsets and install rubies interpreters and gems.  

# How to use it
The script install some bash functions in the `/etc/profile.d/` directory as to be accessible to any server user:  
- addRubyUser $1 $2  
- - This is a standard bash function, will take a name as first parameter (ex: user-rail-1) and an isolation level as a second parameter (ex: demo), the resulting rails daemon of the given example user will be `user-rails-1_demo` and will have a dedicated home into a `application_users` grouped home under `/opt` to isolate them from normal users homes (ex: `/opt/ruby-users/user-rails-1_demo`)  
- addRubyMaintener  
- - Given the running user is a `sudoer`, it promotes himself to the same rola as the `rail-manager` users allowing him to operate maintenace and deploy of served rails instances.

# Release note
Be sure to not have a ruby version manager already installed nor any ruby interpreter at all.  
This script is intended to be used on a __clean debian-based server install__ and should be used in conjonction with rails projects configured using the `railsStandardSetup` gem also sourced in the same Github repository as this software.

# Disclaimer
All rights reserved to the authors of the cited software and trademarks in this document and anywhere in the code of this repository. This is only a set of scripts driving a set of tools I do not own and not going to distribute: you have to go yourself find them and install them on your box.

This SOFTWARE is provided "as is" and "with all faults".  
THE PROVIDER makes no representations or warranties of any kind concerning the safety, suitability, lack of viruses, inaccuracies, typographical errors, or other harmful components of this SOFTWARE.  
There are inherent dangers in the use of any software, and you are solely responsible for determining whether this SOFTWARE is compatible with your equipment and other software installed on your equipment.  
You are also solely responsible for the protection of your equipment and backup of your data, and THE PROVIDER will not be liable for any damages you may suffer in connection with using, modifying, or distributing this SOFTWARE.  

Lets says it AGAIN: the script is given to the community AS IS and I won't be responsible for any damage it may result from their usage on any system or systems.  
*Always* inspect the code before running it to check if it fits with the target configuration and take *your* responsability when you decide to run it.  
