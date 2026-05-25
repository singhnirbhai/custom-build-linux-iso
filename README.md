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

# Builder VM Steps
Use these steps on a fresh Rocky Linux 9 builder VM.

1. Create Builder VM
Recommended VM settings:

OS: Rocky Linux 9 x86_64
CPU: 4 cores
RAM: 8 GB
Disk: 60 GB
Network: NAT or bridged with internet
2. Install Build Tools
sudo dnf update -y
sudo dnf install -y epel-release
sudo dnf install -y lorax livemedia-creator pykickstart anaconda anaconda-tui anaconda-gui
3. Copy This Project Into The VM
Example path inside the builder VM:

/home/student/redhat-exam-linux
4. Build ISO
From the project folder:

sudo bash scripts/build-rocky9-live.sh
Expected output:

build-results/Nirbhai-Exam-Linux-9.iso
5. Test In VMware
Create a new VMware VM and attach:

build-results/Nirbhai-Exam-Linux-9.iso
Expected first boot:

Branded ISO name
Graphical desktop
Auto-login as student
dnf, yum, rpm, systemctl, firewall-cmd, SELinux commands available
6. Common Fixes
If a package is unavailable:

sudo dnf search package-name
Then edit:

kickstarts/rocky9-exam-live.ks
If Kickstart validation fails:

ksvalidator kickstarts/rocky9-exam-live.ks
Fix the line reported by the validator and run the build again.
