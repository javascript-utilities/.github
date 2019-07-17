# Contributing to JavaScript Utilities


Thanks for even thinking about it!


As this Organization grows portions of this document may be moved to GitHub Pages; the following are not _set in stone_ rules but guidelines, and much like other files maintained by this Organization the following may be edited via a _`Pull Request`_.



------


#### Table of Contents


- [:customs: Code of Conduct](#code-of-conduct)

- [How to Contribute](#how-to-contribute)

  - [Open Issues](#open-issues)
  - [Report Bugs](#report-bugs)
  - [Suggest Enhancements](#suggest-enhancements)

- [Style Guidelines](#style-guidelines)

  - [JavaScript](#javascript-style-guidelines)
  - [HTML and CSS](#html-and-css-style-guidelines)
  - [MarkDown](#markdown-style-guidelines)
  - [FrontMatter and YAML](#frontmatter-and-yaml-style-guidelines)

- [Local Development Setup](#local-development-setup)

  - [Linux or Mac](#linux-development-setup)
  - [Windows](#windows-development-setup)

- [Git Tips](#git-tips)

  - [Git Commits](#git-commit-tips)
  - [Git Branching](#git-branch-tips)

    - [Orphan](#orphaned-git-branches)
    - [Development](#development-git-branches)

  - [Git Merging](#git-merge-tips)

- [Pull Requests](#pull-requests)

- [:copyright: License](#license)

- [Attribution](#attribution)


------


## Code of Conduct


**TLDR**
This Organization is a semiprofessional public place, _`Treat others as though they have access to your toothbrush`_, and _`Code and Facts should be seasoned with Levity and Tact`_. Review the [full-length version][branch__current__code_of_conduct] if so inclined.


___


## How to Contribute


The goal is, as always, useful code and documentation, though <sub>[![Support][badge__support]][relative_link__support]</sub> is always appreciated. Sharing Repositories maintained by this Organization is an excellent way to contribute if none of the following options are applicable, because the more eyes on a Code Base the more likely it seems that bugs will be found and fixed. 


### Open Issues


Join the <sub>[![Contributors][badge__contributors]][relative_link__network_members]</sub> issuing Pull Requests that close available <sub>[![Open Issues][badge__issues]][relative_link__issues]</sub>. [New Issues][relative_link__issues_new] may be opened for Reporting Bugs and Suggesting Enhancements. General tips on formatting [MarkDown](#markdown-style-guidelines) guidelines from this document are advisable to follow. However, please search for existing similar Issues first; example search for [`memory-leaks`](https://github.com/javascript-utilities/browser-storage/search?q=memory-leaks&type=Issues) from the `browser-storage` repository.


### Report Bugs


Use the [`bug_report.md`][branch__current__bug_report] Template by selecting _`Bug report`_ from the GitHub web interface when opening a [New Issue][relative_link__issues_new]. Please be detailed and try to include all relevant information within the OP (Original Post). Additionally, if clarifications or more information is requested or discovered, then editing the OP is preferred to adding another post or opening a new issue.


Bugs may also be reported via a Pull Request that purposes fixes, in which case skip opening an Issue and instead use the `:bug:` emoji as the first _word_ of the fix commit.


**Example Bug Report Pull Request**


```Bash
git checkout master
git merge --strategy-option theirs --squash dev-master


git commit -F- <<'EOF'
:bug: memory leak `cow_bell(solo_count_down)` when `solo_count_down=NaN`



**Fixes**
`new-script.js` file, `NaN` passed to `cow_bell(solo_count_down)` no longer causes memory leaks
EOF


git push forked master
```


### Suggest Enhancements


Use the [`feature_request.md`][branch__current__feature_request] Template by selecting _`Feature request`_ from the GitHub web interface when opening a [New Issue][relative_link__issues_new]. Whenever possible provide example/pseudo code along with a detailed description of what needs solved. Or in other-words; napkin-sketches are permitted if it gets helps readers better understand the scope.


Adding new features can also be done via a Pull Request


**Example Enhancement Pull Request**


```Bash
git checkout gh-pages
git merge --strategy-option theirs --squash dev-gh-pages


git commit -F- <<'EOF'
:apple: Cow Bell solos supported on Mac OS



**Additions**


`new-script.js` file;


- `constructor()` method now preforms feature detection for Mac OS

- `solo()` method inspects `ClassName.is_mac` on caught _unsupported_ errors
EOF


git push forked gh-pages
```


___


## Style Guidelines


One does **not** have to use all of the following and this is intended to help keep things consistent between all repositories maintained by this Organization. Or in other-words, no-one will _should_ get offended if a new line is forgotten or similar, but please do **not** break anything when issuing Pull Requests.


- Code that operates as intended is as important as documentation that is comprehensible, so do **not** sacrifice readability for anything

- In most cases two (**`2`**) should be used between sections, one (**`1`**) between sub-sections, and three (**`3`**) between headers and footers or _boilerplate_ sections

- URLs may _break_ column width limits

- Tabs shall be a sequence of two spaces (**`  `**)

- Project, File, and Directory names _should_ be lowercase, with hyphens (**`-`**) in place of spaces (**` `**) except where GitHub requires otherwise

- Documentation should be no more than `1024` lines per file

- Code specific (`.js`) files should aim for less than `512` lines of actionable code, and _doc-strings_/comments should not exceed `20%` of total lines within such files

- _Unix-ish_ new-lines (**`\n`**) are to be used within all files, and aside from very few exceptions any Pull Request using other line-breaks will be rejected until corrected


### JavaScript Style Guidelines


- Lines should not exceed `120` columns wide for code and no more than `80` columns wide for comment blocks

- Comments in most cases should precede code and be formated for digestion by [JSDoc][jsdoc__block_tags] or similar tools

- Use `var` sparingly, and `const`/`let` variable assignments where necessary

- Return _something_ from Methods or Functions even if that is a boolean status of some object mutation

- `throw` and `except` errors! Preferably of specific types or of a descriptive nature

- `continue` past non-matches within loops to avoid _over-nesting_ of conditional logic


**`assets/javascript-modules/deep-thought/deep-thought.js`**


```JavaScript
class DeepThought {
  /**
   * Does some classy things with numerical objects
   * @copyright S0AndS0 2019 GNU AGPL version 3
   * @param {string} operation - Mathematical operation to perform
   * @this DeepThought
   */
  constructor(operation) {
    this.valid_operations = ['multiply', 'divide', 'subtract', 'sum', 'add'];
    if (this.valid_operations.indexOf(operation) == -1) {
      throw new Error('Valid Operations are -> ' + this.valid_operations);
    }
    this.operation = operation;
  }

  /**
   * @param {number} life         - First number to apply `this.operation` to
   * @param {number} the_universe - Second number to apply `this.operation` to
   * @returns {?number}
   * @this DeepThought
   */
  calculate_meaning(life, the_universe) {
    let results_of_everything = NaN;
    switch (this.operation) {
      case 'multiply':
        results_of_everything = life * the_universe;
        break;
      case 'divide':
        results_of_everything = life / the_universe;
        break;
      case 'subtract':
        results_of_everything = life - the_universe;
        break;
      default:
      results_of_everything = life + the_universe;
    }
    return results_of_everything;
  }
}
```


### HTML and CSS Style Guidelines


- Try to be concise because Organizations such as [Liquid Utilities][github__liquid_utilities] and [SCSS Utilities][github__scss_utilities] should be contributed to for compiling HTML and CSS from complex data structures and/or building Templates

- Lines should not exceed `120` columns wide whenever possible

- Use _`BEM`_ or similarly descriptive formatting for class names

- Use HTML5 tags that are well supported and pre HTML5 tags anywhere else

- Only in-line `<style>` and/or `<script>` tags for quick examples, otherwise split things into separate Labeled Code Blocks and include relative `src="script.js"` or `href="style.css"` Attributes


**`assets/css/main.css`**


```CSS
/**
 * Style container__ classes
 */
.container__header,
.container__main_content,
.container__footer {
  margin-left: 50px;
  margin-right: 50px;

}

.container__main_content {
  margin-top: 100px;
  margin-bottom: 100px;
}

.container__footer {
  position: fixed;
  bottom: 0;
  max-height: 100px;
}


/**
 * Style header__ classes
 */
.header__title {
  text-align: left;
}

.header__description {
  text-align: right;
}
```


**`index.html`**


```HTML
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <title>Words for Tab or Window Title Bar</title>


    <meta charset="utf-8">
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">


    <link type="text/css" href="assets/css/main.css" rel="stylesheet"/>


    <script type="text/javascript" src="assets/javascript-modules/deep-thought/deep-thought.js"></script>

    <script type="text/javascript">
      import DeepThought from 'assets/javascript/deep-thought/deep-thought.js';
      /**
       * Example usage for DeepThought class
       */
      const thinker = new DeepThought('multiply');


      /**
       * @param {number} n - Number of iterations and length of returned list
       * @returns {list}
       */
      function think_until(n) {
        let thoughts = [];
        for (let i = 0; i < n; i++) {
          thoughts.push(thinker.calculate_meaning(5, i))
          console.log('Thought ' + i + ' -> ' + thoughts[i]);
        }
        return thoughts;
      }
    </script>

  </head>


  <body onload="think_until(5);">
    <header class="container__header">
      <h1 class="header__title">Title of Document</h1>

      <p class="header__description">
        Short description about content of document, project, and/or code
      </p>
    </header>

    <div class="container__main_content">
      <h4>Table of Contents</h4>
      <ul>
        <li><a href="#first-section">First</a></li>
      </ul>

      <h2 id="first-section">First Section</h2>
      <p>A thing or two about git...</p>
    </div>

    <div class="container__footer">
      <h2>Site Footer</h2>
    </div>
  </body>
</html>
```


### MarkDown Style Guidelines


- There is no set column width limits for MarkDown files, but do not get carried away because the focus should be on getting readers _up to speed_

- External links are permitted but try to keep it to a minimum and instead refer to built-in `man` and/or `help` document wherever possible

- Relative links to other files or locations within documentation is preferred; except for _cross-branch_ linking in which case absolute links are preferred

  - Links be should organized into a Links Section bellow the Content, after three (**`3`**) blank lines
  - Link Names should use two underscores between base location and file or title

- Lists should have one blank line between first layer of items

  - Inner lists should be tabbed in by two (**`2`**) spaces and have no blank lines between items of the same level
  - Nesting lists beyond one layer is discouraged and information should be restructured when it becomes tempting to do otherwise

- Provide a _`Table of Contents`_ section when headings become numerous and use three underscores (**`___`**) as Dividers between main sections

  - Only one _level one_ heading (lines prefixed with a single **`#`** one hash-sign) may be included in a MarkDown document and only when no _`FrontMatter`_ defines a **`title:`** property
  - Main Sections should have a _level two_ heading (prefixed by **`##`** two hash-signs)
  - Sub-Sections should have a _level three_ heading, and nesting beyond this is discouraged

- Code Blocks should have the related language defined as proper nouns, eg. `JavaScript` not `javascript` and `Bash` not `bash`

  - Formatting within code blocks should follow related guidelines for that language
  - Code blocks should not exceed **`120`** lines in length
  - Use links to files instead of copying files into Code Blocks
  - Title code blocks with bold back-ticks and example path for re-use elsewhere within documentation...


```MarkDown
**`file-name.ext`**
```


- Two blank lines should go between Sections, Sub-Sections, Dividers, Code Blocks, and List Blocks.

- Three blank lines should go between Description, and between Content and Links Section


**`readme.md`**


```MarkDown
# Title of Document


Short description about content of document, project, and/or code



------


#### Table of Contents


- [First](#first-section)

- [Second](#second-section)

  - [JavaScript Time](#javascript-time)
  - [JavaScript Variables](#javascript-variables)

- [End](#end-section)


------


## First Section


A thing or two about `git`...


\```Bash
_name='S0AndS0'
_repo='.github'

git clone git@github.com:${_name}/${_repo}.git
\```


Maybe a table with some columns to organize something...


| Column One | Column Two |
|------------|------------|
| cell       | cell       |
| cell       | cell       |


___


## Second Section


Something notes about _`JavaScript`_


### JavaScript Time


**[`AnotherFile.js`][branch__current__another_file]**


\```JavaScript
const today = new Date();

console.log('today -> ' + today);
\```


### JavaScript Variables


Interactive console examples...

\```JavaScript
const once_set = 'Unforgeable';
let set_this_time = 1;
var otherwise = false;
\```


... inspect behavior of re-setting or overwriting things...


\```JavaScript
otherwise = true;
set_this_time = 255;
once_set = 'Remember';
\```


___


## End Section


In summation this is the general outline of MarkDown formatting.


Check [`gh-pages`][branch__gh_pages] branch for example usage and documentation.


See [Somewhere Else][example__somewhere_else] for more details on something else.



[branch__current__another_file]: AnotherFile.js


[branch__gh_pages]: ../tree/gh-pages


[example__somewhere_else]: https://example.com/somewhere-else.html
```


> Note, any prefixed back-slashes (`\` ) should be removed from above example


### FrontMatter and YAML Style Guidelines


- Try to keep custom properties to a minimum; [Liquid Utilities][github__liquid_utilities] may be a better Organization to contribute to for more complexity

- Avoid building complex data structures with FrontMatter or YAML, again [Liquid Utilities][github__liquid_utilities] may be a better Organization to contribute to for such things


**`_data/default-frontmatter.yml`**


```YAML
author: S0AndS0
description: Where JavaScript is utilized
title: JavaScript Utilities
```


**`_posts/2019-06-30-welcome.md`**


```FrontMatter
---
title: Welcome to JavaScript Utilities
description: A post for welcoming readers
date: 2019-06-30 13:42:11 -0700
---



Dedicated to utilizing JavaScript on static web hosts such as GitHub Pages.


Currently under construction, but do check back often for future developments.
```


___


## Local Development Setup


For repositories that do **not** include a `_config.yml` file within a `gh-pages` branch, then Python version 3 is an easy way most systems to preform local testing and development. For repositories that **do** contain a `_config.yml` file then Jekyll is required instead, see the [Jekyll Admin](https://github.com/S0AndS0/Jekyll_Admin) for setup and automation scripts built to make such setup tasks a little swifter.


### Linux Development Setup


> The following steps and variable usage may also work on Mac, and may be Windows **if** a Bash shell is available.


**Shared Variables**


```Bash
_git_name='your-name'
_organization='javascript-utilities'
_repository='project-name'


_https_url="https://github.com/${_organization}/${_repository}.git"
_git_url="git@github.com:${_organization}/${_repository}.git"
_fork_url="git@github.com:${_git_name}/${_repository}.git"
```


> The above Bash variables will be referenced within following sub-sections, modify the values to suite the Forked Repository.


Setup remotes via one of the following;


1. Clone fork and setup remotes


```bash
mkdir -vp "${HOME}/github/${_git_name}"
cd "${HOME}/github/${_git_name}"


git clone --origin forked "${_fork_url}"


cd "${_repository}"
git remote add github "${_git_url}"
```


2. Point existing clone to fork


```Bash
cd "${HOME}/github/${_organization}/${_repository}"
git remote add forked "${_fork_url}"

git remote rename origin github
```


In either case _`git push forked master`_ _should_ push to the forked repository URL, and _`git fetch github master`_ will download any updates from this Organization. If any updates where downloaded then be sure to merge them before issuing a Pull Request.


If Python version `3` or greater is available then a script like _`serve_pwd_to_locahost.sh`_ may be used to serve some of the example web files, where available...


```bash
#!/usr/bin/env bash


__git_project_owner__="${1:-javascript-utilities}"
__git_project_name__="${2:-browser-storage}"


cd "${HOME}/github/${__git_project_owner__}/${__git_project_name__}" || exit 1
python3 -m http.server --bind 127.0.0.1 8080
```


... which could be run via...


```bash
bash serve_pwd_to_locahost.sh
```


... and point a web browser at `http://localhost:8080`


### Windows Development Setup


An untested but likely functional `Batch` script version of `serve_pwd_to_locahost.sh` might look like...


**`serve_pwd_to_locahost.bat`**


```Batch
@ehco off


set __git_project_owner__='javascript-utilities'
set __git_project_name__='browser-storage'


cd /D %UserProfile%\github\%__git_project_owner__\%__git_project_name__ || exit /b
python3 -m http.server --bind 127.0.0.1 8080


pause
```


... of course Pull Requests are welcomed for correcting anything that might be erroneous.


> Note, for references to shared variables within following sections perhaps use something like...


```Batch
set _git_name='your-name'
set _organization='javascript-utilities'
set _repository='project-name'

set _https_url="https://github.com/%_organization/%_repository.git"
set _git_url="git@github.com:%_organization/%_repository.git"
set _fork_url="git@github.com:%_git_name/%_repository.git"
```

___


## Git Tips


This will not be an in-depth or exhaustive guide on `git` usage, as the preexisting documentation available via commands such as _`git help`_ and _`git help submodule`_ are thorough.


> Note, see the _`Shared Variables`_ portion within the [Linux Development Setup](#linux-development-setup) section within this document for example values.


### Git Commit Tips


- First line should not exceed `74` columns wide and punctuation such as apostrophes, quotes, and periods (`"'."`) should be avoided

- First line should be separated from message content by three blank lines

- While not required the following emoji may be used as the first _word_ of commit messages

  - :tada:             `:tada:` for `Initial Commit` of repository, **not** to be used when re-naming files
  - :memo:             `:memo:` for documentation, new file or content, related commits
  - :art:              `:art:` for format and/or structure related changes
  - :coffee:           `:coffee:` for JavaScript additions and/or changes
  - :fire:             `:fire:` for deletion of files, code, or documentation
  - :hankey:           `:hankey:` please avoid needing to use as it's for when moving files or content between branches
  - :dizzy:            `:dizzy:` when re-naming or moving files within a branch, it'll happen for newer projects but need for use is to be avoided past version **`0.0.5`**

  - :bug:              `:bug:` for _stomping_ bugs in general
  - :smoking:          `:smoking:` for resource bug fixes, eg. memory leaks, recursion limits, CPU load
  - :facepunch:        `:facepunch:` when _blaming_ one's self and new commit is to fix bug from recently past commit
  - :do_not_litter:    `:do_not_litter:` when _blaming_ another's recent changes for requiring new committed bug fix
  - :lock:             `:lock:` for security related fixes

  - :penguin:          `:penguin:` for fixing or improving Linux performance or compatibility
  - :apple:            `:apple:` for fixing or improving Apple/Mac performance or compatibility
  - :checkered_flag:   `:checkered_flag:` for fixing or improving Windows/MS performance or compatibility

  - :arrow_up:         `:arrow_up:` for tracking upgraded dependencies
  - :arrow_down:       `:arrow_down:` for tracking downgraded dependencies
  - :bookmark:         `:bookmark:` for Tagging Releases and Request For Comments (RFC)

  - :white_check_mark: `:white_check_mark:` for adding tests
  - :green_heart:      `:green_heart:` when fixing Continuous Integration builds

  - :stars:            `:stars:` for accepting a Pull Request
  - :no_entry:         `:no_entry:` for rejecting a Pull Request



- Additional notes should follow [Markdown Style Guidelines](#markdown-style-guidelines); except for headings as _`#`s_ are considered comments by default and thus ignored by many `commit` message handlers, see following example for other formatting differences


```Bash
git add README.md
git commit -F- <<'EOF'
:memo: Added more content to readme file and spell-checked documentation



**Additions**
Links where tested locally and new content should explain things better.


**Corrections**
Other than spelling there where a few confusing spots that where also reworded.
EOF
```


### Git Branch Tips


This Organization encourages the use of _`orphan`_ branches for separating Code to be included in other projects from Documentation and Usage Examples. Non-orphaned development branches are encouraged when adding features or fixing bugs.


**`master`** branch may only contain;


- `.git/` directory, required for version tracking and logging changes

- _`readme.md`_ file, used for documenting installation and/or usage

- _`script-name.js`_ file, any dependencies should be listed within the _`.gitmodules`_ file under the **`gh-pages`** branch

- _`lib`_ directory, should **only** be used for files that directly support the _`script-name.js`_ file, otherwise please split out reusable code to separate repositories for including as submodules within the `gh-pages` branch


**`gh-pages`** branch may contain;


- `index.html` file, when **no** `_config.yml` file is present; used to demonstrate live example of what _`script-name.js`_ file does, when a `_config.yml` file **is** present; used as the _home page_ for the Repository documentation and link to the test page(s)

- `assets/javascript-modules/project-name/` directory/submodule path should point to the _`https`_ GitHub Clone URL and contain the **`master`** branch code for `project-name`

- `_posts/` or `collection-name/` directories, should contain collections of pages and/or posts documenting anything about the Repository that requires more detail or examples


#### Orphaned Git Branches


The following code blocks demonstrate how new projects are authored and how specific branches are _orphaned_...


**Example `master` branch initialization**


```Bash
## Setup a new git repository
mkdir -vp "${HOME}/github/${_organization}"
cd "${HOME}/github/${_organization}"

git init "${_repository}"
cd "${_repository}"


## Add the following files...
# new-script.js
# README.md
# LICENSE
## ... then track with git
git add new-script.js README.md LICENSE


git commit -F- <<'EOF'
Initial Commit



New Project that does stuff for things


**Additions**


- `new-script.js` file, tests on a browser or two seem error free
- `README.md` file, documentation about `NewClass` from `new-script.js`
- `LICENSE` file, GNU AGPL 3.0 License added to remain consistent with Organization
EOF


## Add remote URL and push `master` branch to forked remote
git remote add 'github' "${_git_url}"
git push forked master
```


**Example `gh-pages` branch initialization**


```Bash
cd "${HOME}/github/${_organization}/new-project"


## Orphan and remove tracking of `master` branch Code and Documentation files
git checkout --orphan gh-pages
git rm --cached new-script.js
git rm --cached README.md


## Add HTTP URL pointing to `master` branch as a submodule
_submodule_destination="assets/javascript-modules/${_repository}"

git submodule add -b master "${_https_url}" "${_submodule_destination}"
git submodule update --init --recursive


## Write an example `index.html` file, and edit the `README.md` file
git add index.html
git add README.md
git add LICENSE


## Commit orphaned branch and push to GitHub
git commit -F- <<'EOF'
Initial Commit



This branch is orphaned to document the `master` branch


**Additions**


- `LICENSE` file, GNU AGPL 3.0 License added to remain consistent with Organization
- `README.md` file, documentation on how to setup and test code from `master` branch
- `index.html` file, live demonstration example page, enables debugging of `NewClass`


**Submodules**


- `assets/javascript-modules/project-name`, tracked for `NewClass` code
EOF

git push forked gh-pages
```


#### Development Git Branches


Development branches are excellent for privately tracking series of changes for new features or especially pervasive bugs. Merging with a _`squash`_ commit back to one of the _main line_ branches prior to publicly pushing to a fork is encouraged, however, please try to be _targeted_ as to what each committed change pertains to.


**Example `dev-master` branch initialization**


```bash
cd "${HOME}/github/${_organization}/new-project"


git checkout master
git checkout -b dev-master
```


Commit changes to `dev-master`, then after tests have passed preform a `squash` merge of `dev-master` from the `master` branch


```Bash
git checkout master
git merge --strategy-option theirs --squash dev-master

git commit -F- <<'EOF'
:bug: Chrome and Mozilla treat DOM triggered JavaScript differently



**Edits**
Chrome does not like JavaScript triggering JavaScript via DOM; must force UI syncing within `syncUI()`
EOF


git push forked master
```


### Git Merge Tips


**Never** `git merge master` from the `gh-pages` branch, and definitely do **not** `git merge gh-pages` when the `master` branch is checked out; orphaned branches should only be merged to and from their respective development (**_`dev-`_**) prefixed branches.


Squash merging is preferred for targeted edits, eg...


```bash
git checkout master
git merge --strategy-option theirs --squash dev-master


git commit -F- <<'EOF'
:coffee: Asking permission from checkboxes before modifying state



**Changes**
`new-script.js` file, `uncheck_all()` continues on unchecked boxes and `check_all()` continues on checked boxes
EOF


git push forked master
```


Also be wary of _`rm`_ vs _`git rm`_ and _`mv`_ vs _`git mv`_ commands, when merging from a development branch back to one of the _mainline_ branches the _non-`git`_ wrapped commands will **not** update state between branches, and Pull Requests that confuse version management will be rejected.


___


## Pull Requests


Issuing Pull Requests to repositories maintained by this Organization will only be considered **if** shared under the same licensing defined under [License](#license) section of this document. Please use any relevant examples from the [`pull_request.md`][branch__current__pull_request] Template and adherer to the Style Guidelines for [Git Commits](#git-commit-tips)



___


## License


By default all Code (including Documentation) are shared under version three (**`3`**) of the GNU AGPL license.


```
Contributing Guidelines for JavaScript Utilities
Copyright (C) 2019  S0AndS0

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation; version 3 of the License.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```


___


## Attribution


Portions of this document, such as emoji usage, where inspired by [_`contributing.md`_][github__atom__contributing] guidelines from the Atom IDE development team.



[relative_link__issues]: issues
[relative_link__issues_new]: issues/new
[relative_link__network_members]: network/members
[relative_link__support]: SUPPORT.md


[branch__current__code_of_conduct]: CODE_OF_CONDUCT.md
[branch__current__bug_report]: ISSUE_TEMPLATE/bug_report.md
[branch__current__feature_request]: ISSUE_TEMPLATE/feature_request.md
[branch__current__pull_request]: PULL_REQUEST_TEMPLATE/pull_request_template.md
[branch__current__readme]: README.md

[github__liquid_utilities]: https://github.com/liquid-utilities
[github__scss_utilities]: https://github.com/scss-utilities

[github__atom__contributing]: https://github.com/atom/atom/blob/master/CONTRIBUTING.md


[jsdoc__block_tags]: https://jsdoc.app/#block-tags


[badge__issues]: https://img.shields.io/github/issues/javascript-utilities/.github.svg
[badge__contributors]: https://img.shields.io/github/forks/javascript-utilities/.github.svg?color=005571&label=Contributors


[badge__support]: https://img.shields.io/badge/&hearts;-Support-lightgray.svg?labelColor=success&color=gray
