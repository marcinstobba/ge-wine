fork for testing 3.8


# ge-wine
My personal all in one wine build. two branches: ge-wine and ge-wine-git. git is synced with latest staging upstream on all patch sources (unless something breaks that I can't fix). ge-wine is synced with latest staging release. 

Contains an arch pkgbuild with the following:  

# Staging:  
-staging upstream patches  

# Gallium Nine:  
-gallium 9 upstream patches  

# PBA:  
-acommenos pba patches  
-ffxiv heap patch for pba  
Note: use envar PBA_DISABLE=1 to disable PBA if need.  

Usage and details for ffxiv heap patch:  
--ffxiv does not like the heap sizes that the pba patches specify. To fix this, this patch adds __PBA_GEO_HEAP and __PBA_CB_HEAP envars. Suggested values for ffxiv dx9 mode is __PBA_GEO_HEAP=256 and __PBA_CB_HEAP=64  

# Game fixes:  
-fallout 4 loading patch and lod patch  
-harmony-fix patch  
-path of exile patch fixed WIC error in path of exile dx11 mode.  
-xaudio2 revert commit b747d6f6ccdf1699a9242a570d681fa246de592e which forces wine to use builtin xaudio2 instead of native, and breaks sound in a lot of games.  

Note: this is only an Arch package with PKGBUILD and files necessary to compile on arch via makepkg. For other distros please see prepare/build sections of PKGBUILD  
