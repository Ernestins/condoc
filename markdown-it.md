
## CommonMark Spec (Latest version (0.30))
- https://spec.commonmark.org/
- https://spec.commonmark.org/0.30/

---


# Markdown Parser -- markdown-it
- https://github.com/markdown-it/markdown-it
- https://www.jsdelivr.com/package/npm/markdown-it
- https://cdnjs.com/libraries/markdown-it

Install markdown-it
```
npm install markdown-it --save
```

## markdown-it -- Plugin
- https://github.com/markdown-it/markdown-it-container
- https://github.com/markdown-it/markdown-it-sup
- https://github.com/markdown-it/markdown-it-sub
- https://github.com/markdown-it/markdown-it-ins
- https://github.com/markdown-it/markdown-it-del
- https://github.com/markdown-it/markdown-it-footnote
- https://github.com/markdown-it/markdown-it-deflist
- https://github.com/markdown-it/markdown-it-abbr
- https://github.com/markdown-it/markdown-it-mark
  - In CommonMark only:
  ```md
  ==mark==
  ```
  - missing hackmd tags:
  ```md
  ##### tags: `tag1` `tag2` `tag3`
  ```
  - missing tags via yaml meta data:
  ```md=
  ---
  tags: tag1, tag2, rage
  ---  
  ```
  - missing cmd tag list:
  ```cmd=
  ###=tags:
  tag1 tag2 tag3
  ###
  ```
  - missing cmd mark list:
  ```md
  ===tags:
  tag1 tag2 tag3
  ===
  ```
  - missing cmd single linkable tag:
  ```cmd
  #tag1#
  ```
  or
  ```cmd
  # Title #tag1#
  
  [Link to Title](@tag1)
  ```

## markdown-it -- addons
- https://github.com/camelaissani/markdown-it-include
- https://github.com/valeriangalliat/markdown-it-anchor
- https://github.com/arve0/markdown-it-attrs
- https://github.com/markdown-it/markdown-it-emoji
  - https://dev.to/nikolab/complete-list-of-github-markdown-emoji-markup-5aia
- https://github.com/valeriangalliat/markdown-it-highlightjs
- https://github.com/camelaissani/markdown-it-include
- https://github.com/cmaas/markdown-it-table-of-contents


## Text URL Rendering 
- https://github.com/markdown-it/linkify-it

## mdurl Util
- https://github.com/markdown-it/mdurl
- needed as Func


