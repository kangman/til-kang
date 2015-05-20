#How to get tab completion working for your ~/.ssh/config file

When you have a decent size config file with hosts and proxy commands and all that good stuff
it might come in handy to have tab completion for these hosts you keep sshing into.  

here is a script I found through the oracle(google) but made a modification as you can have
more than one hostname aka alias. 

```
_complete_ssh_hosts ()
 {
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"
    comp_ssh_hosts=`cat ~/.ssh/known_hosts | \
                    cut -f 1 -d ' ' | \
                    sed -e s/,.*//g | \
                    grep -v ^# | \
	                uniq | \
	                grep -v "\[" ;
            cat ~/.ssh/config | \
	                grep "^Host " | \
		            awk '{print $0}';
		    `
    COMPREPLY=( $(compgen -W "${comp_ssh_hosts}" -- $cur))
    return 0
}
complete -F _complete_ssh_hosts ssh
```

What this is doing is it will go through your ~/.ssh/known_hosts file transform the text to only find the hostnames.  
It will also go through your ~/.ssh/config file and look for the line that starts with "Host..."  
These hits will then be offered when you tab after typing in ssh.

