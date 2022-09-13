# Welcome!

OCamlverse is an effort to document everything worth knowing about
[OCaml](http://www.ocaml.org/), an industrial-strength
functional programming language.

* [Community](content/community.md)
* [Quickstart](content/quickstart.md)
* [Learning](content/learning.md)
* [Frequently asked questions](content/faq.md)
* [Best Practices](content/best_practices.md)
* [Windows Support](content/windows_support.md)
* [Ecosystem](content/ecosystem.md)
* [Future of OCaml](content/future_ocaml.md)
* [Help Wanted](content/help_wanted.md):
list of projects that could use assistance.
* [Compiler](content/compiler.md)
* [Interesting Videos](content/video.md)
* [Google Summer of Code](content/gsoc.md)

## About OCamlverse

OCamlverse is intended to be a fast-moving web site that's easy to
contribute to. We maintain the site on GitHub and treat it almost like
a Wiki.

* [Learn More About OCamlverse](content/about.md)

## Contributing

We depend on the OCaml community's help to make OCamlverse better.
Please contribute! You can:

* [Suggest improvements!](https://github.com/OCamlverse/ocamlverse.github.io/issues)
* [Edit the site and submit a Pull Request!](https://github.com/OCamlverse/ocamlverse.github.io/pulls)
* After building up a history of PRs maintaining the site, you can ask to join the team and help maintain the site (use an Issue).

**Note:** It is important to read our [Contribution Guidelines](content/contrib.md).
They explain the rules for contributing to OCamlverse and how to be a
good contributor.

(We use the terrific [ahrefs](https://ahrefs.com) service to crawl and check our site.)

## Running OCamlverse Locally

OCamlverse is built with [Jekyll](https://jekyllrb.com/), a popular static site generator that originally powered GitHub Pages.

If you want to run OCamlverse (e.g. to preview some changes you've made) all you need to do is:

- Install Ruby (Jekyll is written in Ruby)
- Run the following shell commands in OCamlverse's source folder:

``` shellsession
$ bundle
$ bundle exec jekyll serve
```

At this point you can point your browser to <http://127.0.0.1:4000> and view the
locally running site.

**Note:** If you are using Ruby version 3 or above, you will need to add the `webrick` gem to the Gemfile prior to running `bundle install`.

## License

All content here is licensed under the [CC0 ("No Rights Reserved")](https://creativecommons.org/share-your-work/public-domain/cc0/) license.
