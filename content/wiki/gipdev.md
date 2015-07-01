## get_iplayer Development Version

The development version of get_iplayer is maintained on the **develop** branch in the GitHub repo. It contains fixes and new features for the next release of get_iplayer. There may be occasions when you wish to use the development version of get_iplayer for testing or to get a bug fix in advance of the next release.  

**IMPORTANT: The development version of get_iplayer may contain new bugs and breaking changes - use with caution. Before installing it, be sure you know how to restore your previous version. Both usage and installation of the development version are completely unsupported**.

### Obtaining development version

Development versions of both the command-line interface (CLI) and Web PVR Manager (WPM) can be obtained from the GitHub repo:

#### Using Git

1. Clone the get_iplayer repository to working directory (GitHub account not required)

		git clone git://github.com/get-iplayer/get_iplayer

2. The get_iplayer code will now be in a sub directory named `get_iplayer`

        cd get_iplayer

3. Ensure you are using the **develop** branch

        git checkout develop

#### Direct download

1. Download the development version to working directory

    CLI:

        curl -kLO https://raw.github.com/get-iplayer/get_iplayer/develop/get_iplayer

    WPM:

		curl -kLO https://raw.github.com/get-iplayer/get_iplayer/develop/get_iplayer.cgi

	NOTE: If your system does not have `curl` try `wget`.  Replace `curl -kLO` with `wget --no-check-certificate`. You can use whatever download method you prefer so long as it can download the scripts as plain text files.

### Running development version

You may run both the CLI and WPM directly from the cloned repository, download directory or other preferred location. Be sure to use the `--getiplayer` option when launching the WPM to configure it to use the development version of the CLI. Changes in the WPM may depend on related changes in the CLI, so don't mix release and development versions of the scripts.

### Replacing existing CLI/WPM

If you wish to replace your existing get_iplayer installation, proceed from step #2 in the CLI/WPM [manual installation procedures](/wiki/manual) after first backing up your existing CLI and WPM. If you are replacing a package installation, it is recommended that you first remove the get_iplayer package (but leave external programs installed), then follow the manual installation procedure to install the development version to /usr/local/bin (or similar).  If you're on Windows, replace the get_iplayer.pl (note the addition of .pl extension) and get_player.cgi files in your installation directory.
