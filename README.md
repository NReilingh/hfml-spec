hfml-spec

# Hypertext Fragment Metadata Language

This specification aims to standardize a method by which written work,
typically edited and stored in a CMS with a unique site design,
could be made easily and safely portable to other CMSes with their own
unique design and style rules.
The name references the concept of a document fragment,
which is equivalent to a DOM node that can be considered outside
the context of a complete HTML document.

You can think of an HFML document as a chunk of HTML,
but without <html>, <head>, <body> tags, or a <!DOCTYPE> declaration,
stripped down to just the written content of your page,
without any additional HTML elements for navigation,
headers, footers, or anything structural to the site itself.
This is indeed how many CMS platforms store written content in their
internal databases, but this guarantees that that content is tightly
coupled to the site implementation (CMS plugins, for example, or
specific custom style rules).
By standardizing a format that encapsulates only the needed context
to keep the content itself decoupled from the CMS,
written content can be stored in a truly canonical format.

So far, the best attempts to solve this problem have been to use Markdown
and other textual formats for authoring, often with static site generation
tools for generating complete HTML documents for display in the web browser.
This specification does not aim to replace that pattern,
but simply to augment it so that these documents too are uncoupled
from their static site generator tooling.

Specifically, a `.hfml` file is a UTF8-encoded document written in
any language that supports `<!-- HTML-style comments -->`.
Markdown, being a superset of HTML, is thus supported.
The file opens with a structured, parseable comment containing
metadata (in a simple human-readable email header/YAML-like format)
which describes how the fragment can be integrated into a website,
and desired pieces of metadata about the fragment, like who authored it,
when it was authored, meta title and description, and contact information.
In the case of syntaxes like markdown, it can also formally
declare which implementation it would like to be parsed by.

Ideally, common content management systems would all use
HFML as their primitive storage format, paving the way for
truly git-centric editing workflows where a CMS is primarily just
a purpose-built git host, capable of managing a complex graph of
repositories and subrepositories. Different dev/test environments
for web publishing sites could be pointed at the same exact content repositories,
each simply slaved to a different branch, solving the problem of
developers having to do data dumps and synchronization,
and of editors having to decide to work on future versions of a page
in the live environment to avoid the error-prone and effort-duplicating
processes of making edits in a test site,
and then re-making those edits in a live site,
since if the developers _are_ doing data synchronization for development,
it's going to involve overwriting the test environment periodically.
