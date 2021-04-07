# build

* `git init`

* `yarn init -y`

  * ```
    "scripts":{
    "build":"rm -rf dist && parcel build src/index.html --no-minify --public-url ./"
    }
    ```

* `yarn build`

* 创建 .gitignore 文件

  * ```
    /.cache/
    /node_modules/
    /.idea/
    ```

  * /.idea/只有webstorm有，vscode中没有

* `dist/index.html`

