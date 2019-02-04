Open Web UI Design Specification for Enabling Automation (OUIA) 1.0
===================================================================

Abstract
--------

This specification is designed to promote certain key guidelines to follow when creating a new web
framework or application. Its goal is to ease the burden of individuals wishing to create and
maintain automated testing environments.

The OUIA is composed of multiple sections. An element of an app/framework, can be said to be
compliant with either all of the specification, or one or more of its parts. As such it is defined
as a _composable_ specification. The reason for this is largely due to the prevalent demarcation
between responsibilities of framework and application developers. For instance an application may
use a particular web framework, and be unable to negotiate compliance of that framework with OUIA.
However they may choose to make the elements that they _do_ have control over, fully compliant
with the OUIA.

Language
--------

The key words "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL NOT**",
"**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**MAY**", and "**OPTIONAL**" in this document
are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

Namespacing
-----------

For the purpose of fulfilling or augmenting this specification, including any and all future work:

* All HTML elements created, **MUST** be prefixed with `ouia`.
* All custom HTML attributes, **MUST** be prefixed with `data-ouia`.
* Any additional attributes to Javascript objects, must be prefixed with `ouia`.

Specification Parts
-------------------

The OUIA specification is split up into several sections. As stated, an application or
framework can one or more of the following specification parts, but each section must be implemented
completely. Thus a project can be said to be `OUIA:Widget` or `OUIA:Page` compliant,
as opposed to being completely `OUIA` compliant, but **ALL** components of the
`OUIA:Widget` part **MUST** be adhered to.

The following blocks exist in the specification:

* `OUIA:Widget` - widgets and widget frameworks
* `OUIA:Page` - page identification
* `OUIA:PageSafety` - interaction safety

### `OUIA:Widget`
This part is designed to cover widgets in use on pages. Widgets that are `OUIA:Widget` compliant
**MUST** have the following properties.

* A root level HTML element with a `data-ouia-widget-type` attribute describing a unique name
  identify HTML widgets that can **ALL** be controlled with the same code or interactions.
  * e.g. A page that has a special dropdown, could choose to name that dropdown as `CustomDropdown`.
    All instances of this `CustomDropdown` widget **MUST** be expected to be able to be controlled
    via the same automation.
* An id attribute called `data-ouai-widget-id` this is **OPTIONAL** if there will only be
  one instance of the widget on the page at once. Any `id` on the page **MUST** be unique
  even if it is used by different widget.
  * e.g. A vertical navigation can be expected to only be instantiated once on a page, as such
    it does not need any other identifying factors. Another widget type, like a button, would be
    created multiple times on a page and requires some kind of value as a unique identifying id.
* An attribute called `data-ouia-safe` which is `True` only when the widget is in a static state,
  i.e. no animations are occurring. At all other times, this value **MUST** be `False`.

### `OUIA:Page`
This part is designed to cover page identification. Pages that are `OUIA:Page` compliant **MUST**
have the following properties:

* A `<ouia-page>` html tag with the following attributes:
  * A `type` attribute which determines the base context of the page.
     * e.g. A page listing some inventory of food items could have `food` as its `type` attribute.
  * A `action` attribute, which determines if the page has a controller
     associated with it to perform a specific action. This is **OPTIONAL** if the page does
     not describe a specific action, or is a single action screen displaying information only.
     * e.g. A page providing the edit action of an inventory item could have an `edit` value
       for the `action` attribute. Whereas a modal about page would not need a `action`
       attribute.
  * A page which dynamically changes action without a page reload **MUST** correctly update the
    `type` and `action` attributes if the context of the page changes.
  * An **OPTIONAL** `object-id` attribute, where the page is in the context of a specific instance
    of an object.
    * e.g. A page describing a food item that is being edited, could have an `id` field of 142526.

##### Example of `OUIA:Page`
A page describing the edit action of a food item with the id 142526 could have an attribute
looking like `<ouia-page type="food" action="edit" object-id="142526">`

### `OUIA:PageSafe`
* A javascript accessible attribute named `ouia-page-safe` which declares whether the page
  is safe to access. This should roll up a single value which represents the completion of:
  * Page animations
  * XHR requests
  * Any other operations which affect the DOM structure

### Declaration of Conformity
A project wishing to declare its conformity should use one of the supplied badges, or in the
case that the entire spec has been conformed to in its entirety, should proudly display the overall
compliance badge.

![Compliant Badge](ouia.svg)

![Compliant Badge](ouia-widget.svg)

![Compliant Badge](ouia-page.svg)

![Compliant Badge](ouia-pagesafe.svg)
