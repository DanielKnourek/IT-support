## How to mount any USB device in WSL2

𝗧𝗼 𝗶𝗻𝘀𝘁𝗮𝗹𝗹 𝗼𝗻 𝗪𝗶𝗻𝗱𝗼𝘄𝘀 𝟭𝟬 𝗮𝗻𝗱 𝗪𝗦𝗟𝟮 𝗨𝗯𝘂𝗻𝘁𝘂 𝟭𝟴.𝟬𝟰:
1. PowerShell as admin:

wsl --update
winget install --interactive --exact dorssel.usbipd-win
usbipd wsl list
usbipd wsl attach --busid <busid>

2. WSL2:

sudo apt update
sudo apt upgrade
sudo adduser <user> dialout
sudo apt install linux-tools-5.4.0-77-generic hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/5.4.0-77-generic/usbip 20
sudo cp contrib/60-openocd.rules /etc/udev/rules.d/
sudo udevadm control --reload

Now I'm able to read serial with:
sudo screen /dev/ttyACM0

Hope it helps!

YT video 
<https://www.youtube.com/watch?v=I2jOuLU4o8E>
