# Jupyter for C++20

Install the docker 

```bash
$ cat Dockerfile
FROM jupyter/minimal-notebook
# Install in the default python3 environment
RUN conda install --yes xeus-cling -c conda-forge
$ docker build --rm -t xeuscling .
```

Run the `jupyter` docker

```bash
$ docker run --rm -p 8888:8888 -v "${pwd}":/home/jovyan/work/ xeuscling
```

output 

```bash
   To access the server, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/jpserver-7-open.html
    Or copy and paste one of these URLs:
        http://fe3bb9a80d63:8888/lab?token=e6771ddde3ce81b5664aebe9da3753effbe6ad2346ce3d6e
     or http://127.0.0.1:8888/lab?token=e6771ddde3ce81b5664aebe9da3753effbe6ad2346ce3d6e
```
