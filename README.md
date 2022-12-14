# workman

A simple cli tool to manage your `go.work` file.

## How to install

- method 1: Use the `go` command `go install github.com/dashengyeah/workman@latest`.

- method 2: Go to the [release](https://github.com/dashengyeah/workman/releases) page.

## How to use

just run `workman` in any module inside a `go.work` defined workspace, and you'll see the command line UI interactives.

> BTW, the command itself already support json output and arg-based operations. Run `workman -h` to see the usage.
```
Usage of workman:
  -l    list go.work info
  -n    no command line ui
  -u string
        update go.work (default "{}")
```
> I'm working on a `vscode-go-work-manager` plugin too. But not sure when to finish, ah...๐

### Example

0. Our workspace

Folder tree:

```
~/work/
โโโ go.work
โโโ mod1/
โย ย  โโโ go.mod
โโโ mod2/
โย ย  โโโ go.mod
โโโ mod3/
โย ย  โโโ go.mod
โโโ mod4/
โย ย  โโโ go.mod
โโโ mod5/
โย ย  โโโ go.mod
โโโ mod6/
    โโโ go.mod
```

Our `go.work` file:

```go
go 1.18

use (
    mod1
    mod2
    mod3
)
```

1. Let's try `$ workman`.

Output:

```
Workspace: ~/work/go.work go1.18
Module usage:
โ mod1
โ mod2
โ mod3
 ยท mod4
 ยท mod5
 ยท mod6
change: <Tab> | exit: <Esc>/<q>
```

It displays the `go.work` file path and the `go` version in it.

2. It's interactive. press `<Tab>` key to change the modules we are using.

Output:

```
Modules:
> [โ] mod1
  [โ] mod2
  [โ] mod3
  [โ] mod4
  [โ] mod5
  [โ] mod6
enter: select | tab: confirm | left: none | right: all | type to filter
```

Follow the instructions to turn *OFF* `mod1` `mod3`, and turn *ON* `mod6`.

```
Modules:
  [โ] mod1
  [โ] mod2
  [โ] mod3
  [โ] mod4
  [โ] mod5
> [โ] mod6
enter: select | tab: confirm | left: none | right: all | type to filter
```

Press `<Tab>` to confirm. Then it backs to display the current `go.work` status.

```
Workspace: /home/dash/work/go.work go1.18
Module usage:
โ mod2
โ mod6
 ยท mod1
 ยท mod3
 ยท mod4
 ยท mod5
change: <Tab> | exit: <Esc>/<q>
```

Press `<Esc>` to quit the tool. And `cat go.work` to see its content.

```
go 1.18

use (
    mod2
    mod6
)
```

That's it.
