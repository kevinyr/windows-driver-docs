# Contributing to Windows Driver Documentation

Thank you for your interest in the Windows driver documentation! 
See below for details on how you can contribute to our technical documentation.

## Sign a CLA

If you are not a Microsoft employee, you must [sign a Microsoft Contribution Licensing Agreement (CLA)](https://cla.microsoft.com/) before you can contribute to any Microsoft repositories. 
If you've already contributed to Microsoft repositories in the past, congratulations! 
You've already completed this step.

## Public and private repos

The driver docs are hosted on two different sites.

If you are not a Microsoft employee, work in the [public content repository](https://github.com/Microsoft/windows-driver-docs).

If you are a Microsoft employee, work in the [private content repository](https://cpubwin.visualstudio.com/drivers/_git/drivers).  

## Providing feedback on Windows driver documentation

You can point out errors, suggest changes, or request new topics by creating an issue in the issues page of the appropriate repository.

Issues are reviewed regularly by members of the Windows driver documentation team, and are triaged, assigned, and addressed accordingly.

All of the documentation hosted in this repo is written using [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/).

## Editing topics

To edit an existing file, simply navigate to it and click the "Edit" button. 
If you're using the GitHub-based public repo, GitHub will automatically create your own fork of our repository where you can make your changes. 
If you're using the VSO-based private repo, use the drop-down arrow next to the Commit button and select **Commit to new branch**.
Once you're finished, submit a pull request to the *master* branch of the repository. 
After your pull request is created, someone on the Windows driver documentation team reviews your changes.

If your request is accepted, updates are published to https://msdn.microsoft.com/windows/hardware/drivers.

## Making more substantial changes

To make substantial changes to an existing article, add or change images, or contribute a new article, you will need to create a local clone of the content.

If you are using the public repo, you'll manually create your GitHub fork and then clone the fork down to your local computer.  Work locally, then push your changes back into your fork.  Then open a pull request back into the public repo.

If you are using the private repo, you'll clone the private repo to your local computer.  Create a new branch from master, make your changes, and then push your new branch back into the VSO private repo.  Then open a pull request back to the master branch.
