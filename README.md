# Duf

[![CI](https://github.com/sigoden/duf/actions/workflows/ci.yaml/badge.svg)](https://github.com/sigoden/duf/actions/workflows/ci.yaml)
[![Crates](https://img.shields.io/crates/v/duf.svg)](https://crates.io/crates/duf)

Duf is a fully functional file server.

![demo](https://user-images.githubusercontent.com/4012553/171526189-09afc2de-793f-4216-b3d5-31ea408d3610.png)

## Features

- Serve static files
- Download folder as zip file
- Search files
- Upload files and folders (Drag & Drop)
- Delete files
- Basic authentication
- Upload zip file then unzip
- Serve through https
- Easy to use with curl

## Install

### With cargo

```
cargo install duf
```

### Binaries on macOS, Linux, Windows

Download from [Github Releases](https://github.com/sigoden/duf/releases), unzip and add duf to your $PATH.

## Usage

You can run this command to start serving your current working directory on 127.0.0.1:5000 by default.

```
duf
```

...or specify which folder you want to serve.

```
duf folder_name
```

Listen on all Interfaces and port 3000

```
duf -b 0.0.0.0 -p 3000
```

Allow all operations such as upload, delete

```sh
duf --allow-all
# or
duf -A
```

Only allow upload operation

```
duf --allow-upload
```

Serve a single page application (SPA)

```
duf --render-spa
```

Serve https 

```
duf --tls-cert my.crt --tls-key my.key
```

## CLI

```
Duf is a fully functional file server.

USAGE:
    duf [OPTIONS] [path]

ARGS:
    <path>    Path to a root directory for serving files [default: .]

OPTIONS:
    -a, --auth <user:pass>      Use HTTP authentication for all operations
    -A, --allow-all             Allow all operations
        --allow-delete          Allow delete operation
        --allow-symlink         Allow symlink to directories/files outside root directory
        --allow-upload          Allow upload operation
    -b, --bind <address>        Specify bind address [default: 127.0.0.1]
        --cors                  Enable CORS, sets `Access-Control-Allow-Origin: *`
    -h, --help                  Print help information
        --no-auth-read          Do not authenticate read operations like static serving
    -p, --port <port>           Specify port to listen on [default: 5000]
        --path-prefix <path>    Specify an url path prefix
        --render-index          Render index.html when requesting a directory
        --render-spa            Render for single-page application
        --tls-cert <path>       Path to an SSL/TLS certificate to serve with HTTPS
        --tls-key <path>        Path to the SSL/TLS certificate's private key
    -V, --version               Print version information
```


## API

Download a file
```
curl http://127.0.0.1:5000/some-file

curl -o some-file2 http://127.0.0.1:5000/some-file
```

Download a folder as zip file

```
curl -o some-folder.zip http://127.0.0.1:5000/some-folder?zip
```

Upload a file

```
curl --upload-file some-file http://127.0.0.1:5000/some-file
```

Unzip zip file when unload

```
curl --upload-file some-folder.zip http://127.0.0.1:5000/some-folder.zip?unzip
```

Delete a file/folder

```
curl -X DELETE http://127.0.0.1:5000/some-file
```

## License

Copyright (c) 2022 duf-developers.

duf is made available under the terms of either the MIT License or the Apache License 2.0, at your option.

See the LICENSE-APACHE and LICENSE-MIT files for license details.