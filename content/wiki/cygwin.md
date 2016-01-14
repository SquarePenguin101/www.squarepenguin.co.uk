
## Cygwin

These instructions are for the 32-bit version of Cygwin, but 64-bit Cygwin should work as well. See https://cygwin.com for more information.

### Cygwin and get_iplayer dependencies

1. Download Cygwin installer

    https://cygwin.com/setup-x86.exe

2. Run installer

    NOTE: These instructions assume you choose `C:\cygwin` as your installation directory, so adjust accordingly if you opt for a different location.
      
    Install only the base system initially (accept the default package list). You will run setup-x86.exe again to install get_iplayer dependencies

3. Copy setup-x86.exe to `C:\cygwin`

4. Follow the instructions at http://cygwinports.org/ to use the Cygwin Ports repository to install get_iplayer dependencies. Since you copied setup-x86.exe to `C:\cygwin`, your command would be:

        cygstart -- /setup-x86.exe -K http://cygwinports.org/ports.gpg

    Select the following packages for installation:

        curl 
        ffmpeg 
        rtmpdump 
        atomicparsley 
        perl 
        perl-cgi
        perl-libwww-perl 
        perl-lwp-protocol-https
        perl-xml-simple 
        perl-mp3-tag 
        perl-mp3-info 
        perl-net-smtp-ssl 
        perl-authen-sasl 

### Command-line Interface (CLI)

Use the CLI [manual installation procedure](manual#manual-cli) described for Linux/Unix.

NOTE: `sudo` is not used for CLI installation on Cygwin

### Web PVR Manager (WPM)

Use the WPM [manual installation procedure](manual#manual-cli) described for Linux/Unix.

NOTE: `sudo` is not used for WPM installation on Cygwin
        
