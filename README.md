# custom-build-linux-iso
Red Hat Style Exam Linux
Custom lightweight exam Linux project for Red Hat/RHEL-family training labs.

Recommended base:

Rocky Linux 9 or AlmaLinux 9
RPM packages
dnf and yum command compatibility
SELinux, firewalld, systemd, NetworkManager
VMware-friendly guest tools
Goal
Build a branded ISO that students can boot in VMware for exams and practice.

Target behavior:

Live exam mode
Optional installer mode
Student user environment
Lightweight desktop
Branded boot/menu/wallpaper text
Red Hat style commands and tools
Important Build Note
Build this ISO from a Rocky/Alma/RHEL-family machine or VM, not directly from macOS.

Recommended builder VM:

Rocky Linux 9
4 CPU cores
8 GB RAM minimum
60 GB free disk
Internet access
Project Layout
.
├── kickstarts/
│   └── rocky9-exam-live.ks
├── scripts/
│   └── build-rocky9-live.sh
└── branding/
    └── README.md
First Build
Inside a Rocky Linux 9 builder VM:

sudo dnf install -y lorax livemedia-creator pykickstart anaconda \
  anaconda-tui anaconda-gui
sudo bash scripts/build-rocky9-live.sh
The expected output will be created under:

build-results/
Default Student Login
Initial lab values:

Username: student
Password: student
Root password: redhat
Change these before giving the ISO to real students.

Branding
Edit the values in:

kickstarts/rocky9-exam-live.ks
branding/
Current placeholder name:

Nirbhai Exam Linux
You can replace this with your final institute/course name.

Next Steps
Test the base ISO in VMware.
Confirm whether live mode needs internet or only a specific exam website.
Add lockdown rules for terminal, browser, clipboard, USB, or network as required.
Replace placeholder branding files with final logo and wallpaper.
