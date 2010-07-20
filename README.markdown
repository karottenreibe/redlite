# redlite #

*redlite* is a simple update scanner that scans any website on command
and keeps an HTML diff of the changes, which can be displayed in any browser.


## Dependencies ##

*   [HTML Diff][diff] by Aaron Swartz (included in the repository)
*   [wget][]


## Workflow ##

1.  The URIs to scan need to be specified in `$XDG_CONFIG_HOME/redlite/urls`.
    The config file's syntax is straight forward: one URI per line.

    After the URI, any additional wget parameters may be specified, e.g. `--username`,
    as well as any pipes, e.g. to sed. Here are a few examples:

        # simple URI
        http://www.google.de
        # stripping a footer with sed
        http://www.somesite.com/index.html.de | sed '/id="footer"/,$d'
        # username and password for HTTP auth
        http://www.foo.bar.om/strange/ --user dilbert --password arrrgh

    As you can see, comments are lines starting with a hash tag and are ignored.

2.  Now, `redlite -s` will scan all of those URIs and generate the diffs if changes
    occurred. Note that on the first scan, no diff is generated.
    If you want output, use `redlite -s -v`.

3.  A call to `redlite -q` will list all the stored diff files on stdout.

    Alternatively, you can call `redlite -o` to directly open all the diffs in your
    browser. Note that `$BROWSER` has to be set for this to work.

    ([awesome][] for example does not currently propagate that variable)

4.  A call to `redlite -c` will discard all current diffs and mark all sites
    as having no changes.


[diff]: http://www.aaronsw.com/2002/diff "HTML Diff"
[wget]: http://www.gnu.org/software/wget/ "wget utility"
[awesome]: http://awesome.naquadah.org/ "awesome window manager"

