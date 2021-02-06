# How to improve Haskell documentation

## The Haskell Wiki

### Discovering out-of-date information

The [list of orphaned
pages](https://wiki.haskell.org/Special:LonelyPages) ("not linked from
or transcluded into other pages in HaskellWiki") contains a good set
of candidates for out-of-date pages.  The [Random
Page](https://wiki.haskell.org/Special:Random) feature throws up
surprisingly many out-of-date pages.

### Dealing with out-of-date information

If you come across out-of-date information on the [Haskell
Wiki](https://wiki.haskell.org/) then consider taking one of the
following actions.

* Update the information

  If you know how to bring the outdated information up-to-date then
  please do so by updating the contents of the page.

* Mark the page as outdated

  The simplest thing to do with outdated information on the Wiki is to
  prominently mark it as such.

### How to perform tasks on the Haskell Wiki

* Obtain an account

  The [login page](https://wiki.haskell.org/Special:UserLogin)
  explains how to obtain an account that can log in to the Haskell
  Wiki.  In case you need to prod an admin to create the account, note
  that there is a Wiki page listing [the users with the ability to
  create an
  account](https://wiki.haskell.org/index.php?title=Special:ListUsers&group=createaccount).

* Edit a page

  Follow the "Edit" link that appears on the page (probably near the
  top).

* Update the contents of a page

  Edit the page, change the page's contents in the text box, set the
  "Summary" to an explanation of the changes you have made, and click
  "Save page".

* Discover how long it has been since a page was edited

  Follow the "View history" link that appears on the page (probably
  near the top).

* Mark a page as outdated, with a link to a better source of
  information

  Edit the page and add this snippet at the top. Replace XXXX with the
  year of last update and replace the external link and text with a
  useful reference.  Retain or omit `''extremely''` as you feel
  appropriate.

  Set the "Summary" to "Marked page as outdated" then click "Save
  page".

  ```html
  <span style="color: red">[WARNING: This page is ''extremely'' outdated
  and hasn't been updated since XXXX.  You should look at
  [https://external/link/ External Link Text]
  instead.]</span>
  ```

* Mark a page as outdated, without a link to a better source of
  information

  Edit the page and add this snippet at the top. Replace XXXX with the
  year of last update.  Retain or omit `''extremely''` as you feel
  appropriate.

  ```html
  <span style="color: red">[WARNING: This page is ''extremely'' outdated
  and hasn't been updated since XXXX.]</span>
  ```

  Set the "Summary" to "Marked page as outdated" then click "Save
  page".
