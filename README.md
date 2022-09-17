# arch-steamcmd-wine

AS ROOT

#enable multilib
printf "\n[multilib]\nInclude = /etc/pacman.d/mirrorlist">> /etc/pacman.conf

pacman -Syyu
pacman -S git vi xorg-server-xvfb sudo base-devel wine-staging winetricks giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo libxcomposite lib32-libxcomposite libxinerama lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader cups samba dosbox

useradd -m steam
passwd steam

usermod -aG wheel steam
sed -i '/%wheel\ ALL=(ALL)\ ALL/s/^#//' /etc/sudoers





AS STEAM

sudo -u steam -s

cd /home/steam

git clone https://aur.archlinux.org/steamcmd.git
cd steamcmd
makepkg -si
mkdir -p ~/space-engineers/SpaceEngineersDedicated
cd ..
steamcmd +quit
steamcmd +force_install_dir ~/space-engineers/SpaceEngineersDedicated +login anonymous +@sSteamCmdForcePlatformType windows +app_update 298740 +quit

Xvfb :5 -screen 0 1024x768x16 &
env WINEARCH=win64 WINEDEBUG=-all WINEPREFIX=/home/steam/wineserver WINEDLLOVERRIDES="mscoree=d" wineboot --init /nogui 
env WINEARCH=win64 WINEDEBUG=-all WINEPREFIX=/home/steam/wineserver winetricks corefonts 
env WINEARCH=win64 WINEDEBUG=-all WINEPREFIX=/home/steam/wineserver winetricks sound=disabled 
env WINEARCH=win64 WINEDEBUG=-all WINEPREFIX=/home/steam/wineserver DISPLAY=:5.0 winetricks -q vcrun2019 
env WINEARCH=win64 WINEDEBUG=-all WINEPREFIX=/home/steam/wineserver DISPLAY=:5.0 winetricks -q --force dotnet48




env WINEARCH=win64 WINEDEBUG=-all WINEPREFIX=/home/steam/wineserver DISPLAY=:5.0 wine SpaceEngineersDedicated.exe -noconsole -ignorelastsession



wine SpaceEngineersDedicated.exe -noconsole -ignorelastsession -path Z:\\home\\steam\\space-engineers\\
