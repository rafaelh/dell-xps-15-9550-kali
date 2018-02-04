### Save current map, keycode 66 is where Caps lock lies
xmodmap -pke > ~/.Xmodmap.bak

### add following content to ~/.Xmodmap:
clear lock
keycode 66 = Control_L
add control = Control_L Control_R

We're using lightdm, no need to source that file.
### make it work in current session
xmodmap ~/.Xmodmap