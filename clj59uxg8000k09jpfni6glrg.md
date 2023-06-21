---
title: "Using `git bisect` to figure out when brokenness was introduced"
datePublished: Wed Jun 21 2023 05:26:40 GMT+0000 (Coordinated Universal Time)
cuid: clj59uxg8000k09jpfni6glrg
slug: git-bisect
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687325710902/c87af813-479c-4144-a294-7819e0d3f4cf.png
tags: tutorial, git, debugging, drupal

---

One fine day, I did a fresh installation of [Drupal](https://www.drupal.org/) 8, and came across a bit of ugliness: an ugly grey border on the home page, caused by an empty div being inserted into the page:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687312054906/f8da89e0-c686-421f-bd9b-389d224d19d2.png align="center")

My last fresh install was about a week prior and didn't have this problem. I didn't relish the idea of going through [all of the commits](https://git.drupalcode.org/project/drupal/-/commits) since then one-by-one to figure out where this bug was introduced.

Enter the [git bisect](https://git-scm.com/docs/git-bisect) command!

The `git bisect` command works by performing a ["binary" search](http://en.wikipedia.org/wiki/Binary_search_algorithm) between one state of the code and the other in order to find, by process of elimination, where a given problem was introduced. It's quick, it's easy, and by golly, it *just works*!

Here's how to use `git bisect`, step-by-step!

## **Step 1: Find a commit where things were working.**

Have a look through the git log for a commit from around the time you know things were last working, such as [fd0a623f478e335794e09](https://git.drupalcode.org/project/drupal/-/commit/fd0a623f478e335794e09).

Confirm that this commit actually works ok by switching your checkout to it instead:

(Tip: you only need to reference the first 5-6 characters of the commit hash; you don't need the entire thing... Git is smart and will figure it out!)

```bash
$ git checkout fd0a623f

Note: checking out 'fd0a623f'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

git checkout -b new_branch_name

HEAD is now at fd0a623 - Patch #1201024 by pillarsdotnet: drupal_realpath() should describe when it should be used.
```

Now refresh your Drupal site in your browser. Yay! No more ugly border. So we know that this version of the code, at least, was working okay. Progress!

## **Step 2: Find a commit where things are *not* working.**

Next, we need to know the *current* commit hash, where things are not working so well. That would be [256d85044583970a2d39e](https://git.drupalcode.org/project/drupal/-/commit/256d85044583970a2d39e).

Confirm this by doing:

```bash
$ git checkout 256d85
Previous HEAD position was fd0a623... - Patch #1201024 by pillarsdotnet: drupal_realpath() should describe when it should be used.
HEAD is now at 256d850... Issue #1011614 by catch: Fixed Theme registry can grow too large for MySQL max_allowed_packet() and memcache default slab size.
```

...and refreshing the page again. That ugly border is back again. Ick!

## **Step 3 - N: Use git bisect to find the problem commit.**

Great. So we know where it was working, and we know where it isn't anymore. Time for some fun!

To begin, we need to start `git bisect` and then give it the "known good" place, and the "known bad" place.

```bash
$ git bisect start
$ git bisect good fd0a623
$ git bisect bad 256d850
Bisecting: 28 revisions left to test after this (roughly 5 steps)
[68c0c8c6359961cbef832398c4ddab0fe2f17083] Issue #1238258 by kiamlaluno, izmeez: Change 'Track page visits' to 'Page visits'.
```

Git bisect looked at all of the commits between fd0a623 and 256d850, picked the middle one, and switched the current checkout to that instead.

Now, we need to figure out if the code in commit 68c0c8c has the same issue or not. Reload the page. Hey, the ugly border is gone again!

Tell Git about the good news, and it will start the next search, this time at the halfway point between commit 68c0c8c (*new* known good) and 256d850 (known bad):

```bash
$ git bisect good
Bisecting: 14 revisions left to test after this (roughly 4 steps)
[03b443e8f5043b6e8c3a743ad01a3db9d663ad3c] Issue #1123092 by michaellenahan, varunarora: Fixed user-profile.tpl.php doc has confusing/misleading first paragraph.
```

Refresh the page. Ewww. Border's back again. That's no good. However, we did manage to find a new "known bad" state. Let's tell Git about it so it can give us a new version to try:

```bash
$ git bisect bad
Bisecting: 6 revisions left to test after this (roughly 3 steps)
[e217c4ef1bf06ad75bf6124b9af520195f212001] Issue #1291458 by arithmetric: Fixed Database::getConnection mentions short-lived fixed bug and shouldn't.
```

You know the drill now. Reload. Border gone. Bisect good!

```bash
$ git bisect good
Bisecting: 3 revisions left to test after this (roughly 2 steps)
[08b9bd41723a0a23687c59033c15d66c1840b4f3] Issue #918808 by moshe weitzman, Damien Tournoud, dww: Standardize block cache as a drupal_render() #cache.
```

Reload. Border's back. BAD!

```bash
$ git bisect bad
Bisecting: 0 revisions left to test after this (roughly 1 step)
[9763ca906a6229125dfbe1b56956405457d55892] Issue #1290512 by droplet: Fixed Seven: remove duplicated css.
```

One last time, reload. Border's gone. GOOD!

```bash
$ git bisect good
08b9bd41723a0a23687c59033c15d66c1840b4f3 is the first bad commit
commit 08b9bd41723a0a23687c59033c15d66c1840b4f3
Author: Nathaniel
Date: Thu Sep 29 12:29:59 2011 +0900

Issue #918808 by moshe weitzman, Damien Tournoud, dww: Standardize block cache as a drupal_render() #cache.

:040000 040000 493cba4b1f84c0e907a37f5f4e40d3576bb84785 7763c1bb6f7e4e7b1296863b5df945f5b1760f67 M modules
```

**BAM!** By process of elimination, we've just found our problem [commit](https://git.drupalcode.org/project/drupal/-/commit/08b9bd41723a0a23687c59033c15d66c1840b4f3)! It was from pesky old issue [#918808](http://drupal.org/node/918808). Time to [update the issue](http://drupal.org/node/918808#comment-5065722) with a pointer to the [bug](http://drupal.org/node/1297370) it introduced (and vice-versa).

## **Step 4: Get back to a working state.**

Once you're all finished up, run these commands to end your `git bisect` session and get back to the normal branch:

```bash
$ git bisect reset
Previous HEAD position was 9763ca9... Issue #1290512 by droplet: Fixed Seven: remove duplicated css.
HEAD is now at 256d850... Issue #1011614 by catch: Fixed Theme registry can grow too large for MySQL max_allowed_packet() and memcache default slab size.

$ git checkout 8.0.x

Switched to branch '8.0.x'
```

Now you're back in business!

## **Awww, yeah!**

We've successfully deduced where a problem was introduced in about 3 minutes. Sifting through commit logs and trying to revert patches on an ad-hoc basis can take 10 times that or more. Let's say it together now, **Git bisect rules**!! :D