---
layout: post
title: "Quest for a custom CSL validator"
---

If you have experience with RESTful APIs, I have a job for you :).

Validating CSL styles and locale files against the CSL schema plays a very important role in our quality control process. Currently we [point](https://github.com/citation-style-language/styles/wiki/Validation) users to one of two sites:

[csl-validator.js](http://simonster.github.io/csl-validator.js/), by Simon Kornblith of Zotero, and based on the *rnv* XML validator, has the simplest interface. This dedicated CSL validator is a little bit clunky (e.g., on smaller screens, it is very easy to get 'caught' in the giant text window when scrolling down the page to get to the "Validate" button), and limited in options.

[Validator.nu](http://validator.nu/), based on the *Jing* XML validator, is a general HTML/XML validator. It has convenient options for validating files by URL, via upload, or via copy and paste. It also allows for customization of the schema used for validation. However, users always need to make sure the correct settings are used, and the validator always produces some warnings that are irrelevant to the user.

High on my wish list is a dedicated CSL validator more flexible than csl-validator.js, and less cluttered than Validator.nu. Since Validator.nu offers a RESTful interface, it seems relatively easy to create a customized frontend for this validator. If this sounds like a fun project, please drop me a line on Twitter or via the contact form on [CitationStyles.org](http://citationstyles.org/).

To get things started, I made a comparison between the current interface of Validator.nu, and a simplified interface for CSL:

<figure class="half">
	<img src="/images/validator-original.png">
	<img src="/images/validator-customized.png">
	<figcaption>Original (left) and mockup (right) layout for Validator.nu</figcaption>
</figure>

Future additional improvements could include support for Schematron validation, and implementation of some other checks that go beyond the CSL schema. Jing currently ignores the embedded Schematron rules in the CSL schema, but it's possible to extract these rules into a dedicated Schematron schema, and do a secondary validation against that. We also use Travis CI to perform a range of extra checks on styles submitted to our style repository, and it might be possible to run some of these in our validator as well (e.g., all style IDs have to start with "http://www.zotero.org/styles/...").