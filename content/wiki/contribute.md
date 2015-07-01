## Contribute to get_iplayer

### Code

If you would like to contribute to get_iplayer development, fork the repository on GitHub and submit a pull request with your changes (GitHub account required). See GitHub help documentation for basic information on [forking a repo](https://help.github.com/articles/fork-a-repo/) and [creating a pull request](https://help.github.com/articles/creating-a-pull-request/). The get_iplayer project repo is:

<https://github.com/get-iplayer/get_iplayer>

Follow a few basic guidelines for pull requests:

- Each pull request should be submitted from its own feature branch in your fork of the repository.  This will make it easier to manage further changes after the pull request is submitted. 

- You should base your feature branch on the **develop** branch in the get_iplayer repo, so create it similar to:

        git checkout -b feature/goodstuff develop

- Each pull request should contain only one new feature or a fix for a single bug.

- Each pull request should contain only one commit unless there are exceptional reasons to do otherwise.

- Each pull request should be independent of changes made in any other pull request.

- get_iplayer uses tabs for indentation - **not** spaces - and so must the changes in your pull request.

- Run `git diff --check` on your code before committing to ensure you don't have whitespace errors.  If you do, fix them before submitting your pull request.

GitHub pull requests are strongly preferred.  However, you may also submit patches to the [get_iplayer mailing list](http://lists.infradead.org/mailman/listinfo/get_iplayer) so long as they conform to the above guidelines.  Patches sent to the mailing list will only be reviewed if you explicitly state that you are submitting code for inclusion in get_iplayer.  Make sure your patches apply cleanly to the current **develop** branch in the get_iplayer repo, otherwise they may be rejected - don't expect committers to fix your code.  If you create patch files, use `git format-patch` to ensure your patches are in the correct format.  Use `git send-email` to mail your patches in order to ensure your patches are not mangled by your email software. Sending the patch to yourself first, then checking that you can save it to a file and apply it, is a useful technique.  

### Documentation

If you would like to contribute new documentation or make changes in existing documentation, you can edit the project wiki  (GitHub account required). The get_iplayer project wiki is:

<https://github.com/get-iplayer/get_iplayer/wiki>

Markdown content is preferred.
