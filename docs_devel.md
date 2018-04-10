

## How to improve docs?

* learn from https://jtablesaw.wordpress.com/an-introduction/
* how to illustrate joins https://blog.jooq.org/2016/07/05/say-no-to-venn-diagrams-when-explaining-joins/



## gitbook documentation

for gitbook page layout see https://toolchain.gitbook.com/pages.html

https://github.com/GitbookIO/gitbook/blob/master/docs/setup.md

```bash
#npm install gitbook-cli -g

#cd /Users/brandl/projects/kotlin/krangl/docs/manual
gitbook serve
gitbook build

gitbook build ./ --log=debug --debug

```

don't miss the local editor
https://www.gitbook.com/editor

https://github.com/GitbookIO/theme-api

nice extensions
https://github.com/GitbookIO/theme-api
https://github.com/jadu/gitbook-theme


for theming add
```
"styles": {
  "website": "assets/continuum/cp.css"
}
```

docs in sub-directory https://github.com/GitbookIO/gitbook/issues/688
