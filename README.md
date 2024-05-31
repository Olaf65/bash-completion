# bash-completion
bash-completion in Ubuntu 22.04.4 LTS not working with "find" if parameter "-exec" follows

Description of the Problem

Issue: Bash-completion in Ubuntu 22.04.4 LTS not working with find if the parameter -exec follows.

System Information:

    PRETTY_NAME: "Ubuntu 22.04.4 LTS"
    NAME: "Ubuntu"
    VERSION_ID: "22.04"
    VERSION: "22.04.4 LTS (Jammy Jellyfish)"
    VERSION_CODENAME: "jammy"

Bash-completion:
    
    VERSION: "1:2.11-5ubuntu1"
    
Affected File:

    /usr/share/bash-completion/bash_completion

Problem Details:
In the function _command_offset(), line 1925:

((COMP_POINT -= ${#COMP_WORDS[i]}))

I added the following to prevent COMP_POINT from becoming negative:

((COMP_POINT < 0)) && COMP_POINT=0

Steps to Reproduce:

    Use the find command with the -exec parameter like 'find / -exec'.
    Attempt to use tab completion after /.
    'bash: COMP_POINT: Teilstring-Ausdruck < 0.' appears.

Solution:

Modify the _command_offset() function to include the following check:

((COMP_POINT < 0)) && COMP_POINT=0

This prevents COMP_POINT from becoming negative, resolving the issue with bash-completion for find -exec.

