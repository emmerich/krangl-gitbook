## Why doesn't krangl provide vectorized comparison operators?

Some (`+`, `-`, `*`, `!`) can be overridden for collections, but others cannot (e.g. all arithmetic and boolean comparison ops)

No vectorization for `>`,  `&&` `==`, etc. in table forumlas → Use function calls or not so pretty `gt`, `AND`, `eq`, etc.

