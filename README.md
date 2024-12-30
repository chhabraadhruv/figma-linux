# figma-linux
Guide to Installing Figma on your Linux Desktop

Here's a comprehensive guide with all the necessary bash commands to install Figma on Ubuntu:

First, make sure Chrome is installed. If not, install it:

bashCopy# Add Chrome's repository and key
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

# Update package list and install Chrome
sudo apt update
sudo apt install google-chrome-stable

Create a directory for Figma in your Applications folder:

bashCopymkdir -p ~/.local/share/applications

Check if Chrome is properly installed and get its version:

bashCopygoogle-chrome --version

Install required dependencies for Chrome and PWAs:

bashCopysudo apt install -y libappindicator1 libindicator7

Install font dependencies (Figma uses various fonts):

bashCopy# Create fonts directory if it doesn't exist
mkdir -p ~/.fonts

# Install Microsoft fonts (optional but recommended)
sudo apt install -y ttf-mscorefonts-installer

# Update font cache
fc-cache -f -v

Launch Chrome and install Figma as PWA:

bashCopygoogle-chrome --app=https://www.figma.com

To make Figma run smoother, you can increase the amount of inotify watchers:

bashCopy# Check current limit
cat /proc/sys/fs/inotify/max_user_watches

# Increase the limit
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

To ensure Figma has access to your system clipboard:

bashCopy# Install xclip for clipboard support
sudo apt install -y xclip
After installation:

Open Chrome and go to Figma.com
Sign in to your account
Click the install icon in the address bar (or three dots menu → Install Figma)
Accept the installation

To launch Figma in the future, you can either:

Use the Ubuntu applications menu
Create an alias in your ~/.bashrc:

bashCopyecho 'alias figma="google-chrome --app=https://www.figma.com"' >> ~/.bashrc
source ~/.bashrc
Then you can launch Figma by typing:
bashCopyfigma
Troubleshooting commands:
bashCopy# Check if Chrome is running properly
ps aux | grep chrome

# Check Chrome's crash logs
cat ~/.config/google-chrome/chrome_debug.log

# Clear Chrome's cache and data if needed
rm -rf ~/.cache/google-chrome/
rm -rf ~/.config/google-chrome/Default/Cache
If you have any issues with fonts not showing up:
bashCopy# Install font manager for better font handling
sudo apt install font-manager

# Check installed fonts
fc-list

# Rebuild font cache
sudo fc-cache -f -v
