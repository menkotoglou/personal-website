---
title: "Republishing and maintaining Profanity-check"
date: "2021-01-31"
tags:
  ["python", "machine-learning", "data-science", "teamworking", "maintenance"]
author: Menelaos Kotoglou
# author: ["Me", "You"] # multiple authors
ShowReadingTime: true
showToc: false
TocOpen: false
draft: false
hidemeta: false
disableShare: false
cover:
  image: "/images/whooshkaa-podcast-image.jpg"
  alt: "photo"
  caption: ""
  relative: false
comments: true
---

As previously posted here:
<https://dev.to/koti/updating-an-important-but-stale-python-library-3o6i>, me
and Dimitry cooperated on updating a Python library important for the smooth
operations of his company.

Unfortunately, it seems that its original author never accepted our previous
Pull Request to revive the profanity-check package. As a result, Github issues
were kept being opened by other developers asking about the library and issues
they had while using it. What surprised us the most, was this one:
<https://github.com/vzhou842/profanity-check/issues/28>, where someone actually
recommended our fork of the project as a "_new version available here, that
solves the issue very well_".

Considering this and seeing that package seemed to have many users, either in
production or for personal use, we decided that re-publishing the same library
would be a great idea to bring the package back to life and make it accessible
for more developers to experiment with. The main problem was following up with
scikit-learn package's updates which rendered the initial models problematic as
the next versions were released.

After taking this quick and handy tutorial from Real Python:
<https://realpython.com/courses/how-to-publish-your-own-python-package-pypi/>,
we made some minor modifications to the project's repository and uploaded our
updated version to PyPi.

Outcome turned out to be really beneficial during the process and made us better
both as people and developers. For example, we found out that when uploading a
PyPI package, you don't really sync your repository to the PyPI project page.
You only upload a tar'ed "/dist" directory's content produced after running the
`python setup.py bdist_wheel` command.

We also realised that many developers can sometimes be demanding things out of
nowhere. They may request features and bug fixes, unable to understand that
open-source software main purpose is the community's contribution in every
possible way. They should consider putting some work on the projects themselves
or contributing in other ways or at least saying "thanks".

At any case, taking on the "responsibility" of maintaining a Python package,
widely used by the community seems to be an exciting journey on the open-source
software adventure. It makes you feel proud and responsible for ensuring that
other people's projects continue to operate smoothly.

You can find the package and instructions for its installation here:
<https://pypi.org/project/alt-profanity-check/>. Also, the source code can be
found here: <https://gitlab.com/dimitrios/alt-profanity-check>. Contributions
and new feature ideas are more than welcome.
