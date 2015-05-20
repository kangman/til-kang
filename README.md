
#TIL
##Today I Learned

Wed Apr  8 10:34:16 EDT 2015

###units 

command is used to get units of measurement as well as a quick way to convert between units

###ngrep

It's like grep but for the network

##VIM

###VIM: A 

inserting at the end of the line
###VIM: I 

inserting at the beginning of the line

##SCP

copy files with ssh key

`scp -i /path/to/private/key -r /your/directory user@newserver.com:/new/folder/`

##Bash

change permission bits selectively using the "find" command
`find /opt/lampp/htdocs -type f -exec chmod 644 {} \;`

##Less

Output of less with color using [Pygmentize](http://pygments.org/)

Create a ~/.lessfilter file that will contain the Pygmentize script
'''
#!/bin/sh
case "$1" in
    *.awk|*.groff|*.java|*.js|*.m4|*.php|*.pl|*.pm|*.pod|*.sh|\
    *.ad[asb]|*.asm|*.inc|*.[ch]|*.[ch]pp|*.[ch]xx|*.cc|*.hh|\
    *.lsp|*.l|*.pas|*.p|*.xml|*.xps|*.xsl|*.axp|*.ppd|*.pov|\
    *.diff|*.patch|*.py|*.rb|*.sql|*.ebuild|*.eclass)
        pygmentize -f 256 "$1";;
    .bashrc|.bash_aliases|.bash_environment)
        pygmentize -f 256 -l sh "$1"
        ;;
    *)
        grep "#\!/bin/bash" "$1" > /dev/null
        if [ "$?" -eq "0" ]; then
            pygmentize -f 256 -l sh "$1"
        else
            exit 1
        fi
esac

exit 0
'''

in your .bashrc or .bash_profile add
'''
export LESS='-R'
export LESSOPEN='|~/.lessfilter %s'
'''

make your ~/.lessfilter executable
'''
chmod u+x ~/.lessfilter
'''

link to stackexchange [post](http://superuser.com/questions/117841/get-colors-in-less-command)

