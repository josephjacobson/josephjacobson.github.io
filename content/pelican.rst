Getting Started With Pelican
############################

:date: 2018-12-08 08:30
:slug: pages-pelican
:authors: joej
:summary: Getting started on pages.github.com with Pelican


Time to put some content in `GitHub Pages <https://pages.github.com/>`_.

We'll need an ssh key first.  I have a lot of keys and use a ``<user>.<domain>``
convention to keep track of them::

  ssh-keygen -t ed25519 -o -f ~/.ssh/keys/josephjacobson.github.com

The corresponding ``~/.ssh/config`` bit::

  Host github.com
    User git
    IdentityFile ~/.ssh/keys/josephjacobson.github.com

Now we can clone and commit::

  git clone git@github.com:josephjacobson/josephjacobson.github.io.git

I have a lot of git repos too, so let's be explicit in this particular repo
about the user::

  cd josephjacobson.github.io
  git config --local user.name "Joseph Jacobson"
  git config --local user.email "jacobson@pobox.com"


Setup complete.  Now what to put here....
`StaticGen <https://www.staticgen.com/>`_ has a bunch of interesting options.
I use `jinja2 <http://jinja.pocoo.org/>`_ a lot with
`ansible <https://www.ansible.com/>`_ and
`cdm <https://cloud.google.com/deployment-manager/docs/quickstart>`_, so let's
try `pelican <https://getpelican.com/>`_.


Using a mac, but don't want to pollute the base install, so user install it is::

  easy_install --user pip
  PATH="~/Library/Python/2.7/bin:$PATH"
  pip install --user pelican
  pip install --user Markdown

The `docs <http://docs.getpelican.com/en/stable/install.html#kickstart-your-site>`_ say ``pelican-quickstart``. I ran into this::

  $ pelican-quickstart   
  Traceback (most recent call last):
    ...
    File ".../Library/Python/2.7/lib/python/site-packages/pelican/utils.py", line 29, in <module>
      from six.moves.html_parser import HTMLParser

But force installing a user verison of ``six`` fixed it::

  pip install --user --force-reinstall six

If you told ``pelican-quickstart`` you were going to use GitHub Pages, it
will set up the ``Makefile`` to use ``ghp-import`` for publishing.  You can
found out more about this here:

- http://docs.getpelican.com/en/stable/tips.html

Install with::

  pip install --user ghp-import

So the workflow should be create a git branch, e.g. `pelican`.  Set up pelican
and save content there.  Then do a ``make publish`` and ``make github`` to 
copy the output to the ``master`` branch. 

Docs are pretty straightforward about building content.  A bunch of
`themes <http://pelicanthemes.com/>`_ are available, but didn't see anything
that immediately appealed to me.  The
`simple <https://github.com/getpelican/pelican/tree/master/pelican/themes/simple/templates>`_
theme is available by default, so I decided to ``cp`` and
`hack <http://docs.getpelican.com/en/stable/themes.html>`_ on that.  Use
``pelican-themes -v -l`` to find the locally installed files.

Spent some time refreshing my CSS and HTML.  Normalizing css instead of full
resets seem to popular right now.  New semantics in HTML5.

- https://github.com/necolas/normalize.css
- https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5

I think I've gotten the basic stuff done at this point.
I'll iterate improvements as I go.

