iTerm2 shortcuts: 
==================

* To switch between panes :  ```alt + cmd + arrow keys (or) cmd + [ or ]```
* To switch between windows: ```cmd + arrow```
* To split the current window vertically: ```cmd + d ```
* To split the current window horizontally: ```cmd + shift + d```
* To turn of transparency in the window: ```cmd + u``` ( to enable the transparancy, its the same shortcut). 

Shell 
===========
* To make a currently running background process as nohup background process: ```disown -h %jobId```
* To get the job ids of background processes : ```jobs```
* To create an array in shell script: ```array_name=( value1 value2 )```
* To iterate on an array in for loop: 
```bash
for val in "${array_name[@]}"; 
  do echo $i ; 
done
```
* To create a function in shell script: 
```bash
  function foo {
    echo $1 # $1 is the first parameter to the function 
  }  
  foo Hello # function name and then the args. 
```  
* fish shell prompt
```fish
# replace USERNAME and HOSTNAME with your own values- 
function fish_prompt --description 'Write out the prompt'
        if test -z $WINDOW
   printf '%s%s⚈%s%s%s%s%s-> ' (set_color yellow) (whoami | sed 's/USERNAME/λ/' ) (set_color purple) (hostname|cut -d . -f 1 | sed 's/HOSTNAME/⒳  /' ) (set_color $fish_color_cwd) (prompt_pwd) (set_color normal)
 else
   printf '%s%s@%s%s%s(%s)%s%s%s▶ ' (set_color yellow) (whoami) (set_color purple) (hostname|cut -d . -f 1) (set_color white) (echo $WINDOW) (set_color $fish_color_cwd) (prompt_pwd) (set_color normal)
 end
end

```
