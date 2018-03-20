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
Note: use envar PBA_DISABLE=1 to disable PBA if need.  

Usage and details for ffxiv heap patch:  
--ffxiv does not like the heap sizes that the pba patches specify. To fix this, this patch adds __PBA_GEO_HEAP and __PBA_CB_HEAP envars. Suggested values for ffxiv dx9 mode is __PBA_GEO_HEAP=256 and __PBA_CB_HEAP=64  

# Game fixes:  
-fallout 4 loading patch and lod patch  
-wolfenstein 2 loading patch and staging vulkan patch  
-harmony-fix patch  
-strider patch to prevent strider from crashing  
-origin patch stops OriginWebHelper.exe from crashing  
-path of exile patch fixed WIC error in path of exile.  

Note: this is only an Arch package with PKGBUILD and files necessary to compile on arch via makepkg. For other distros please see prepare/build sections of PKGBUILD  

