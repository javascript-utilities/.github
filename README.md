# JavaScript Utilities


This GitHub organization is dedicated to building JavaScript tools for static web sites, such as those hosted by GitHub Pages. Other than the `.github` repository all others maintained by this Organization _should_ be able to be included within other GitHub projects as a `submodule`.


------


#### Table of Contents


- [&#9889; TLDR of Organization][tldr-of-organization]

- [&#9851; Submodules][submodules]

  - [Installation][submodule-installation]
  - [Updates and Cloning Considerations][submodule-updates-and-cloning-considerations]
  - [Version Locking][submodule-version-locking]


------


## TLDR of Organization
[tldr-of-organization]:
  #tldr-of-organization
  "&#9889; Synopsizes and links for more information"


[![Security][badge__security]][relative_link__security]
Security issues related to Languages, Browsers, Operating Systems, and such _should_ be reported to the respective development team(s), check the _`Security`_ section of individual repositories for any specific security related considerations. Otherwise please review the [Security Guidelines][relative_link__security] for practices, and reporting security related issues regarding projects maintained by this Organization


[![Contributors][badge__contributors]][relative_link__contributors]
Please review the [Contributing Guidelines][relative_link__contributing] and [Code of Conduct][relative_link__code_of_conduct] prior to opening _`Issues`_ or _`Pull Requests`_, and sharing projects maintained by this Organization with others is also a valid method of contributing. Hint, GitHub's documentation on [Forking][help_fork] and issuing [Pull Requests][help_pull_request] are excellent resources if these are new terms.


[![Support][badge__support]][relative_link__support]
It feels good when others find projects like these valuable, so let the maintainers of this Organization know when/if that occurs.


## Submodules
[submodules]:
  #submodules
  "&#9851; The hows, whys, and what fores submodules from Git are used"


For compatibility with GitHub Pages this Organization makes persistent use of _`Git`_ submodules.


**Example variables**


> Note, the following are referenced within next few sections, all of which _should_ be entered within a _`Bash`_ shell


```Bash
_module_name='browser-storage'
_module_relative_path="assets/javascript-modules/${_module_name}"
_module_https_url="https://github.com/javascript-utilities/${_module_name}.git"

_account_name='your-name'
_project_name='new-project'
_project_git_url="git@github.com:${_account_name}/${_project_name}.git"
```


### Submodule Installation
[submodule-installation]:
  #submodule-installation
  "Git tracking within a Git tracked repository!"


Instead of _polluting_ package management systems such as NPM and requiring extra dependencies, utilizing _`Git`_ submodules one can track a repository from within another repository; all without confusing _`Git`_!<sub>...mostly</sub>.


**Tracking _`_module_name`_ within _`_project_name`_**


```Bash
## Make a new repository if necessary
# git init "${_project_name}"

## Change current working directory to project root
cd "${_project_name}"

## Make general path for modules and track
##  submodules under a subdirectory
mkdir assets/javascript-modules
git submodule add -b master "${_module_https_url}" "${_module_relative_path}"
```


**Example `git status`**


```git
On branch gh-pages

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .gitmodules
	new file:   javascript-modules/browser-storage
```


Check that something similar to the above results from `git status`, perhaps link to [Cloning Considerations](#submodule-cloning-considerations) or copy examples contained there to documentation for _`_project_name`_, then `commit` and `push` changes.


### Submodule Updates and Cloning Considerations
[submodule-updates-and-cloning-considerations]:
  #submodule-updates-and-cloning-considerations
  "Just a few things to keep in mind when utilizing submodules"


**Cloning a repository that unitizes submodules**


```Bash
git clone --recurse-submodules "${_project_git_url}"
```


The above or similar _should_ make it's way into documentation for _`_project_name`_, as should the following for those that may have already cloned _`_project_name`_...


```Bash
git submodule update --init --recursive
git submodule update --merge
```


Sometimes the _`HEAD`_ for a submodule can become detached, if that is bothersome then the following may be of use too...


```Bash
cd "${_module_relative_path}"
git checkout master
git pull
```


### Submodule Version Locking
[submodule-version-locking]:
  #submodule-version-locking
  "For those that audit every dependency prior to version upgrades"


```Bash
```


[git_book__submodules]: https://git-scm.com/book/en/v2/Git-Tools-Submodules


[help_fork]: https://help.github.com/en/articles/fork-a-repo
[help_pull_request]: https://help.github.com/en/articles/about-pull-requests
[help_github_pages__submodules]: https://help.github.com/en/articles/using-submodules-with-pages


[relative_link__code_of_conduct]:
  CODE_OF_CONDUCT.md
  "Expectations of contributor and maintainer behavior towards others"

[relative_link__contributing]:
  CONTRIBUTING.md
  "Pull Request or Issue tips"

[relative_link__contributors]:
  graphs/contributors
  "Join us?... promise there are no brain slugs..."

[relative_link__security]:
  SECURITY.md
  "Practices and reporting of security issues"

[relative_link__support]:
  SUPPORT.md
  "Thanks for even thinking about it!"

[relative_link__issues]:
  issues
  "Search for Open or Closed issues"

[relative_link__members]: network/members


[badge__contributors]: https://img.shields.io/github/contributors/javascript-utilities/.github.svg?label=Contributors

[badge__support]: https://img.shields.io/badge/&#x2764;-Support-lightgray.svg?labelColor=success&color=gray
[badge__security]: https://img.shields.io/badge/&#9888;-Security-lightgray.svg?labelColor=FF9400&color=gray
