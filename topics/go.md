# Source environment variables in docker.

If you want to change `GO*` variables in docker image you can

* Use `ENV` command in `Dockerfile`. This is a simplest solution.
* Copy env file to image in `Dockerfile` and provide bash script which reads this file line by line, split each line into two segments such as variable name and variable value, calls `go env +w $varName=$varVal`. I found it too complex to use. I ended up using `ENV` command in `Dockerfile`.

Note you shouldn't change `GOROOT` variable. If you set it to some other value, you'll end up getting errors when calling go commands. Something about `GOPROXY` being empty and something about `GOROOT` being invalid. I don't remember.

You mostly need to change

* `GOPATH`
* `GOCACHE`
* `GOMODCACHE`
* `GOBIN`

variable if you want to keep variable state between jumping from one go binary to another. For example, when swithing linux distors or when using `docker run --rm` to call go command but use packages downloaded previously.

Using `ARG` with assignment doesn't seem to work:

```
//like this
ARG MYVAR=MYVAL
```

Consequive use of `ENV` like this

```
ENV MYENVVAR=$MYVAL/somedir
```

is going to create `MYENVVAR` initialized by `/somedir`.

I'm not sure because I seemed to work for some time but later it ended up with `/somedir` situation. Maybe it didn't work from the beginning but I didn't see it.
