# ReadMe Summary Generation on Category Directories
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

### About
This repository contains code to automatize the generation of readmes for the different contribution in the
repo of the [DevOps course](https://github.com/KTH/devops-course/) of KTH.
This code is specific to the structure of the specified repository, but it can easily be adapted to another form of a repository.


## Overview

In this repo, you find a GitHub action on pushes that execute a script to generate the readme of the different types of contributions.
This generates a list of information forming a summary of every contribution in the category.
The action will generate a Pull Request with all the list updated without modifying specific rules or previous instructions in the category readme.

## How It Works
In order to do update the readmes automatically,
- The GitHub action trigger on specific modification in the contributions' directory [`contributions/demo`](contributions/demo) for example.
- A Python script analyses each directory and try to retrieve important information in the readme:
  * Title of the contribution
  * Name of the contributors
  * Email of the contributors
  * GitHub of the contributors
- The script displays the date in the format of the list with a link to the different contributions and updates the category readme.
- At the same time, the script print which contribution does not contain a proper README.md.
- The GitHub action gets the updates and creates an automatic Pull-Request.

## Formats Accepted

### Structure

To allow a good execution of the script, each category folder should be placed in the [`contributions`](contributions) folder.
The contributions should be in the format of the kebab case to separate the contributors `contributorone-contributortwo`.

In other word, the structure of the repo to analyse is the following: 

```
contributions/
|-- category1/
|    |-- contributorone-contributortwo/ 
|    |    |-- README.md
|    |    +-- ...
|    |-- contributorthree-contributorfour/ 
|    |    |-- README.md
|    |    +-- ...
|    |
|    +--  .../
|    
|-- category2/
|    |-- contributorfive-contributorsix/ 
|    |    |-- README.md
|    |    +-- ...
|    |
|    +--  .../
|    
+-- complexe-category
     |-- sub-directory1/ 
     |    |-- contributorone-contributortwo/ 
     |    |    |-- README.md
     |    |    +-- ...
     |    +-- contributorthree-contributorfour/ 
     |         |-- README.md
     |         +-- ...
     |-- sub-directory2/ 
     |    |    |-- contributorone-contributortwo/ 
     |    |    |-- README.md
     |    |    +-- ...
     +-- sub-directory3/ 

```

The result in the readme of the `category1` will looks like: 

```markdown
- [__tittle of the contribution__](contributorone-contributortwo/) by:
  * Name Surname, email: email@something.com, github: [GithubAcount](https://github.com/user)
  * Name2 Surname2, email: email2@something.com, github: [otherAcount](https://github.com/user)
- [__tittle of the second contribution__](contributorthree-contributorfour/) by:
  * Name3 Surname3, email: email@something.com, github: [GithubAcount](https://github.com/user)
  * Name4 Surname4, email: email2@something.com, github: [otherAcount](https://github.com/user)
- ...
```

However, the result of the readme for the `complexe-category` will looks like:

```markdown
- [sub-directory1](sub-directory1/)
  * [__Fantastic Tittle__](sub-directory1/contributorone-contributortwo/) by:
    + Good Name, email: email@somewher.net
    + Anna Nicename, email: cccc@somewhere.net
  * [__Demo proposal: Another good Tittle__](sub-directory1/contributorthree-contributorfour/) by:
    + Peter Greatname, email: aaaaaa@something.com, github: https://github.com/user
    + Oliver Goodname, email: bbbbb@something.com, github: https://github.com/anna

- [sub-directory2](sub-directory2/)
  * [__Great Tittle__](sub-directory2/contributorone-contributortwo/) by:
    + Good Name, email: email@somewher.net
    + Anna Nicename, email: cccc@somewhere.net
  * ...
...
```

### README.md Format
Inside a contribution folder, the script will analyse its readme and try to look for a title with minimal `#`.
Then, it will try to find a members section of the format:
```(markdown)
# tittle of the contribution

## Member(s)

Name Surname (email@something.com) [GithubAcount](https://github.com/user)
Name2 Surname2 (email2@something.com) [otherAcount](https://github.com/user)
```

The result should look like this:

---
- [__tittle of the contribution__](directory) by:
  * Name Surname, email: email@something.com, github: [GithubAcount](https://github.com/user)
  * Name2 Surname2, email: email2@something.com, github: [otherAcount](https://github.com/user)
---

However, the script works also with another title of section and format of data, it adapts itself. 
See the following, or the examples in the [`contributions/`](contributions) folder.
```(markdown)
# Great Tittle

### section one 

bla bla bla

### Contributor | Author | members |...

email@something.com Name Surname Github: https://github.com/user

Name2 Surname2, email: email2@something.com, github: githubAccount

## section three
bla bla bla
```

The result should look like this:

---
- [__Great Tittle__](directory) by:
  * Name Surname, email: email@something.com, github: https://github.com/user
  * Name2 Surname2, email: email2@something.com, github: githubAccount
---
## Demonstration

You can find as an example, the "[contribution](contributions)" directory of this repository, or the code in my [fork](https://github.com/FelixFonteneau/devops-course) of the DevOps course repository (see actions and pull requests).

In [here](contributions), you have two different categories of contributions, the first is the normal category (demo & demo2).
These directories have direct contributions, whereas presentations that have contributions separated in different weeks.

The result of the action is visible as a [pull request](https://github.com/FelixFonteneau/readme-Generation-for-Devops-Course/pulls) of this repository. 
### Contributor
Any questions?

-> Félix Fonteneau: felixfon@kth.se

