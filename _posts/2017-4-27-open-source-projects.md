---
layout: post
title:  "A Successful Open Source Project"
tags: hpc software
---

# A Successful Open Source Project

Its all too common for people and companies today to put some portion of their software (aka code) on GitHub and subsequently claim they are using open source practices. Perhaps this is due to the term "open source" being used as a buzz word that get management excited. Releasing code like this is a step in the right direction, but to truly reap the benefits of open source more effort is required.

When creating or selecting an open source project/library/tool there are a few certain things I always look for. Here's my list of things that every open source project should have.

## 1. A User Guide
It can be as simple as a README.md, or more complex. There are several great tools for creating a user guide. GitHub Wiki's and Read The Docs are two great examples. (Even if you use these more advanced tools, you should be documenting their use in the README.md, so others can know where to go.)  You user guide should contain at least a few things:
1. An Overview
2. Installation instructions
3. Contributing instructions (This can be as simple as, "pull-requests accepted!")

## 2. Releases
This is one of the easiest ways to know if this is a serious open source project or not. If you only have one release, from 1+ year(s) ago, then I know I'll never get the authors to maintain anything. Multiple steady releases are a sign of continued development and developers who care. I always look at this number and even view the latest release to see when kind of release notes I can expect in the future. Mature projects tag, and release regularly.

## 3. CI badges
These badges give users confidence that future releases and fixes wont be broken. Things like documentation badges, CI badges, and code coverage badges are all fantastic ways to show off the hard work of developers. Here are a few badges I recommend:

![github badges](/img/github-badges.png)

A great list of badges can be found at: [http://shields.io/](http://shields.io/)

## 4. A Package manager
Python has [PIP](https://pypi.python.org/pypi), node.js has [NPM](https://www.npmjs.com/), and C# has [nuget](https://www.nuget.org/). Users know using a package manager will make their life a lot easier. Developers should strive to support at least one, more if applicable. This will simplify installation instructions and increase project visibility. (Google will find a few pages referencing your project.)

# Conclusion

Maintaining a nice looking repo will get your code more views and put you on a path with devoted community members.

# References

[The US goverment mandates that 20% of its code must be open source](https://sourcecode.cio.gov/).
