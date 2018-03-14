# ge-wine
My personal all in one wine build.  

Contains an arch pkgbuild with the following:  

# Staging:  
-staging upstream patches  
-staging vulkan patches re-enabled  

# Gallium Nine:  
-gallium 9 upstream patches  
-temporary patch to allow gallium 9 to compile with staging upstream  

# PBA:  
-acommenos pba patches  
-ffxiv heap patch for pba  

# Vulkan(temporary):  
-patches to remove curren wine-vulkan (roderickc's vulkan patches)  
-patches to re-add wine-staging's vulkan patches  

# Game fixes:  
-fallout 4 loading patch and lod patch  
-wolfenstein 2 loading patch and staging vulkan patch  
-harmony-fix patch  

Note: this is only an Arch package with PKGBUILD and files necessary to compile on arch via makepkg. For other distros please see prepare/build sections of PKGBUILD  

