---
title: "Updating an important but stale Python library"
date: "2020-07-01"
tags: ["python", "machine learning", "datascience", "opensource"]
author: Menelaos Kotoglou
# author: ["Me", "You"] # multiple authors
ShowReadingTime: true
showToc: false
TocOpen: false
draft: false
hidemeta: false
disableShare: false
cover:
    image: "<image path/url>"
    alt: "<alt text>"
    caption: "<text>"
    relative: false
comments: true
---

The project is based on a “profanity-check” library created by Victor Zhou. You can read more about it here and find it online here: https://github.com/vzhou842/profanity-check. Firstly, we installed the library in a virtual environment and experimented with different samples.

We tested the model with an internal dataset consisting of 850 tweets retrieved through Twitter’s sampling API then labeled manually. This produced the following results:

Confusion Matrix

| Actual<br> Predicted | Not Profane (0) | Profane (1) |
|------------------|---------------|-----------|
| Not Profane (0)    |           703 | 14        |
| Profane (1)        | 93            | 39        |

Accuracy Score: **87.4%**

The issue that came up is that with newer Python and scikit-learn versions a list of warnings was thrown when including the library. Library’s dependencies were gradually deprecated and we had to update them making them compatible with newer versions of Python and scikit-learn. This is important because at any given point in time new releases of these libraries might not be able to deserialize the joblib’ed (alternative to pickle) file stored with the library.

As the library’s documentation states https://scikit-learn.org/stable/modules/model_persistence.html :

“… pickle (and joblib by extension), has some issues regarding maintainability and security. Because of this,

Never unpickle untrusted data as it could lead to malicious code being executed upon loading.
While models saved using one version of scikit-learn might load in other versions, this is entirely unsupported and inadvisable. It should also be kept in mind that operations performed on such data could give different and unexpected results.”

This was not happening in this case as the original author had provided the input dataset and the serialised model files, but not the script to create them from these data. For this, I installed Python3.8 and scikit-learn 0.23.1. After lots of experiments, I substituted CountVectorizer from Victor Zhou’s blog post with TfidfVectorizer, trained the model based on the “clean_data.csv” from which the initial version was trained with and got roughly the same accuracy score as the previous model had. In detail:

Confusion Matrix

| Actual<br> Predicted | Not Profane (0) | Profane (1) |
|------------------|---------------|-----------|
| Not Profane (0)    |           697 | 20        |
| Profane (1)        | 87            | 45        |

Accuracy Score: **87.4%**

Working on this project helped me to:
- Enhance my Python and scikit-learn knowledge.
- Work with pandas, NumPy, and Joblib libraries.
- Get familiar with open source development workflows.
- Use git working alongside with another collaborator to solve a problem.

The biggest surprise was a versioning issue that came up. Specifically, I had to find a way to update the model in a version compatible with Python3.8 since the current model’s scikit-learn version was not compatible with that version. Fortunately scikit-learn 0.23.1 works with Python3.8 hence chose this version.

Overall, It’s been a great experience. I was able to use my academic knowledge to solve a real world problem. Also I was lucky to be supervised and mentored by Dimitrios, [yourself.online](https://www.yourself.online)’s current CTO: was confident to speak and discuss every question that came up, even the dumbest ones. During every project’s step constant and immediate feedback was provided.

My model is currently used in production as committed in the fork here: https://github.com/dimitrismistriotis/profanity-check. Changes have also been submitted to the original library: https://github.com/vzhou842/profanity-check/pull/19. As stated the model is used as part of the content classification checks that happen within [yourself.online](https://www.yourself.online)’s service which is available here: https://www.yourself.online.