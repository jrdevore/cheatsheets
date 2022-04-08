---
title: tmux
category: CLI
---

### Commands

    $ tmux
      -u        # UTF8 mode
      -S ~/.tmux.socket

#### Sessions

    $ tmux new
    $ tmux new -s session_name

    $ tmux attach # Default session
    $ tmux attach -t session_name

    $ tmux switch -t session_name

    $ tmux ls     # List sessions

    $ tmux detach

#### Windows

    $ tmux new-window

    # Enter Command Mode in TMUX session
    <leader> :

    # e.g. sourcing your conf file after changes
    <leader>:source-file ~/.tmux.conf

### Sessions

    $ tmux new -s myname
    $ tmux a  #  (or at, or attach)
    $ tmux a -t myname
    $ tmux ls
    $ tmux kill-session -t myname

### Help

    <leader> ?

### Scrolling

    <leader> [       # Enter scroll mode then press up and down

### Copy/paste

    <leader> [       # 1. Enter scroll mode first.
    Space       # 2. Start selecting and move around.
    Enter       # 3. Press enter to copy.
    <leader> ]       # Paste

### Panes

    <leader> %       # vert
    <leader> "       # horizontal split
    <leader> esc 1   # change from horiz to vert
    <leader> esc 2  # change from vert to horiz
    <leader> <spacekey>  # cycle tonext layout (vert -> horiz || horiz -> vert)
    <leader> hkjl    # navigation
    <leader> HJKL    # resize
    <leader> o       # next window
    <leader> x       # close pane
    C-b %       # vert
    C-b "       # horiz
    C-b hkjl    # navigation
    C-b HJKL    # resize
    C-b o       # next window
    C-b q       # show pane numbers
    C-b x       # close pane

    <leader> { or }  # move windows around

### Windows

    <leader> c       # New window
    <leader> 1       # Go to window 1
    C-b c       # New window
    C-b 1       # Go to window 1
    C-b n       # Go to next window
    C-b p       # Go to previous window
    C-b w       # List all window

### Detach/attach

    <leader> d       # Detach
    <leader> ( )     # Switch through sessions
    $ tmux attach

### Niceties

    <leader> t    # Time

### Renaming

    <leader> ,    # rename current window in session
    <leader> $    # rename current session


## Status formats

```
setw -g window-status-format `#[fg=8,bg=default]#I`
```

See `message-command-style` in the man page.

### Attribute/colors

| `#[fg=1]` | standard color |
| `#[fg=yellow]` | yellow |
| `#[bold]` | bold |
| `#[fg=colour240]` | 256 color |
| `#[fg=default]` | default |
| `#[fg=1,bg=2]` | combinations |
| `#[default]` | reset |

### Colors

 * `black` `red` `green` `yellow` `blue` `magenta` `cyan` `white`
 * `brightred` (and so on)
 * `colour0` ... `colour255`
 * `#333` (rgb hex)

### Attributes

 * `bold` `underscore` `blink` `noreverse` `hidden` `dim` `italics`

### Variables

| `#(date)` | shell command |
| `#I` | window index |
| `#S` | session name |
| `#W` | window name |
| `#F` | window flags |
| `#H` | Hostname |
| `#h` | Hostname, short |
| `#D` | pane id |
| `#P` | pane index |
| `#T` | pane title |

## Options

    set -g status-justify [left|centre|right]
    set -g status-left '...'

    setw -g window-status-style
    setw -g window-status-activity-style
    setw -g window-status-bell-style
    setw -g window-status-content-style
    setw -g window-status-current-style
    setw -g window-status-last-style

    setw -g window-status-format
    setw -g window-status-current-format

    setw -g window-status-separator

## My Tmux Config
> ~/.tmux.conf
> _As of: Tuesday Mar 26, 2019_

```
et -g prefix C-a
set -g mouse on
setw -g window-status-format " #I #W "
setw -g window-status-current-format "#[fg=color82,bold] #I #W "
setw -g window-status-current-fg colour65
setw -g window-status-current-bg black
setw -g window-status-current-attr bright
set -g status-position top
set -g status-left-length 40
set -g status-left "#[fg=colour65,bold]#I:#P #[fg=colour246]#S"
set -g status-right "#[fg=colour246]%d %b %R"
set -g status-justify centre

# Enable VI mode
setw -g mode-keys vi
bind -T copy-mode-vi 'v' send -X begin-selection

# Mouse Scrolling & VI Copy
bind -n WheelUpPane if-shell -F -t = "#{mouse_any_flag}" "send-keys -M" "if -Ft= '#{pane_in_mode}' 'send-keys -M' 'select-pane -t=; copy-mode -e; send-keys -M'"
bind -n WheelDownPane select-pane -t= \; send-keys -M
bind -t vi-copy WheelUpPane halfpage-up
bind -t vi-copy WheelDownPane halfpage-down

bind P paste-buffer
bind-key -t vi-copy 'v' begin-selection
bind-key -t vi-copy 'y' copy-pipe "xclip -sel clip -i"
bind-key -t vi-copy 'r' rectangle-toggle
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D
run-shell ~/tmux-pain-control/pain_control.tmux
```

---

## Extensions / Plugins

*  [tmux-plugins/tmux-pain-control: standard pane key-bindings for tmux](https://github.com/tmux-plugins/tmux-pain-control)
*  [Tmux Plugins](https://github.com/tmux-plugins)
