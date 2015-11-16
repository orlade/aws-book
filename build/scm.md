# Source Code Management (SCM)

Source code is an extremely precise medium. In typical English language text, errors in spelling and grammar may be overlooked. In code, a single incorrect character -- sometimes even *whitespace* -- can potentially break an entire application... or worse. Simple software bugs can destroy user data, customer trust, business value and even human lives.

Are you scared yet? Because the problem is magnified when multiple software developers must work together. The structure and intent of code is quite complex and idiosyncratic. When merging code from two different people, it is terribly easy to introduce bugs.

A **version control system** (VCS) keeps track of every single change to every line of code by every developer over the life of a project. It provides invaluable support for process that protect against these emergent bugs. It also allows us to go back in time to examine when and where bugs were introduced.


## Git

[​Git​][git] is a "distributed" VCS (or DVCS), a (not so) new generation of VCS. Instead of maintaining a single central VCS database on a server, every developer keeps a complete local copy of the history. Changes are made and "committed" locally, then "pushed" to a remote copy. There is still an "official" copy on a server (called `origin`) with which multiple developers can synchronise, but local development is not bound to it.

Git is far and away the leading VCS in use today. Every software project should use it. Even non-software projects can often benefit from it (for example, this book [developed on GitHub][hub] and [published by Gitbook][book]).

[GitHub][github] and [Bitbucket][bitbucket] are the leading providers of hosted `origin` repositories. Both provide free hosting for public repositories, and have commercial plans for private repositories. GitHub charges per repository, and Bitbucket charges per collaborating user. GitHub has a more vibrant community for open-source projects, but Bitbucket private repositories are free for up to five users.

Most importantly, both GitHub and Bitbucket are well-integrated with other Web services. This simplifies the process of automating the build system. We'll explore this automation in more detail in [continuous integration](ci.md).


## What should I do?

1.  Sign up for a Git repository hosting account. It's up to you, but as a rule of thumb I store private repositories on Bitbucket and open-source projects on GitHub.

   Assuming your project is private, I'll assume you sign up for Bitbucket.
1. Create a private Bitbucket repository.
1. Clone the empty repository to your local machine, or if you've already started, initialise your local working copy with Bitbucket as the `origin` remote.
1. Commit and push some content in a `README.md` file, and ensure [it appears on Bitbucket's repository overview page][readme].


## See Also

For the academic interest of comparison, there are some alternatives to Git:

* [Subversion][svn]: the old gold standard of the centralised VCS era. In common use on old [SourceForge][sf] projects.
* [Mercurial][hg]: Similar to Git. There are some [pros][hg-pros] and [cons][hg-cons].
* [Bazaar][bazaar]: Also similar to Git. More focus on [ease of use][bazaar-pros], suppored by [Launchpad][launchpad].


[git]: https://git-scm.com/
[hub]: https://github.com/orlade/aws-book
[book]: https://orlade.gitbooks.io/aws/content/index.html
[github]: https://github.com
[bitbucket]: https://bitbucket.org/
[readme]: https://confluence.atlassian.com/bitbucket/display-readme-text-on-the-overview-221449772.html
[svn]:https://subversion.apache.org/
[sf]: http://sourceforge.net/
[hg]: https://www.mercurial-scm.org/
[hg-pros]: https://blogs.atlassian.com/2012/02/mercurial-vs-git-why-mercurial/
[hg-cons]: https://blogs.atlassian.com/2012/03/git-vs-mercurial-why-git/
[bazaar]: http://bazaar.canonical.com/en/
[bazaar-pros]: http://doc.bazaar.canonical.com/migration/en/why-switch-to-bazaar.html
[launchpad]: https://launchpad.net/
