# Maintainer: Adrià Cereto i Massagué <ssorgatem at gmail.com>
# Contributor: Daniel Bermond < yahoo-com: danielbermond >

pkgname=wine-staging-git
pkgver=3.8.r0.geb684dd9+wine.3.8.r0.g7280f7fb74
pkgrel=1
pkgdesc='A compatibility layer for running Windows programs (staging branch, git version) with Vulkan patches'
arch=('i686' 'x86_64')
url='https://www.wine-staging.com/'
license=('LGPL')
_depends=(
    'attr'                  'lib32-attr'
    'fontconfig'            'lib32-fontconfig'
    'lcms2'                 'lib32-lcms2'
    'libxml2'               'lib32-libxml2'
    'libxcursor'            'lib32-libxcursor'
    'libxrandr'             'lib32-libxrandr'
    'libxdamage'            'lib32-libxdamage'
    'libxi'                 'lib32-libxi'
    'gettext'               'lib32-gettext'
    'freetype2'             'lib32-freetype2'
    'glu'                   'lib32-glu'
    'libsm'                 'lib32-libsm'
    'gcc-libs'              'lib32-gcc-libs'
    'libpcap'               'lib32-libpcap'
    'desktop-file-utils'
)
makedepends=('git' 'autoconf' 'ncurses' 'bison' 'perl' 'fontforge' 'flex'
    'gcc>=4.5.0-2'
    'giflib'                'lib32-giflib'
    'libpng'                'lib32-libpng'
    'gnutls'                'lib32-gnutls'
    'libxinerama'           'lib32-libxinerama'
    'libxcomposite'         'lib32-libxcomposite'
    'libxmu'                'lib32-libxmu'
    'libxxf86vm'            'lib32-libxxf86vm'
    'libldap'               'lib32-libldap'
    'mpg123'                'lib32-mpg123'
    'openal'                'lib32-openal'
    'v4l-utils'             'lib32-v4l-utils'
    'alsa-lib'              'lib32-alsa-lib'
    'libxcomposite'         'lib32-libxcomposite'
    'mesa'                  'lib32-mesa'
    'libgl'                 'lib32-libgl'
    'opencl-icd-loader'     'lib32-opencl-icd-loader'
    'libxslt'               'lib32-libxslt'
    'libpulse'              'lib32-libpulse'
    'libva'                 'lib32-libva'
    'gtk3'                  'lib32-gtk3'
    'gst-plugins-base-libs' 'lib32-gst-plugins-base-libs'
    'vulkan-icd-loader'     'lib32-vulkan-icd-loader'
    'sdl2'                  'lib32-sdl2'
    'samba'
    'opencl-headers'
)
optdepends=(
    'giflib'                'lib32-giflib'
    'libpng'                'lib32-libpng'
    'libldap'               'lib32-libldap'
    'gnutls'                'lib32-gnutls'
    'mpg123'                'lib32-mpg123'
    'openal'                'lib32-openal'
    'v4l-utils'             'lib32-v4l-utils'
    'libpulse'              'lib32-libpulse'
    'alsa-plugins'          'lib32-alsa-plugins'
    'alsa-lib'              'lib32-alsa-lib'
    'libjpeg-turbo'         'lib32-libjpeg-turbo'
    'libxcomposite'         'lib32-libxcomposite'
    'libxinerama'           'lib32-libxinerama'
    'ncurses'               'lib32-ncurses'
    'opencl-icd-loader'     'lib32-opencl-icd-loader'
    'libxslt'               'lib32-libxslt'
    'libva'                 'lib32-libva'
    'gtk3'                  'lib32-gtk3'
    'gst-plugins-base-libs' 'lib32-gst-plugins-base-libs'
    'vulkan-icd-loader'     'lib32-vulkan-icd-loader'
    'sdl2'                  'lib32-sdl2'
    'cups'
    'samba'
    'dosbox'
)
options=('staticlibs')
install="$pkgname".install
source=('wine-git'::'git+https://github.com/wine-mirror/wine.git'
        "wine-staging"::'git+https://github.com/wine-staging/wine-staging.git'
	'wine-pba'::'git+https://github.com/firerat/wine-pba.git#branch=heap_size_envvars'
        'gallium9'::'git+https://github.com/sarnex/wine-d3d9-patches.git'
        'fallout4.patch'
        'pathofexile.patch'
        'harmony-fix.diff'
        '30-win32-aliases.conf'
        'wine-binfmt.conf')
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
	    'SKIP'
            'SKIP'
            'SKIP'
            '50ccb5bd2067e5d2739c5f7abcef11ef096aa246f5ceea11d2c3b508fc7f77a1'
            '9901a5ee619f24662b241672a7358364617227937d5f6d3126f70528ee5111e7'
            '6dfdefec305024ca11f35ad7536565f5551f09119dda2028f194aee8f77077a4')

