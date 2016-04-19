# FAQ

*   *Where can I get help?*

    Mail us at [admin@software-carpentry.org](mailto:admin@software-carpentry.org),
    or join our [discussion list](http://lists.software-carpentry.org/mailman/listinfo/discuss_lists.software-carpentry.org)
    and ask for help there.

*   *Where can I report problems or suggest improvements?*

    Please file an issue against [https://github.com/swcarpentry/workshop-template](this repository)
    or [mail us](mailto:admin@software-carpentry.org).

*   *Why does the workshop repository have to be created using `import.github.com`? Why not fork `workshop-template` on GitHub?*

    Because any particular user can only have one fork of a repository,
    but instructors frequently need to work on several workshops at once.

*   *Why use the `gh-pages` branch instead of `master`?

    Because [GitHub automatically publishes `gh-pages`](https://help.github.com/articles/creating-project-pages-manually/)
    as a website.

*   *Why use Jekyll?  Why not some other markup language and some other converter?*

    Because it's the default on GitHub.
    If we're going to teach people to use that site,
    we should teach them to use it as it is,
    not as we wish it was.

*   *Where should pages go if multiple workshops are running at a site simultaneously?*

    Use subdirectories like `2015-07-01-esu/beginners`,
    so that main directory names always follow our four-part convention.

*   *What if I want to add more values to `index.html`, like `address1` and `address2` for different rooms on different days?*

    Go ahead,
    but you *must* have the variables described in [CUSTOMIZATION.md](CUSTOMIZATION.md).

*   *What is the "Windows installer"?*

    We have built a small installation helper for Windows
    that installs nano and SQLite, adds R to the path, and so on.
    It is maintained in
    [https://github.com/swcarpentry/windows-installer](https://github.com/swcarpentry/windows-installer),
    which also has an up-to-date description of what it actually does.
    The latest version is always available at
    [http://files.software-carpentry.org/SWCarpentryInstaller.exe](http://files.software-carpentry.org/SWCarpentryInstaller.exe);
    contributions are always welcome.

## Debugging

*   *Eventbrite registration isn't showing up on the workshop's home page.*

    First check that you have something like

    ~~~
    eventbrite: 1234567890AB
    ~~~

    at the YAML header of `index.html`.
    If the YAML header is set properly you probably are accessing
    `file:///home/to/workshop/directory/_site/index.html` directly.
    Instead,
    please run

    ~~~
    $ jekyll serve --config _config.yml,_config_dev.yml
    ~~~

    and look at `http://localhost:4000` in your browser
    (or push your changes to GitHub and view your page there).

*   *What do I do if I get a "can't convert nil into String" error?*

    On some Linux distributions (e.g, Ubuntu 14.04), you may get this error:

    ~~~
    $ ./tools/preview
    /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require': iconv will be deprecated in the future, use String#encode instead.
    /usr/lib/ruby/1.9.1/time.rb:265:in `_parse': can't convert nil into String (TypeError)
	    from /usr/lib/ruby/1.9.1/time.rb:265:in `parse'
	    from /usr/bin/jekyll:95:in `block (2 levels) in <main>'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1391:in `call'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1391:in `block in parse_in_order'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1347:in `catch'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1347:in `parse_in_order'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1341:in `order!'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1432:in `permute!'
	    from /usr/lib/ruby/1.9.1/optparse.rb:1453:in `parse!'
	    from /usr/bin/jekyll:137:in `<main>'
    ~~~

    This occurs because you are using an old version of Jekyll located in `/usr/bin`.
    Make sure that you have installed Jekyll using:

    ~~~
    $ gem install jekyll
    ~~~

    This installs Jekyll in `/usr/local/bin`,
    so make sure this directory comes before `/usr/bin` in your `PATH` environment variable.
    When your path is set correctly,
    you should see:

    ~~~
    $ which jekyll
    /usr/local/bin/jekyll
    ~~~

    You may also have to install the `nodejs` package to disable references to JavaScript,
    which you can do using:

    ~~~
    $ sudo apt-get install nodejs
    ~~~

    For more information, see
    [http://michaelchelen.net/81fa/install-jekyll-2-ubuntu-14-04/](this article).

*   *Help, my website isn't rendering correctly once its pushed to GitHub!*

    This can occur if you're trying to view the website over a HTTPS connection
    because the content from the Software Carpentry website is not currently served over HTTPS.
    Your browser sees this as unsecure content, so won't load it.

    To solve this,
    use `http` in the URL instead of `https`
    and make sure the link you distribute does so as well.
    If you're using a browser plugin like [HTTPS Everywhere](https://www.eff.org/https-everywhere)
    you will need to disable it for your workshop's site.
    We are presently (January 2015) working to get HTTPS working properly on our website.

*   *Help, my github.io website is not updating!*

    Ensure that strings in the index.html header are enclosed in quotations `"`.
    Special characters such as `"&"` may render correctly on your local machine but cause rendering to fail (silently?) on GitHub.
