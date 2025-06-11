# Making this book your own
This repo contains most of the necessary parts of a Jupyter-book (configured for GLOCAL usage) - I've included a few sample parts and chapters as a starting point. Sample Part 3 Chapter 3 is probably my best example of 'good' markdown usage - so use it as a reference sheet if you'd like.

## What to Change:
- README.md lines 1, 3, 4, 5
- CONTRIBUTING.md lines 28, 29, 45, 56
- deploy.yml (if publishing) lines 27, 32, 33, 38
- glocal-book-template folder name
- glocal-book-template/_config.yml lines 8, 9, 29
- glocal-book-template/conf.py lines 6, 31,

## Table of Contents FAQ:
Formatting a TOC is a̶n̶n̶o̶y̶i̶n̶g̶  easy - just follow this template:
```yml
format: jb-book
root: index

parts:
  - caption: "Part One"
    chapters:
      - file: part-one/intro
      - file: part-one/chapter-a
        sections:
          - file: part-one/chapter-a/section-1
          - file: part-one/chapter-a/section-2
      - file: part-one/chapter-b

  - caption: "Part Two"
    chapters:
      - file: part-two/chapter-c
      - file: part-two/chapter-d
        sections:
          - file: part-two/chapter-d/section-3
          - file: part-two/chapter-d/section-4

  - caption: "Extras"
    chapters:
      - file: extras/glossary
      - file: extras/appendix
      - url: https://example.com
        title: "External Link"

```