if [ "$CARCH" = 'i686' ] 
then
    # strip lib32 etc. on i686
    _depends=("${_depends[@]/*32-*/}")
    makedepends=("${makedepends[@]/*32-*/}" "${_depends[@]}")
    optdepends=("${optdepends[@]/*32-*/}")
    provides=(
        "wine=$(        printf '%s' "$pkgver" | sed 's/.*\+wine\.//')"
        "wine-git=$(    printf '%s' "$pkgver" | sed 's/.*\+wine\.//')"
        "wine-staging=$(printf '%s' "$pkgver" | sed 's/\+wine.*//')"
    )
    conflicts=('wine' 'wine-git' 'wine-staging')
else
    makedepends=("${makedepends[@]}" "${_depends[@]}")
    provides=(
        "wine=$(        printf '%s' "$pkgver" | sed 's/.*\+wine\.//')"
        "wine-wow64=$(  printf '%s' "$pkgver" | sed 's/.*\+wine\.//')"
        "wine-git=$(    printf '%s' "$pkgver" | sed 's/.*\+wine\.//')"
        "wine-staging=$(printf '%s' "$pkgver" | sed 's/\+wine.*//')"
    )
    conflicts=('wine' 'wine-wow64' 'wine-git' 'wine-staging')
fi

prepare() {
    cd "${srcdir}"/wine-staging
    git reset --hard HEAD      # restore tracked files
    git clean -xdf             # delete untracked files
    git checkout tags/v3.8     # version checkout
    
    cd "${srcdir}"/gallium9
    git reset --hard HEAD      # restore tracked files
    git clean -xdf             # delete untracked files
    git checkout tags/wine-d3d9-3.8     # version checkout

    cd "${srcdir}"/wine-pba
    git reset --hard HEAD      # restore tracked files
    git clean -xdf             # delete untracked files
    git checkout tags/3.7      # version checkout

    cd "${srcdir}"/wine-git
    # restore the wine tree to its git origin state, without wine-staging patches
    # (necessary for reapllying wine-staging patches in succedent builds,
    # otherwise the patches will fail to be reapplied)
    msg2 'Cleaning wine source code tree...'
    git reset --hard HEAD      # restore tracked files
    git clean -xdf             # delete untracked files
    git checkout "$(../wine-staging/patches/patchinstall.sh --upstream-commit)"     # version checkout

    # fix path of opencl headers
    sed 's|OpenCL/opencl.h|CL/opencl.h|g' -i configure*
        
    # freetype harmony fix
    echo "***freetype harmony fix***"
    patch -Np1 < ../harmony-fix.diff
    
    # fix fallout 4
    echo "***fallout 4 fix***"
    patch -Np1 < ../fallout4.patch

    # fix path of exile
    echo "***path of exile fix***"
    patch -Np1 < ../pathofexile.patch
    
    #fix xaudio2 
    git revert --no-commit b747d6f6ccdf1699a9242a570d681fa246de592e
    
    # then apply staging patches
    echo "***staging patches***"
    ../wine-staging/patches/patchinstall.sh --all

    # add pba patches
    echo "***pba patches***"
    for _f in ../wine-pba/patches/00*.patch; do
        echo "applying ${_f##*/}"
        patch -Np1 <  "${_f}"
    done
    
    # gallium 9
    echo "starting g9 staging helper"
    patch -Np1 < ../gallium9/staging-helper.patch

    echo "starting g9 patches"
    patch -Np1 < ../gallium9/wine-d3d9.patch

    autoreconf -f

}

