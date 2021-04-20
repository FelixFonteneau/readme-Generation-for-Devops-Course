# ReadMe Summary Generation on Category Directories
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

### About
This repository contains code to automatise the generation of readmes for the different contribution in the
repo of the [DevOps course](https://github.com/KTH/devops-course/) of KTH. 
This code is specific to the structure of the specified repository, but it can easily be adapted to other form of repository.


## Overview

In this repo, you find a GitHub action on pushes that execute a script to generate the readme of the different type of contributions.
This generates a list of information forming a summary of every contribution in the category. 
The action will generate a Pull Request with all the list updated without modifying specific rules or previous instruction in the category readme.

## How It Works
In order to do update the readmes automatically,
- The GitHub action trigger on specific modification in the contributions' directory.
- A Python script analyse each directory and try to retrieve important information in the readme:
    * Tittle of the contribution
    * Name of the contributors
    * Email of the contributors
    * GitHub of the contributors
- The script displays the date in format of list with link to the different contributions and update the category readme.
- In the same time, the script print which contribution does not contain a proper README.md.
- The GitHub action get the updates and create an automatic Pull-Request.

## Format accepted
To allow a good execution of the script, each category folder should be place in the `contributions` folder. 
The contributions should be in the format of kebab case to separate the contributors `contributorone-contributortwo`.

Inside a contribution folder, the script will try to look for a tittle with minimal `#`.
Then, it will try to find a members section of the format:
```(markdown)
# tittle of the contribution

## Member(s)

Name Surname (email@something.com) [GithubAcount](https://github.com/user)
Name2 Surname2 (email2@something.com) [otherAcount](https://github.com/user)
```

The result should look like ti: 

---
- [__tittle of the contribution__](directory) by:
  * Name Surname, email: email@something.com, github: [GithubAcount](https://github.com/user)
  * Name2 Surname2, email: email2@something.com, github: [otherAcount](https://github.com/user)
---

However, the script works also with other tittle of section and format of data, it adapts itself.
```(markdown)
# Great Tittle

## section one 

bla bla bla

## Contributor | Author | members |...

email@something.com Name Surname Github: https://github.com/user

Name2 Surname2, email: email2@something.com, github: githubAccount

## section three
bla bla bla
```

The result should look like to:

---
- [__Great Tittle__](directory) by:
  * Name Surname, email: email@something.com, github: https://github.com/user
  * Name2 Surname2, email: email2@something.com, github: githubAccount
---
## Demonstration

You can find as example, the "[contribution](contributions)" directory of this repository, or the code in my [fork](https://github.com/FelixFonteneau/devops-course) of the DevOps course repository (see actions and pull requests).

In [here](contributions), you have two different category of contribution, the first is the normal category (demo & demo2). 
These directories have direct contributions, whereas presentation that have contribution separated in different weeks.

### Contributor

Félix Fonteneau: felixfon@kth.se

