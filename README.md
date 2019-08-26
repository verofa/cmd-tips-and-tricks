

# Command Lines - Tips and Tricks **

- Powerline customization:

  <u>Username</u>

  Change the username powerline prompt value for the one that you like:

  ```python
  # Access to the directory that contain the py file with the username value
  cd $HOME/Library/Python/2.7/lib/python/site-packages/powerline/segments/common/
  # Check that env.py file is there
  ls -la env.py
  -rw-r--r--  1 verogo  verogo  5681 26 Aug 11:39 env.py
  
  # This is the segment that assign the username valut to the prompt:
  
  def user(pl, segment_info, hide_user=None, hide_domain=False):
          '''Return the current user.
  
          :param str hide_user:
                  Omit showing segment for users with names equal to this string.
          :param bool hide_domain:
                  Drop domain component if it exists in a username (delimited by '@').
  
          Highlights the user with the ``superuser`` if the effective user ID is 0.
  
          Highlight groups used: ``superuser`` or ``user``. It is recommended to define all highlight groups.
          '''
          global username
          if (
                  segment_info['environ'].get('_POWERLINE_RUNNING_SHELL_TESTS')
                  == 'ee5bcdc6-b749-11e7-9456-50465d597777'
          ):
                  return 'user'
          if username is False:
                  username = _get_user()
          if username is None:
                  pl.warn('Failed to get username')
                  return None
          if username == hide_user:
                  return None
          if hide_domain:
                  try:
                          username = username[:username.index('@')]
                  except ValueError:
                          pass
          euid = _geteuid()
          return [{
                  'contents': username,
                  'highlight_groups': ['user'] if euid != 0 else ['superuser', 'user'],
          }]
  
  
  ```

  

Therefore, to modifiy the username value of powerline prompt you have to change ***_get_user()*** instructions for the *string* that you want:

```python
def user(pl, segment_info, hide_user=None, hide_domain=False):
        '''Return the current user.

        :param str hide_user:
                Omit showing segment for users with names equal to this string.
        :param bool hide_domain:
                Drop domain component if it exists in a username (delimited by '@').

        Highlights the user with the ``superuser`` if the effective user ID is 0.

        Highlight groups used: ``superuser`` or ``user``. It is recommended to define all highlight groups.
        '''
        global username
        if (
                segment_info['environ'].get('_POWERLINE_RUNNING_SHELL_TESTS')
                == 'ee5bcdc6-b749-11e7-9456-50465d597777'
        ):
                return 'user'
        if username is False:
                username = 'verogo'
        if username is None:
                pl.warn('Failed to get username')
                return None
        if username == hide_user:
                return None
        if hide_domain:
                try:
                        username = username[:username.index('@')]
                except ValueError:
                        pass
        euid = _geteuid()
        return [{
                'contents': username,
                'highlight_groups': ['user'] if euid != 0 else ['superuser', 'user'],
        }]



```



- Unix Like systems

  - Redirect output messages in the terminal:

  ```bash
  The > operator redirects the output usually to a file but it can be to a device. You can also use >> to append.
  
  If you don't specify a number then the standard output stream is assumed but you can also redirect errors
  
  > file redirects stdout to file
  1> file redirects stdout to file
  2> file redirects stderr to file
  &> file redirects stdout and stderr to file
  
  /dev/null is the null device it takes any input you want and throws it away. It can be used to suppress any output.
  
  ## Source: https://askubuntu.com/questions/350208/what-does-2-dev-null-mean
  ```

  - Change the *bash* **HISTORY** configuration:
  
  ```bash
    ## Check the actual size of .bash_history file. You can check these values as well, listing env variables (the way to do it is in this readme)
    $ echo $HISTSIZE # the number of commands to remember in the command history
    500
    $ echo $HISTFILESIZE # the maximum number of lines contained in the history file
    500
    
    ## Increase .bash_history
    $ export HISTSIZE=1000000
    
    $ export HISTFILESIZE=1000000
    
    # Change the one history file macos
    $ echo $SHELL_SESSION_HISTORY
  1
  
  $ export SHELL_SESSION_HISTORY=0
  
  #To make it permanent, you have to add it to the .bash_profile file, for further information about how this works -> https://stackoverflow.com/questions/19454837/bash-histsize-vs-histfilesize
    
    ## Delete .bash_history
    $ srm -m ~/.bash_history
    
  ### more info https://www.shellhacks.com/tune-command-line-history-bash/
  ```
  
  - List all shell env variables
  
  ```bash
    #In bash to list the "shell variables" (shell variables plus environment variables):
    
    $ ( set -o posix ; set ) | more
  
    # In bash print all the environment variables:
    $ printenv
    # or as an alternative
    $ env
  ```
  
    
  
  - 
  
  - 
  
  
  
    

