---
comments: true
title: git commit style guid from Udacity
published: 2020-3-27
updated: 2020-3-27
tags: [git]
categories: [development]
---

Udacity의 git commit style guide다.



원본 [페이지](https://udacity.github.io/git-styleguide/)

# Commit Messages

### 1. Message Structure

A commit messages consists of three distinct parts separated by a blank line: the title, an optional body and an optional footer. The layout looks like this:

```
type: subject

body

footer
```



### 2. Title

#### The type

- **feat:** a new feature
- **fix:** a bug fix
- **style:** formatting, missing semi colons, etc; no code change
- **refactor:** refactoring production code
- **test:** adding tests, refactoring test; no production code change
- **docs:** changes to documentation
- **chore:** updating build tasks, package manager configs, etc; no production code change

#### The subject

```
- no greater than 50 characters
- begin with a capital letter
- do not end with a period
- Use an imperative tone
```



### 3. Body

```
- optional
- Use the body to explain the what and why of a commit, not the how.
- limit the length of each line to no more than 72 characters.
```



### 4. Footer

```
- optional
- used to reference issue tracker IDs.
```



### example

````
feat: Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
````

