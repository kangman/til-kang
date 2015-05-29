#How to comment multiple lines of Bash

```
: << 'COMMENT'
BLAH BLAH
BLAH BLAH 
for i in {1..3}
do
echo "hello"
done
COMMENT
```

#Context
some backgroud on what is happening here.  Note this is not recommended practice.
The colon is a shell builtin command that is a [NOP](https://en.wikipedia.org/wiki/NOP)
Because it is a command arguments sent to the command are accepted.  This can easily
cause unintended consequences.  Hence why the word 'COMMENT' is contain with single quotes
to deny expansion or substitution.  

Great answer on [stackexchange](https://unix.stackexchange.com/questions/37411/multiline-shell-script-comments-how-does-this-work )