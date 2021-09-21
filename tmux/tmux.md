# T-Mux

The powerfull multiplexer terminal:

![tmux view](tmux.view1.png)

## Session Commands

### Detach from a session

``` Ctrl+b d```

### List all sessions

```bash
$ tmux ls
0: 1 windows (created Sat Dec 12 15:03:37 2020) (attached)
```
### Attach to a running session

```tmux a -t session-name```
```bash
$ tmux a -t 0
```

### Give a name | Rename a session

``` Ctrl+b $```

![tmux view](tmux.rename.png)

### Kill a session

```bash
$ tmux ls
mysession: 1 windows (created Sat Dec 12 15:03:37 2020)
$ tmux kill-session -t mysession
$ tmux ls
no server running on /tmp/tmux-0/default
```

## Panes

### split pane horizontal  
```Ctrl+b "```
### split pane vertical 
```Ctrl+b %```
### close current pane 
```Ctrl+b x```

### switch panes
```Cltrl+b ← ```
```Cltrl+b ↑ ```
```Cltrl+b → ```
```Cltrl+b ↓ ```




