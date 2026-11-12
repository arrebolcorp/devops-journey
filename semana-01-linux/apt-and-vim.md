Hi there! For today, I gonna start removing (bascly purging) trn4 that I installed for error in the last class. I confused rn with rm and well, happens! 
And, is a good exercise for star this practice. Because I going to use sudo + apt (that is important for today) + purge (I use purge and not remove trn4 because I don't want to keep configurations files).
Ammm well, after this I used sudo apt autoremove for removing files that don't use.
<img width="387" height="166" alt="image" src="https://github.com/user-attachments/assets/fde639ed-23d3-4300-8696-484ab5a54eca" />

Let's start with the topic for today.

## Concepts: packages and apt
-apt- means Advanced Package Tool. This is function that helps us to install own first package or managing complex repository configurations. Basicly, is the primary tool that we use daily basis.

## Introduce to apt
apt is the default package manager on Ubuntu. This is a function that we use day-to-day in many activities like a, package operations, manage repositories in the DEB822. Is the core package managment system for Ubuntu and other Debian-based distributions. Whis this could dowloading, upgrading, and removing .deb packages while automatically we resolve dependencies. 
I start with this four commands lines:
1. Update package index	---> $ sudo apt update
2. Install a package --->	$ sudo apt install package-name
3. Upgrade all packages	---> $ sudo apt upgrade
4. Remove a package	---> $ sudo apt remove (purge)  package-name
Remember that $ in the previous class.

## apt vs apt-get
apt is more user-friendly while apt-get its output format is more stable across versions.

## What's new in AOT on Ubuntu 26.04
  Introduces several important change. For exapmle:
  -- Solver3 is the default - Is a new dependency resolver and now is enabled by default for all apt CLI operations. Use a SAT-solver-inspired approach that produces faster and more predictable results.
  -- DEB822 source format by default - Is a repository that are now configured in .sources files using the structured DB822 format rather than the legacy ine-line .list format.
  -- apt why and apt why-not - is the new diagnostic subcommands that explain why a package is or is not select for installation, this use a solver3's for trace a decision.
  -- Repository filtering with Include/Exclude - DEB822 source file options shows the allowlist or denylist of specific package from a repository without complex rules.
  -- apt modernize-sources - this command is a migration tool that converts legacy .list files to the DEB822 .sources format automatically.
  -- Scriter cryptographic policies - DSA keys and RSA keys smaller than 2048 bits are reject.


  ## Essential APT commands for Ubuntu 26.04
On top, I wrote some basic commands, now I write some ones more.

## Installing packages
-- $sudo apt install vim curl wget <--- this command helps us to install multiple packages in a single command by listing them separated by spaces. In this example I install 'vim', 'curl' and 'wget' in a single line.
<img width="401" height="268" alt="image" src="https://github.com/user-attachments/assets/f8191bc2-54e1-41d9-bc37-ad3c05db6c1d" />

-- if you need install a specific version of a package we can use ---> $ sudo apt install package-name=version

## Removing packages
atp has two ways to remove packages and one combination. 
--- $ sudo apt remove package-name and $sudo apt purge package-name <--- those commands lines have a different function, remove only uninstall the package but keeps the configuration files while purge remove both.
Usually we have to use $sudo apt autoremove for clean some dependencies that may no longer be needed.

## Upgrading packages
$ sudo apt upgrade
upgrade command never remove an existing package. If you to allow such removals, use full-upgrade: $ sudo apt full-upgrade.

$sudo apt update
Update commmand is important during distribution upgrades, where dependency changes are more common.

## Searching packages
It's so easy learn this command, because don't use sudo before apt because it only reads form local package cache. 
$ apt search keyword
$ apt show package-name

## Listing packages
The same case of searching packages, don't use sudo.
- Shows all installed packages on my system: $ apt lis --installed
- Shows all packages that needs have upgrade o have a upgrade available: $ apt list --upgradable
- Shows the lista of available version of a specific package: $ apt list -a package-name

## Managin repositories and Software Sources
NOTE: THE REPOSITORIES ARE REMOTE SERVERS THAT HOST COLLECTIONS OF .deb PACKAGES.
For this version of Ubuntu we may need to add third-party repositories to access additional software. 
-- Repository Source Files Ubuntu 26.04 <--- the repository sources are stored in the /etc/apt/sources.list.d/ directory. 
The primary system source files is ---> /etc/apt/sources.list.d/ubuntu.sources <--- the file uses DEB822 format.

## Adding a Third-Party Repository
To add a third-party repository I need create a new .sources file in  /etc/apt/sources.list.d/ and we have to import the repository's GPG key. Let's scrip! 

-Step 1 I gonna to download the GPG key for packages authentication. Download it an store it in /usr/share/keyrings/:
$ wget -qO- https://example.com/repo-key.gpg | sudo tee /usr/share/keyrings/example-keyring.gpg > /dev/null

-Step 2 I gonna to create .sources file: Create a new DEB822 format source file:
$ sudo nano /etc/apt/sources.list.d/example.sources
and gonna add repository definitions
Types, URIs, Suites, Components, Signed-By;

-Step 3 Update the package index using $ sudo apt update

##VIM 
Is a advanced editor of text. It main funtions are:
1. Manage servers: Allows editing configutation files on the system directly by SSH and don't need a graphic interface
2. Programming and develp: The developers use this for write code in Phyton, C, JavaScrip or PHP lenguage.
3. Editing faster without mouse
4. Low resources consume.
To install VIM on Ubuntu can use $ sudo apt install vim and next consulting the version with $ vim --version.
There are two modes that so different behaviours.
Normal mode and Inster mode. The normal mode is used to imput commands, and inster mode for writing text-similar to regular text edtitor's.

You can type a 'vim testfile' for create automatically a test file where you practice or we can run 'vimtutor' for study all funtionallities of vim.

<img width="801" height="535" alt="image" src="https://github.com/user-attachments/assets/f412ffae-4d54-4145-8203-297a2b6e47ec" />

its all for today, see ya! 











