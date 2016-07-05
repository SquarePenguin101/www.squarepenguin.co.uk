## get_iplayer Development Version

The development version of get_iplayer is maintained on the **develop** branch in the [GitHub repo](https://github.com/get-iplayer/get_iplayer). It contains fixes and new features for the next release of get_iplayer. There may be occasions when you wish to use the development version of get_iplayer for testing or to get a bug fix in advance of the next release.

**IMPORTANT: The development version of get_iplayer may contain new bugs and breaking changes - use with caution. Before installing it, be sure you know how to restore your previous version.**

**NOTE: These instructions are intentionally terse and assume certain knowledge on your part. If you do not understand them, do not attempt to install the development version. Installation and usage of the development version are NOT SUPPORTED.**

### Obtaining the development version

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

	NOTE: If your system does not have `curl` try `wget`.  Replace `curl -kLO` with `wget --no-check-certificate`. 

You can use your web browser or any other download method you prefer so long as it can download the scripts as **plain text files**.

### Running the development version

You may run both the CLI and WPM directly from the cloned repository, download directory or any other location. Be sure to use the `--getiplayer` option when launching the WPM to configure it to use the development version of the CLI. Changes in the WPM may depend on related changes in the CLI, so don't mix release and development versions of the scripts.

Don't replace a Unix package version of get_iplayer with the development version. Remove the package version - you can always reinstall later - but keep its dependencies installed.  You can run the development version from any convenient location.

The same goes for Windows - don't replace files installed by the get_iplayer installer. See the [Windows instructions](/wiki/windows#custom) for information on how to create a copy of get_iplayer for customisation. Note that on Windows the `get_iplayer` script is renamed to `get_iplayer.pl`.
