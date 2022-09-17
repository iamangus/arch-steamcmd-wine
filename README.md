# arch-steamcmd-wine

AS ROOT

#enabling color and candy
sed -i '/Color/s/^#//' /etc/pacman.conf
sed -i '/Color/a ILoveCandy' /etc/pacman.conf

#enable multilib
printf "\n[multilib]\nInclude = /etc/pacman.d/mirrorlist">> /etc/pacman.conf

pacman -Syyu
pacman -S git sudo base-devel wine-staging winetricks giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo libxcomposite lib32-libxcomposite libxinerama lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader cups samba dosbox

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
steamcmd +force_install_dir ~/space-engineers/SpaceEngineersDedicated +login anonymous +@sSteamCmdForcePlatformType windows +app_update 298740 +quit

git clone https://aur.archlinux.org/wine-ge-custom.git
cd wine-ge-custom/
makepkg -si


OR

git clone https://github.com/p-mng/proton-ge-custom-updater.git
cd proton-ge-custom-updater
ch



pacman-key --init
pacman-key --recv-key FBA220DFC880C036 --keyserver keyserver.ubuntu.com
pacman-key --lsign-key FBA220DFC880C036
pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
pacman -Sy
pacman -S wine-ge-custom


Append (adding to the end of the file) to /etc/pacman.conf:

[chaotic-aur]
Include = /etc/pacman.d/chaotic-mirrorlist



wine SpaceEngineersDedicated.exe -noconsole -ignorelastsession -path Z:\\home\\steam\\space-engineers\\\\
