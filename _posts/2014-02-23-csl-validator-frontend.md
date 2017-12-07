---
layout: post
title: "Quest for a custom CSL validator [2014-02-23]"
---

*Update October 2014. I developed the envisioned CSL validator frontend myself. It is live at [http://validator.citationstyles.org/](http://validator.citationstyles.org/).*

If you have experience with RESTful APIs, I have a job for you :).

Validating CSL styles and locale files against the CSL schema plays a very important role in our quality control process. Currently we [point](https://github.com/citation-style-language/styles/wiki/Validation) users to one of two sites:

[csl-validator.js](http://simonster.github.io/csl-validator.js/), by Simon Kornblith of Zotero, and based on the *rnv* XML validator, has the simplest interface. This dedicated CSL validator is a little bit clunky (e.g., on smaller screens, it is very easy to get 'caught' in the giant text window when scrolling down the page to get to the "Validate" button), and limited in options.

[Validator.nu](http://validator.nu/), based on the *Jing* XML validator, is a general HTML/XML validator. It has convenient options for validating files by URL, via upload, or via copy and paste, and allows for customization of the schema used for validation. It can also show the validated document, and highlight the lines where errors have occurred. However, users always need to make sure the correct settings are used, and the validator always produces some warnings that are irrelevant to the user.

High on my wish list is a dedicated CSL validator more flexible than csl-validator.js, and less cluttered than Validator.nu. Since Validator.nu [offers](http://about.validator.nu/#api) a RESTful interface, it seems relatively easy to create a customized frontend for this validator. If this sounds like a fun project, please drop me a line on Twitter or via the contact form on [CitationStyles.org](http://citationstyles.org/contact).

To get things started, I made a comparison between the current interface of Validator.nu, and what I imagine a simplified interface for CSL to look like:

<figure class="half">
    <a href="/images/validator-original-large.png"><img src="/images/validator-original.png"></a>
	<a href="/images/validator-customized-large.png"><img src="/images/validator-customized.png"></a>
	<figcaption>Original (left) and mockup (right) layout for Validator.nu</figcaption>
</figure>

The changes would be:

- hide the "Encoding" field (keep default value of "As set by the server/page")
- change the "Schemas" text field, which currently accepts a URL to a schema, to a dropdown menu where the user can simply select the desired CSL schema version
- hide the "Preset" field (keep default value of "None")
- hide the "Parser" field (change value to "XML; don't load external entities")
- hide the "XMLNS Filter" field
- hide the "Be lax about HTTP Content-Type" checkbox (check)
- hide the "Show Image Report" checkbox (keep unchecked)
- hide the "Show Source" checkbox (check)
- hide the "Show Outline" checkbox (keep unchecked)
- hide any warnings in the validation output

We could host the validator via GitHub Pages, and link to it from validator.citationstyles.org.

Future additional improvements could include support for Schematron validation, and implementation of some other checks that go beyond the CSL schema. Jing currently ignores the embedded Schematron rules in the CSL schema (which we use to make sure all called macros really exist), but it's possible to extract these rules into a dedicated Schematron schema, and do a secondary validation against that. We also use Travis CI to perform a range of extra checks on styles submitted to our style repository, and it might be possible to run some of these in our validator as well (e.g., all style IDs have to start with "http://www.zotero.org/styles/...").
