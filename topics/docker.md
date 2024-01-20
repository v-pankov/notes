# Source environment variables in docker.

Simplest way is to use `ENV` command in `Dockerfile`.

Other way is to create user in `Dockerfile` and add `.` command to `.bashrc` or `.profile` files (if you want variables to be available in bash sessions).

# Package installation in Dockerfile

* Use `apt-get` instead of `apt` becase later one causes warnings or errors. I don't remember.
* Use `apt-get` with `-y` to disable interation.
* Use `apt-get` with `--no-install-recommends` to prevent installing recommended packages.
* Use `export export DEBIAN_FRONTEND=noninteractive &&` before `apt-get ...` in order to prevent warnings. I don't remember what kind of warnings.
* Use `apt-get install apt-utils` - `apt-get` will complain about `apt-utils` not being installed. It will complain while you install `apt-utils`. I don't know should I care about it. Must research.
* Use `apt-get install bash-completion` if you want docker container to be used in interactive mode and commands to be autocompleted.

# Making callable docker run.

If you want container to be used as binary replacement then make sure it's run with `-it` flag. Otherwise you won't be able to interrupt the binary.

For example, let's assume you have a `go` project and `go run ./cmd/` launches a server and the only way to stop it is to send terminate signal via `Ctrl+C`.

Lets assume you have a container image containing `go` binary and you run it like this

```
docker run --rm .:/workspace mygoimage bash -c cd /workspace && go run ./cmd
```

Now you cannot interrupt it. The only way to stop it is to stop the container.

Just add `-it` flags. This way your `Ctrl+C` will be send to application `go run ./cmd` in docker.
