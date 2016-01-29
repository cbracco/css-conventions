# CSS Conventions

*based on [idiomatic-css](https://github.com/necolas/idiomatic-css)*

Enclosed in this document are organizational guidelines for CSS development. I do not wish to impose my style preferences on your code; however, outlining some common, sensible patterns will help keep your codebase lean and more readable for all developers involved, whether new or existing.

Ideas are always welcome. Please contribute!

### Table of contents

- [General principles](#general-principles)
	- [Indentation](#indentation)
	- [Capitalization](#capitalization)
	- [Whitespace](#whitespace)
- [Naming conventions](#naming-conventions)
	- [Explanation](#naming-explanation)
	- [Usage](#naming-usage)
	- [Examples](#naming-examples)
	- [IDs vs. classes](#naming-ids-vs-classes)
- [Comments](#comments)
	- ["Table of contents" blocks](#comments-table-of-contents)
	- [Section blocks](#comments-section-blocks)
	- [Sub-section / Description blocks](#comments-subsection-description-blocks)
	- [Basic comments](#comments-basic)
- [Formatting](#formatting)
	- [Rulesets](#formatting-rulesets)
	- [Declaration order](#formatting-declaration-order)
	- [Exceptions](#formatting-exceptions)
	- [Misc.](#formatting-misc)

<a name=general-principles></a>
## General principles

<a name=indentation></a>
### Indentation

Never mix spaces and tabs when indenting code. My indentation style preference is **2 spaces**.

<a name=capitalization></a>
### Capitalization

Use **lowercase only** when writing CSS. Do not capitalize any CSS selectors, properties, or property values (with the exception of strings).

<a name=whitespace></a>
### Whitespace

Remove any trailing whitespace in your code, wherever possible. If your text editor has the option to automatically trim trailing whitespace, turn it on before working on a new application.

**Pro-tip:** configure your editor to "show invisibles". This will allow you to eliminate end-of-line whitespace, eliminate unintended blank line whitespace, and avoid polluting commits.

**Suggestion:** use an [.editorconfig](http://editorconfig.org/) file (or equivalent) to help maintain the basic whitespace conventions across the application.

<a name=indentation></a>
## Naming conventions

I prefer the [BEM](http://bem.info/method/definitions/), or "Block Element Modifier" methodology for naming IDs and classes.

Instead of presentational or cryptic names, try to write ID and class names that reflect the purpose of the property in question, or that are otherwise generic.

<table>
	<thead>
		<th>Bad</th>
		<th>Good</th>
	</thead>
	
	<tr>
		<td><code>#twr-34575665 {}</code> - confusing</td>
		<td><code>#gallery {}</code> - provides purpose</td>
	</tr>
	
	<tr>
		<td><code>.button-green {}</code> - presentational</td>
		<td><code>.button--primary {}</code> - generic & reusable</td>
	</tr>
</table>

<a name=naming-explanation></a>
### Explanation

The different parts of your application layout (eg. header, navigation, content, footer) can be thought of separate **"blocks"** that make up the entire layout. A block can either be simple or compound (containing other blocks).

These blocks will often have various **"elements"** that perform certain functions (eg. the input field and submit button in a search form). Elements only make sense in the context of the block containing them.

**"Modifiers"** are used when you want to create a block that is similar to the default, but with a slightly altered appearance or behavior (eg. a button that is green instead of black).

<a name=naming-usage></a>
### Usage

When writing ID and class names, use **hyphens** to separate the name of the block from the name of the element, and use **underscores** to separate words in long names.

This makes it easy to double-click and select different portions of the name, and easy to distinguish between a block name and an element name.

<a name=naming-examples></a>
### Examples

#### Generic structure

	.block-name               {} /* Block */
	.block-name__element-name {} /* Element */
	.block-name--modifier     {} /* Modifier */

#### Simple blog post example

	.post          {} /* Block */
	.post__image   {} /* Element */
	.post__title   {} /* Element */
	.post__date    {} /* Element */
	.post__excerpt {} /* Element */
	.post--last    {} /* Modifier */

<a name=naming-ids-vs-classes></a>
### IDs vs. classes

**Use classes whenever possible.** IDs are unique; classes are not. IDs should only appear once on any given page, while classes can be used multiple times on any given page.

I’d recommend only using IDs when you need to build navigation with anchor links, or when you need to target an element with JavaScript.

<a name=comments></a>
## Comments

Well-commented code is always a tremendous help for all, but especially for new developers. Take the time to describe CSS properties and values; don’t leave the team guessing!

* Place comments on a new line, above their subject.
* Avoid end-of-line comments.
* Keep line-length at a sensible maximum (somewhere around the [Python convention of 72 characters](http://www.python.org/dev/peps/pep-0008/#maximum-line-length) is recommended. I personally use **80 characters**).
* Make liberal use of comments to break code up into sensible sections.

**Pro-tip:** configure your text editor to provide you with keyboard shortcuts to output the agreed-upon comment patterns.

<a name=comments-table-of-contents></a>
### "Table of contents" blocks

Always include a "Table of contents" at the top of the CSS file. This gives developers an overview of the sections within the file, and instructions on how to use the text editor’s built-in “find” function to navigate to a specific section in the code.

	/* ================================================================== *\
	   Table of contents
	   (Ctrl/Cmd + F, and search for `$section` to jump to a section)
	   01. Base................Normalize.css (minified), important styles
	   02. Typography..........Basic typography elements
	   03. Non-typography......Important elements that are not type-based
	   04. Grids...............A simple grid system and width classes
	   05. Layout..............Common layout items (wells, islands, etc)
	   06. Buttons.............Basic styles, sizes, and shapes
	   07. Tables..............Styles for tabular data
	   08. Main................Your styles go here!
	   09. Helpers.............Some useful, global classes
	   10. Print...............Inlined, barebones print styles
	\* ================================================================== */

<a name=comments-section-blocks></a>
### Section blocks

Use the following comment style to define a new section in your stylesheet. Make sure to add the "($section)" portion to the comment block so that developers can use their text editors’ built-in “find” function to navigate to that section in the code.

	/* ================================================================== *\
	   Section ($section)
	\* ================================================================== */

<a name=comments-subsection-description-blocks></a>
### Sub-section / Description blocks

Use the [Doxygen-style](http://doxygen.org) comment block to define a sub-section within a main section in your stylesheet. This can also be used to describe the code directly beneath it. Use a number system to indicate the attributes that are related to the description.

	/**
	 * Header
	 */

**or,**

	/**
	 * 1. Inherits percentage declared on above <html> as the root `font-size`
	 * 2. Unitless `line-height`, which acts as a multiple of the root `font-size`
	 */

	body {
	    color: #444;
	    font-size: 1rem;  /* 1 */
	    font-family: "Helvetica Neue", Arial, sans-serif;
	    line-height: 1.5; /* 2 */
	}

<a name=comments-basic></a>
### Basic comments

Use the traditional CSS commenting format when you want to type something brief about a property, attribute, value, etc.

	/* This is a thing */

<a name=formatting></a>
## Formatting

The formatting of your CSS should be easy to read and easy to clearly comment. This helps reduce the chance of accidents and errors.

<a name=formatting-rulesets></a>
### Rulesets

* Type one selector per line in multi-selector rulesets.
* Type a single space before the opening brace of a ruleset.
* Use one declaration per line in the declaration block.
* Always include a semi-colon at the end of a declaration.
* Place the closing brace in the same column as the first character in the ruleset.
* Separate each ruleset with a blank line.
* Always align vendor prefix values vertically.

**And, voila:**

	.selector-1,
	.selector-2,
	.selector-3 {
	    -webkit-box-sizing: border-box;
	    -moz-box-sizing:    border-box;
	    box-sizing:         border-box;
	    display: block;
	    color: #333;
	    background: #fff;
	}

<a name=formatting-declaration-order></a>
### Declaration order

My preference for ordering properties within a ruleset is to group them into related sections. You do not have to comment each section, but try to get into the mindset of grouping your properties in this order.

	.selector {
	    /* Positioning */
	    position: absolute;
	    z-index: 10;
	    top: 0;
	    right: 0;
	    bottom: 0;
	    left: 0;
	
	    /* Display & Box Model */
	    display: inline-block;
	    overflow: hidden;
	    box-sizing: border-box;
	    width: 100px;
	    height: 100px;
	    padding: 10px;
	    border: 10px solid #333;
	    margin: 10px;
	
	    /* Other */
	    background: #000;
	    color: #fff;
	    font-family: sans-serif;	
	    font-size: 16px;
	    text-align: right;
	}

**Protip:** if your text editor supports it, I recommend installing [CSSComb](http://csscomb.com/), a plugin that lets you automatically re-order your CSS properties with a quick keyboard shortcut. It’s sweet.

<a name=formatting-exceptions></a>
### Exceptions

Large blocks of rulesets with only one declaration can use a **single-line** format. A space should be included after the opening brace and before the closing brace.

	.selector-1 { width: 10%; }
	.selector-2 { width: 20%; }
	.selector-3 { width: 30%; }

Longer property values - such as collections, gradients, and shadows - can be arranged across **multiple lines** to improve readability.

	.selector {
	    box-shadow:
	        1px 1px 1px #000,
	        2px 2px 1px 1px #ccc inset;
	    background-image:
	        linear-gradient(#fff, #ccc),
	        linear-gradient(#f3c, #4ec);
	}

<a name=formatting-misc></a>
### Misc.

- Use lowercase hex values, e.g., #aaa.
- Use single or double quotes consistently. Preference is for double quotes, e.g., content: "".
- Always quote attribute values in selectors, e.g., input[type="checkout"].
- Where allowed, avoid specifying units for zero-values, e.g., margin: 0.
