---
tags: [learning, best practices]
---

# Best Practices

Here is a collection of community-chosen best practices for successful programming in OCaml.

## Coding Style Tooling
Rather than spending precious time worrying about the correct format for syntax, it's much more convenient to have
tooling that will automatically lay out the code for you in a canonical manner. While ocp-indent used to be the clear
choice for automatic coding style, ocamlformat is a recent arrival that, inspired by ReasonML's `refmt` tool, uses
a more comprehensive approach of end-to-end parsing and printing. Both tools can be integrated into editors to automatically lay out code as you write it.

* [ocp-indent](https://github.com/OCamlPro/ocp-indent) is a coding style formatting tool that relies on heuristics and partial
parsing rather than a full end-to-end parsing and printing approach, like ocamlformat below. The advantage of ocp-indent's approach
is that even partially-compiling files can be indented, as can code fragments.
* [ocamlformat](https://github.com/ocaml-ppx/ocamlformat) is a comprehensive coding style formatting tool that parses the code
and prints it out again. This follows the example of the `refmt` tool for Reason. While new, `ocamlformat` may eventually overtake `ocp-indent`.

## Coding Style Guidelines
* [OCaml programming guidelines at ocaml.org](http://www.ocaml.org/learn/tutorials/guidelines.html)
* [XEN – OCaml Best Practices for Developers](http://wiki.xen.org/wiki/OCaml_Best_Practices_for_Developers)
* [Jane Street Style](https://opensource.janestreet.com/standards/)
* [Ocaml Towards Clarity and Grace](https://github.com/lindig/ocaml-style)

## Documentation Best Practices

* [Documentation Guidelines](documentation_guidelines.md)

## Writing Efficient Code

See [Optimizing OCaml performance](optimizing_performance.md)
