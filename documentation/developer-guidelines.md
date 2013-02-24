OpenShift Developer Guidelines
==============================

[Summary](#summary)

[Communication](#communication)

* [Google+](#google)
* [IRC](#irc)
* [Mailing list](#mailingList)
* [Twitter](#twitter)

[Commits in git](#commitsGit)

* [Squash commits](#squashCommits)
* [Enhancements and updates](#enhancementsUpdates)
* [Bug fixes](#bugFixes)

[Various expectations](#variousExpectations)

* [Fail gracefully](#failGracefully)
* [Secrets in quickstarts](#secretsQuickstarts)
* [Storing sensitive data from gears in MongoDB](#storingSensitiveMongoDB)
* [Provide machine-readable script outputs](#machineReadableOutputs)
* [Hardcoding assumptions from the Online project](#hardcodingAssumptions)

<h1 id="summary"> Summary </h1>

For any project with more than a handful of contributors, it is helpful to
agree on some guidelines for participation. This document walks through
various expectations that have developed for the OpenShift project. Some
may be reactions to mistakes that we are still working to correct, so
we request patience with past transgressions. With awareness that any
open source project guidelines must sometimes bend to allow specific
circumstances, we hope these will be useful guidelines for making this
project successful.

<h1 id="communication"> Communication </h1>

<h3 id="google"> Google+ </h3>

The OpenShift Origin community central coordination point is our
[Google+ community](https://plus.google.com/communities/114361859072744017486). Join for news and Q/A.

<h3 id="irc"> IRC </h3>

OpenShift developers discuss the project in realtime on [#openshift-dev on freenode](http://webchat.freenode.net/?randomnick=1&channels=openshift-dev&uio=d4).

<h3 id="mailingList"> Mailing list </h3>

The OpenShift developer mailing list is <dev@lists.openshift.redhat.com> - you may join freely at
<https://lists.openshift.redhat.com/openshiftmm/listinfo/dev>.

<h3 id="twitter"> Twitter </h3>

Follow [@openshift](https://twitter.com/openshift) on Twitter.

<h1 id="commitsGit"> Commits in git </h1>

<h3 id="squashCommits"> Squash commits </h3>

DO:

* Use `git rebase -i` to combine multiple interim commits into single
coherent commits with helpful commit logs before submitting a pull
request. This keeps our commit logs readable.

AVOID:

* Pull requests with lots of small commits for tweaks and interim
saves. This is just noise in the log.
* Squashing commits from unrelated changes into one large commit -
this obscures the purpose and makes rollback of individual changes harder.

<h3 id="enhancementsUpdates"> Enhancements and updates </h3>

DO:

* `git commit` without `-m` for multiline messages.
* Format log messages like this:

    \<script, class, or component\> short description of the work done
    
    (Line 2) Link to Trello card, PEP, or other planning documentation
    
    (Remainder) Detailed explanation as needed

AVOID:

* Minimalist commit messages like this:

    Changed foo to bar (where, why?)

    \<broker\> updated some things

These make later viewers work harder to figure out what it is.


<h3 id="bugFixes"> Bug fixes </h3>

DO:

* `git commit` without `-m` for multiline messages.
* Format a commit message like this:

    Bug `number` - short description of the fix, symptom, or bug
    
    (Line 2) Bugzilla link <https://bugzilla.redhat.com/show_bug.cgi?id=number>
    
    (Remainder) Detailed explanation as needed

Some benefits from this:

1. By doing "bug `number`" ("bug" or "Bug" but not "BZ" or "Bugzilla")
our GitHub detector will **automatically** put a message into the bug
record once your commit hits master (which means test will know that
your code is really in master).
2. Adding the short description helps folks scan the commit log more
easily. Including the BZ link (which you probably have handy) makes it
that much easier to get to it later (when you probably do not).

AVOID:

* Minimalist commit messages like this:

    Bug `number`

    Fixed a bug

These make later viewers work harder to figure out what it is.

<h1 id="variousExpectations"> Various expectations </h1>

<h3 id="failGracefully"> Fail gracefully </h3>

DO:

* Expect and check for failure conditions and raise or wrap as appropriate.
* Set a timeout (preferably configurable) on any operation that could block forever.

<h3 id="secretsQuickstarts"> Secrets in quickstarts </h3>

DO:

* Salt or otherwise scramble secrets embedded in
quickstarts such that they are unique per application,
not universally shared. An obvious example would be [Rails
secret_token.rb](http://www.phenoelit.org/blog/archives/2012/12/21/let_me_github_that_for_you/index.html)

<h3 id="storingSensitiveMongoDB"> Storing sensitive data from gears in MongoDB </h3>

AVOID:

* Your cartridge storing any environment variables in MongoDB that might be considered sensitive. Keys and passwords are obvious candidates. DB contents are too likely to be displayed indiscreetly.

<h3 id="machineReadableOutputs"> Provide machine-readable script outputs </h3>

DO:

* With any script, provide at least an option for machine-readable output (well-defined e.g. YAML, JSON, XML, a DSL, etc.). The default may be intended for human consumption but options should enable other scripts based on your script.

<h3 id="hardcodingAssumptions"> Hardcoding assumptions from the Online project </h3>

AVOID:

* Coding constants in origin-server for specific gear profiles,
cartridges, external integration points, or anything else we might
reasonably expect an OpenShift administrator to want to customize.

DO:

* Use configuration files, cartridge manifests, and plugins to enable specific behavior.