pkgver() {
    cd "${srcdir}"/wine-staging
    local _staging_tag="$(git tag --sort='version:refname' | tail -n1 | sed 's/-/./g;s/^v//;s/\.rc/rc/')"
    local _staging_version="$(git describe --long --tags \
                                | sed 's/\([^-]*-g\)/r\1/;s/-/./g;s/^v//;s/\.rc/rc/' \
                                | sed "s/^latest.release/${_staging_tag}/")"
    cd "${srcdir}"/wine-git
    local _wine_version="$(git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g;s/^v//;s/\.rc/rc/')"
    
    printf '%s+%s' "$_staging_version" "$_wine_version"
}

build() {    
    # delete old build dirs (from previous builds) and make new ones
    rm    -rf wine-staging-{32,64}-build
    mkdir -p  wine-staging-32-build

    # workaround for FS#55128
    # https://bugs.archlinux.org/task/55128
    # https://bugs.winehq.org/show_bug.cgi?id=43530
    export CFLAGS="${CFLAGS/-fno-plt/}"
    export LDFLAGS="${LDFLAGS/,-z,now/}"
    
    # build wine-staging 64-bit
    # (according to the wine wiki, this 64-bit/32-bit building order is mandatory)
    if [ "$CARCH" = "x86_64" ] 
    then
        msg2 'Building Wine-64...'
        mkdir -p wine-staging-64-build
        cd "${srcdir}"/wine-staging-64-build
        ../wine-git/configure \
                        --prefix='/usr' \
                        --libdir='/usr/lib' \
                        --with-x \
                        --with-gstreamer \
                        --enable-win64 \
                        --with-xattr
        make
        local _wine32opts=(
                    '--libdir=/usr/lib32'
                    "--with-wine64=${srcdir}/wine-staging-64-build"
        )
        export PKG_CONFIG_PATH='/usr/lib32/pkgconfig'
    fi
    
    # build wine-staging 32-bit
    msg2 'Building Wine-32...'
    cd "${srcdir}"/wine-staging-32-build
    ../wine-git/configure \
                    --prefix='/usr' \
                    --with-x \
                    --with-gstreamer \
                    --with-xattr \
                    "${_wine32opts[@]}"
    make
}

package() {
    depends=("${_depends[@]}")
    
    # package wine-staging 32-bit
    # (according to the wine wiki, this reverse 32-bit/64-bit packaging order is important)
    msg2 'Packaging Wine-32...'
    cd "${srcdir}"/wine-staging-32-build
    
    if [ "$CARCH" = 'i686' ] 
    then
        make prefix="${pkgdir}/usr" install
    else
        make prefix="${pkgdir}/usr" \
             libdir="${pkgdir}/usr/lib32" \
             dlldir="${pkgdir}/usr/lib32/wine" install
        
        # package wine-staging 64-bit
        msg2 'Packaging Wine-64...'
        cd "${srcdir}"/wine-staging-64-build
        make prefix="${pkgdir}/usr" \
             libdir="${pkgdir}/usr/lib" \
             dlldir="${pkgdir}/usr/lib/wine" install
    fi
    
    # font aliasing settings for Win32 applications
    install -d "$pkgdir"/etc/fonts/conf.{avail,d}
    install -m644 "${srcdir}/30-win32-aliases.conf" "${pkgdir}/etc/fonts/conf.avail"
    ln -s ../conf.avail/30-win32-aliases.conf       "${pkgdir}/etc/fonts/conf.d/30-win32-aliases.conf"
    
    # wine binfmt
    install -D -m644 "${srcdir}/wine-binfmt.conf"   "${pkgdir}/usr/lib/binfmt.d/wine.conf"
}
