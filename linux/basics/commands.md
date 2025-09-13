# Commands

## XBPS

Common commands for the X Binary Package System (XBPS):  
- `xbps-install -Su`: update the system  
- `xbps-install <package_name>`: install <package>  
- `xbps-install -A`: install a package temporarily, for evaluation. this package and its dependencies will be removed when `xbps-remove -o` is run  
- `xbps-query -Rs <query>`: search repositories for packages  
- `xbps-query -f <package>`: list files provided by <package>  
- `xbps-query -l`: list all packages with versions and descriptions  
- `xbps-query -l | cut -d " " -f 2 | sed "s/^\(.*\)-.*$/\1/"`: list all package names (might want to alias this)  
- `xbps-remove -R <package>`: remove a package and any of its dependendcies that are no longer needed  
- `xbps-remove -Oo`: remove orphan packages and clean the cache. will also remove packages installed with `xbps-install -A`  

## Other Useful Commands

- `flatpak install flathub <flathub_url>`: Install Flathub application  
  - From my understanding this is good for apps you want sandboxed on the system.  
