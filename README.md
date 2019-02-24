# fuego
A command-line firestore client

## Installation

Install fuego via [go](https://golang.org/dl/):

```sh
go get github.com/sgarciac/fuego
```

Or use one of the precompiled binaries (untested) from the [latest release](https://github.com/sgarciac/fuego/releases).

## Usage

### Writing and reading data

You can add new documents:

```sh
fuego add people '{"name": "sergio", "age": 41}'
# Rv7ZfnLQWprdXuulqMdf
```

Of fetch them:

```sh
fuego get people Rv7ZfnLQWprdXuulqMdf
# {
#    "age": 41,
#    "name": "sergio"
# }
```

You can also update an existing document:

```
fuego set people Rv7ZfnLQWprdXuulqMdf '{"name": "sergio", "age": 41}' # It's my birthday!
```

In both ```add``` and ```set``` commands, the document argument can be either a
json string (if it starts with the character '{') or a path to a json file, i.e.:

```sh
fuego add animals ./dog.json
```


### Hacking

Creating binary executables:

```sh
(gox -os="linux darwin windows" -arch="amd64" -output="dist/fuego_{{.OS}}_{{.Arch}}")
(cd dist; gzip *)

```

Releasing on github:

```sh
# create and push a tag git tag -a v0.0.1 -m "Release description"
# git push --tags
export GITHUB_TOKEN=mytoken
export TAG=v0.0.1
ghr -t $GITHUB_TOKEN -u processone --replace --draft  $TAG dist/
```

