## jest intellisense in VS Code
---

create the `jsconfig.json` file at the project level folder (same folder where the `src` and `public` folders are) and add:

```json
{
    "typeAcquisition": {
        "include": [
            "jest"
        ]
    }
}
```
also install: 
```bash
npm i @types/jest --save-dev
```

restart the VS Code.

## JEST version
---

If the application was create using `npx create-react-app` and you try to install `jest` using `npm install jest` you don't get the latest version of `jest`.

Type installing it using:
 ```bash
 npm install jest@^29
 ```
 , or whatever is the latest version of `jest`.


