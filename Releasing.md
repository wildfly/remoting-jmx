# Releasing Remoting JMX

To release Remoting JMX first checkout the project and ensure you are on the latest commit for the 3.2.x branch with no local changes.

Prior to releasing you should ensure you have your own GPG signing key set up, published to a key server and listed on [wildfly.org](https://www.wildfly.org/contributors/pgp/).

## Prepare the release

Execute:

    mvn release:prepare -Pjboss-release

Enter the version being released:

    What is the release version for "Remoting JMX"? (remoting-jmx) 3.2.0.CR1: 3.2.0.Alpha1

The tag will default to the version:

    What is the SCM release tag or label for "Remoting JMX"? (remoting-jmx) 3.2.0.Alpha1:

Set the next version:

    What is the new development version for "Remoting JMX"? (remoting-jmx) 3.2.1.Alpha1-SNAPSHOT: 3.2.0.CR1-SNAPSHOT

The release commit can be checked with:

    git show ${TAG}

If everything is Ok perform the release which will deploy to Nexus.

## Perform the release

Execute:

    mvn release:perform -Pjboss-release

This will deploy the release to the `wildfly-staging` repository.

Wait for 10 minutes then visit the Validation task for the `wildfly-staging` repository in Nexus. If this task ran at least 10 minutes after the release was deployed check the latest results on the Settings tab and verify that at least one component was processed and that there were no errors. If the task has not run it can be manually kicked off using the Run button.

e.g.

> Processed 1 components.
> - no errors were found.
> - the deployment was a dry run (no actual publishing).

If others are also deploying at the same time this count could be higher, the important check is that the scan was at least 10 minutes after it was deployed, 1 or more components were scanned and no errors specific to Remoting JMX are reported.

## Complete the release

If no issues are reported complete the release.

Move the component to the releases repository:

    git checkout ${TAG}
    mvn nxrm3:staging-move
    git checkout 3.2.x

Push the branch and tag to GitHub:

    git push upstream 3.2.x
    git push upstream ${TAG}

## Rollback the Release

If the release failed, revert the release.

Delete the component from Nexus:

    git checkout ${TAG}
    mvn nxrm3:staging-delete
    git checkout 3.2.x

Reset your local Git checkout:

    git reset --hard upstream/3.2.x
    git tag --delete ${TAG}