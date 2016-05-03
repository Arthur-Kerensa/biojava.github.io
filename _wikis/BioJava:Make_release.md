---
title: BioJava:Make release
---

How to make a BioJava release
-----------------------------

This page is intended for BioJava release managers. I was documenting
this while I was doing the BioJava 1.7
release. --[Andreas](User:Andreas "wikilink") 15:14, 12 April 2009 (UTC)

### Required time

A few hours. Most time is being spent in verifying that the code base is
release ready. The actual preparation of the .jar files and copying them
to the open-bio.org server is quite quick and can be done
semi-automatic.

### Prior to release

-   Announce release deadlines on mailing list
-   Run optimize imports across whole project
-   Make sure all java classes have the copyright statement by running
    this shell script: <BioJava:EnsureCopyrightHeader>

### Configure Authentication Keys

You need to configure the following 3 items for performing a full
release 
 1. OSS Sonatype login (OSS Jira account login) 
 2. PGP signature for code signing (only can upload signed jars to OSS Sonatype) 
 3. Write permission to `github.com/biojava/biojava.github.io`

#### OSS Sonatype login

As of release 4.0.0 we moved our repository hosting from biojava's web
server to Maven Central. To push releases there, you need to first get
an account set up at the [OSS Sonatype
Jira](https://issues.sonatype.org). One of the people who already have
permission (currently @andreasprlic and @heuermh) can request to add you
to the already existing biojava project. The BioJava pom.xml is set up
correctly to upload the jars for you, as long as you set up your login:

You need to configure maven with your username and identity file. In
~/.m2/settings.xml (on the build machine), add or merge the following
xml:

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
     http://maven.apache.org/xsd/settings-1.0.0.xsd">  
      <localRepository/>  
      <interactiveMode/>  
      <usePluginRegistry/>  
      <offline/>  
      <pluginGroups/>  
      <mirrors/>  
      <proxies/>  
      <profiles/>  
      <activeProfiles/>  
      <servers>  
         <server>  
              <id>ossrh</id>  
              <username>username</username>  
              <password>pwd</password>  
         </server>  
      </servers>  
</settings>
```

Maven reports 'Auth Error' in the release:perform stage if you keys are
not properly set up. Permissions errors mean that authentication was
successful but you can not write to the correct location (for instance,
if a maven-metadata.xml exists from a previous build by another user).

More information about using the Maven release plugin to push to OSS
Sonatype is
[here](http://blog.sonatype.com/2013/09/simplified-releases-to-the-central-repository-with-nexus/).

#### BioJava web server project write access

Make sure you can write to `https://github.com/biojava/biojava.github.io`

#### PGP Signature

Set up a PGP signature for code signing. For documentation how to do
this see [here](https://www.gnupg.org/gph/en/manual/c14.html).

On release date
---------------

**Verify code base**

-   Make sure code is ready for release. Check last minute commits
    (there usually are some).
-   Make sure the auto-build page (cruisecontrol) does not report any
    problems

Clean checkout
--------------

Create a clean clone on a machine with ssh keys set up to access
cloudportal.open-bio.org (and associated maven settings; see above).

`git clone git@github.com:biojava/biojava.git bj3.0.7`

### Make maven release

the release process is very straightforward nowadays. It is rather
time-consuming, as maven runs all tests during each step.

`mvn release:clean `  
`mvn release:prepare `  
`mvn release:perform`

The second and third steps set up your local git repository and deploy
jar files for each module to cloudportal. If something goes wrong, you
can technically run \`mvn release:rollback\`, but it is easier to just
reset your git repository to master.

`git reset --hard origin/master`

AP: I recommend NOT to do git reset, once files have been uploaded to
sonatype. release:rollback will clean up for you.

### Push to Github

If all three steps work fine, the maven release plugin will push on your
behalf to Github and release the jars on OSS Sonatype. Note:
```mvn:release``` takes about 1 hour since the bandwith to upload at OSS
Sonatype is limited.

If there is a problem, here how to add the release tag by hand:

push the tag to github and merge it to releases. Note that I'm assuming
origin refers to the central biojava repository.

<span style="color:red">Note: double check these commands</span>

```
git pull master #merge any commits that occurred while releasing
git push --tags origin master #push the new master (with updated pom) and new tags

git checkout release  
git merge biojava-3.0.7
git diff biojava-3.0.7 release #shouldn't print anything
git push origin release
```

And here how to delete a release tag again:

```
git tag -d biojava-3.0.7
git push origin :refs/tags/biojava-3.0.7
```

### Prepare and release javadoc files

(Still in git checkout, e.g. bj3.0.7 if you're following along or
biojava/target/checkout/ if you did not mvn clean in the meanwhile)

build javadoc:

`mvn site`

Here we assume the version nr. of the current release is 3.0.7.

` cd target/site/`  
` mv apidocs/ api3.0.7`  
` tar czvf api3.0.3.tar.gz api3.0.7/`  
` scp api3.0.7.tar.gz username@cloudportal.open-bio.org:/home/websites/biojava.org/html/static/docs/`

now log into the couldportal server:

`ssh andreas@cloudportal.open-bio.org`  
  
`cd /home/websites/biojava.org/html/static/docs/`  
`tar zxvf api3.0.7.tar.gz`  
`rm api`  
`ln -s api3.0.7 api`

and back to your local machine...

### Create the biojava-all bundle

If needed, rename your git checkout to bj3.0.7

`mv checkout/ bj3.0.7`

remove .git files

`rm -rf .git .gitignore .travis.yml KEYS ignore.txt`

Create -all tarball

`cd ..`  
`tar czvf bj3.0.7-all.tar.gz bj3.0.7`  

on portal.open-bio

`mkdir /home/websites/biojava.org/html/static/download/bj3.0.7`

back to your local machine

`scp biojava-3.0.7-all.tar.gz andreas@cloudportal.open-bio.org:/home/websites/biojava.org/html/static/download/bj3.0.7`

### Javadocs

this is how to enable analytics in javadocs

`cd biojava-svn/target/bj3.0.7/`

`mvn clean install source:jar javadoc:jar javadoc:aggregate`

`cd biojava-svn/target/bj3.0.7/target/site/apidocs`

upload apidocs

### Update the wiki pages to link to the new release

Create a new download file for the release. (I copied
`BioJava:Download_3.0.4` to `BioJava:Download_3.0.5`). Modify the new
page to the latest data.

Update <BioJava:Download> (Change the redirect on the BioJava:Download
page to <BioJava:Download_3.0.5>)

Update [Template:Current version](Template:Current version "wikilink"),
which should change all the references on the home page, sidebar, etc.

Double check that there are no additional references to the old version
using an
[<http://biojava.org/w/index.php?title=Special%3ASearch&profile=advanced&fulltext=Search&ns0=1&ns4=1&redirs=1&search>=
Advanced Search].

### AND FINALLY

Write release announcement to biojava-l and biojava-dev
