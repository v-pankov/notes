# Forward arguments

Use `$@`:

```
// myscript.sh
//!bin/bash
go $@

// using myscript.sh
./myscript.sh run ./cmd/main.go

// result: same as calling
go run ./cmd/main.go
```

# Source environment variables from file.

Create env file. It should contain variable definitions like

```
//myenvfile
MYVAR=myval
```

Use `.` command to read variables from file:

```
. myenvfile
```

`MYVAR` variable will be available after that.

Note that sourced environment variables are not inherited. For example, `MYVAR` will be empty in `bash` session started by `. myenvfile && bash`

# Read file line by line and process each line.

This answer is useful:
https://stackoverflow.com/a/16318005

# Split string into two substring using delimeter

For example, to split variable definition string `MYVAR=MYVAL` to get variable name and variable value.

Here is how to do it:

```
string="iuhiwr=912u3"
IFS='=' read -r part1 part2 <<< "$string"
```

This can be used in combination with reading file line by line.

How it works:

* `IFS='='` sets delimiter for `read -r`
* `read -r` scans input string and creates variables `$part1` and `$part2` containing values from left and from the right side of `=`