#!/bin/bash

# Ensure script is run with root privileges
if [ "$EUID" -ne 0 ]; then
  echo "Please run as root or with sudo"
  exit 1
fi

# Detect Operating System using /etc/os-release
if [ -f /etc/os-release ]; then
    . /etc/os-release
    OS=$ID
else
    echo "Cannot detect OS: /etc/os-release not found."
    exit 1
fi

case "$OS" in
    ubuntu|debian)
        echo "Detected OS: $NAME"
        echo "Updating package lists and installing software..."
        
        apt-get update -y
        # Add your Ubuntu packages below:
        apt-get install -y curl git htop
        
        # Verification check
        if [ $? -eq 0 ]; then
            echo "Installation completed successfully on $NAME."
        else
            echo "Installation failed."
            exit 1
        fi
        ;;

    centos|rhel|rocky|almalinux)
        echo "Detected OS: $NAME"
        echo "Installing software..."
        
        # Uses dnf if available, falls back to yum
        PKG_MANAGER=$(command -v dnf || command -v yum)
        
        # Add your CentOS packages below:
        $PKG_MANAGER install -y curl git htop
        
        # Verification check
        if [ $? -eq 0 ]; then
            echo "Installation completed successfully on $NAME."
        else
            echo "Installation failed."
            exit 1
        fi
        ;;

    *)
        echo "Unsupported OS: $OS"
        exit 1
        ;;
esac
