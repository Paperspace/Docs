# Notebook Workspace Include Files

On notebook stop we copy some files to your [storage provider](../../../data/data-overview/private-datasets-repository/storage-providers.md) so you can see your notebook files in the offline view and so other users can fork your notebook. By default, the list of files is fairly restrictive and includes `.ipynb` and `.md` files and if your workspace is a git repo we will upload any files that are tracked by git. The more files you include the more time your notebook will spend "tearing down" and "setting up".

You can control which files are uploaded by providing a `.notebookinclude` file at `/notebooks/.notebookinclude`. This file uses [`.gitignore`](https://git-scm.com/docs/gitignore) syntax however, the patterns _include_ files instead of ignoring them. Negative patterns are supported and _exclude_ files from being uploaded.

## Default File

The default patterns are always provided and if you supply any user patterns it is like they are appended to the following ignore file:

```text
*.md
*.ipynb

# and all of the files from `git ls-files`
```

## Examples

### Upload all pngs but skip my dataset

```text
*.png # include all png files
!datasets/**/*.png # exclude the ones in my datasets
```

### Change the default rules

This file will upload `.ipynb` files but skip `.md` files:

```text
!*.md
```

## Full Specification

* A blank line matches no files, so it can serve as a separator for readability.
* A line starting with \# serves as a comment. Put a backslash \("`\`"\) in front of the first hash for patterns that begin with a hash.
* Trailing spaces are ignored unless they are quoted with backslash \("`\`"\).
* An optional prefix "`!`" which negates the pattern; any matching file included by a previous pattern will become excluded again. Put a backslash \("`\`"\) in front of the first "`!`" for patterns that begin with a literal "`!`", for example, "`\!important!.txt`".
* The slash `/` is used as the directory separator. Separators may occur at the beginning, middle or end of the `.notebookinclude` search pattern.
* If there is a separator at the beginning or middle \(or both\) of the pattern, then the pattern is relative to the directory level of the particular `.notebookinclude` file itself. Otherwise the pattern may also match at any level below the `.notebookinclude` level.
* If there is a separator at the end of the pattern then the pattern will only match directories, otherwise the pattern can match both files and directories.
* For example, a pattern `doc/frotz/` matches `doc/frotz` directory, but not `a/doc/frotz` directory; however `frotz/` matches `frotz` and `a/frotz` that is a directory \(all paths are relative from the `.notebookinclude` file\).
* An asterisk "`\*`" matches anything except a slash. The character "`?`" matches any one character except "`/`". The range notation, e.g. `[a-zA-Z]`, can be used to match one of the characters in a range. See `fnmatch(3)` and the `FNM_PATHNAME` flag for a more detailed description.
* Two consecutive asterisks \("`\*\*`"\) in patterns matched against full pathname may have special meaning:
  * A leading "`**`" followed by a slash means match in all directories. For example, "`**/foo`" matches file or directory "`foo`" anywhere, the same as pattern "`foo`". "`\*\*/foo/bar`" matches file or directory "`bar`" anywhere that is directly under directory "`foo`".
  * A trailing "`/**`" matches everything inside. For example, "`abc/**`" matches all files inside directory "`abc`", relative to the location of the `.notebookinclude` file, with infinite depth.
  * A slash followed by two consecutive asterisks then a slash matches zero or more directories. For example, "`a/\*\*/b`" matches "`a/b`", "`a/x/b`", "`a/x/y/b`" and so on.
  * Other consecutive asterisks are considered regular asterisks and will match according to the previous rules.

