# Figma Installation Guide for Ubuntu
A comprehensive guide for installing and configuring Figma as a Progressive Web App (PWA) on Ubuntu using Google Chrome.

## Prerequisites
- Ubuntu Operating System
- Administrator privileges
- Active internet connection

## Installation Steps

### 1. Installing Google Chrome
If Chrome isn't already installed, run these commands:
```bash
# Add Chrome's repository and key
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

# Update package list and install Chrome
sudo apt update
sudo apt install google-chrome-stable
```

### 2. Setting Up Required Directories and Dependencies
```bash
# Create necessary directories
mkdir -p ~/.local/share/applications
mkdir -p ~/.fonts

# Install required dependencies
sudo apt install -y libappindicator1 libindicator7

# Install Microsoft fonts (optional but recommended)
sudo apt install -y ttf-mscorefonts-installer

# Update font cache
fc-cache -f -v
```

### 3. System Optimization
```bash
# Increase inotify watchers for better performance
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

# Install clipboard support
sudo apt install -y xclip
```

### 4. Installing Figma as PWA
1. Launch Chrome with Figma:
```bash
google-chrome --app=https://www.figma.com
```
2. Sign in to your Figma account
3. Click the install icon in the address bar (or three dots menu → Install Figma)
4. Accept the installation

### 5. Quick Launch Setup (Optional)
Add an alias to your `~/.bashrc`:
```bash
echo 'alias figma="google-chrome --app=https://www.figma.com"' >> ~/.bashrc
source ~/.bashrc
```

## Troubleshooting

### Font Issues
```bash
# Install font manager
sudo apt install font-manager

# Check installed fonts
fc-list

# Rebuild font cache
sudo fc-cache -f -v
```

### Chrome Issues
```bash
# Check Chrome processes
ps aux | grep chrome

# View Chrome crash logs
cat ~/.config/google-chrome/chrome_debug.log

# Clear Chrome cache and data
rm -rf ~/.cache/google-chrome/
rm -rf ~/.config/google-chrome/Default/Cache
```

## Additional Configuration

### Chrome Settings for Figma
1. Open Chrome settings
2. Navigate to Privacy and security → Site Settings → Additional permissions → Fonts
3. Enable "Sites can use their own fonts"
4. Add Figma (figma.com) to allowed sites

## Post-Installation
- Log out and log back in (or restart your system) to ensure all changes take effect
- Figma can be launched from:
  - Ubuntu applications menu
  - Terminal using the `figma` command (if alias was set up)
  - Dock (if pinned)

## Support
If you encounter any issues, please:
1. Check your Chrome version: `google-chrome --version`
2. Verify all dependencies are installed
3. Ensure your system is up to date: `sudo apt update && sudo apt upgrade`

## Contributing
Feel free to contribute to this guide by submitting issues or pull requests.

## License
This guide is available under the MIT License. Feel free to modify and distribute as needed.
