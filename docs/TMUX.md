Start new session: `tmux`

Start new named session: `tmux new -s session_name`

Attach to a session: `tmux attach -t session_name`

Detach from session: `Ctrl+b d`

List sessions: `tmux ls`

Kill session: `tmux kill-session -t session_name`

Split pane horizontally: `Ctrl+b "`

Split pane vertically: `Ctrl+b %`

Switch to pane: `Ctrl+b arrow_key`

Close pane: `exit` or `Ctrl+d`

Create window: `Ctrl+b c`

Switch to window: `Ctrl+b window_number`

Rename window: `Ctrl+b ,`

Find window: `Ctrl+b f`


To scroll in tmux, you need to enter copy mode:
Enter copy mode: `Ctrl+b [`

Scroll up/down: `Use arrow keys or Page Up/Page Down`

Scroll up a page: `Press Ctrl + ↑`

Scroll down a page: `Press Ctrl + ↓`

Exit copy mode: `Press q`

In tmux, you can adjust the size of the panes manually with specific commands after pressing Ctrl+b followed by : to enter command mode.
Resize Down: `resize-pane -D [amount]`

Resize Up: `resize-pane -U [amount]`

Resize Right: `resize-pane -R [amount]`

Resize Left: `resize-pane -L [amount]`

If you want to redistribute the space equally among all panes within a window, you can use the select-layout command.
Equal Horizontal Distribution: `select-layout even-horizontal`

Equal Vertical Distribution: `select-layout even-vertical`

For more interactive resizing without entering command mode:
Resize Mode: Press `Ctrl+b followed by :`, then type `resize-pane -m` to enter resize mode. After this, you can use the arrow keys to resize the active pane. Press `Enter` to exit resize mode.
