## Install latest version of nodejs
---

by default in debian apt repository you don't find the latest version of `nodejs`. Here is an example how to install the `19.x` version.


```bash
$ sudo apt-get install curl software-properties-common 
$ curl -sL https://deb.nodesource.com/setup_18.x | sudo bash -
$ sudo apt-get install -y nodejs
$ npm install --global yarn
$ node -v 
v19.3.0
$ npm -v
9.3.0
$ yarn -v
1.22.19
```


