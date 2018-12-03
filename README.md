Web UI Design Specification for Automation (OpenUIAuto) 1.0
=========================================================

Definition
----------

This document is designed to describe certain key guidelines to follow when creating a new web
framework or application. It's goal is to ease the burden of the QA department in creating and
maintaining automated testing environments. Each section is designed to be adhered, or implemented
in isolation, meaning that it is a composable specification, as opposed to an all or nothing
approach. This has been done to allow users/teams to use a web framework that does not meet the
OpenAuto specification for widgets, whilst maintaining the adherence to the specification for
page identification.

Adherence Blocks
----------------

The OpenUIAuto specification is split up into several sections. As stated, an application or
framework can one or more of the following sub-specifications, but each section must be implemented
completely. Thus a project can be said to be `OpenUIAuto/Widget` or `OpenUIAuto/Page` compliant,
as opposed to being completely `OpenUIAuto` compliant.

The following blocks exist in the specification:

* `OpenUIAuto:Widget` - covering adherence of widgets and widget frameworks
* `OpenUIAuto:Page` - covering adherence of page identification

### `OpenUIAuto:Widget`
This Adherence block is designed to cover widgets in use on pages. Widgets that are
`OpenUIAuto:Widget` compliant have the following properties.

* A root level HTML element with a `data-ouia-widget-type` attribute describing a unique name to identify
  HTML widgets that can be controlled with the same code. All instances of this `CustomDropdown` widget should be expected to be able to be controlled
  via the same automation.
  * e.g. A page that has a special dropdown, may choose to name that dropdown as `CustomDropdown`.
* `[OPTIONAL]` An id attribute called `data-ouai-widget-id` this is only optional if there will never be
  more than one instance of the widget on the page at once. Any `id` on the page must be unique
  even if it is from a different widget.
  * e.g. A vertical navigation can be expected to only be instantiated once on a page, as such
    it does not need any other identifying factors. Another widget type, like a button, may be
    created multiple times on a page and requires some kind of value as an id.

### `OpenUIAuto:Page`
This adherence block is designed to cover page identification. Pages that are `OpenUIAuto:Page`
compliant have the following properties.

* A named `<xxxx>` html tag with the following attributes:
  * A `data-ouia-page-type` attribute which determines the base content of the page
     * e.g. A page listing some inventory of food items could have `food-list` as its id
  * `[OPTIONAL]` A `data-ouia-page-action` attribute, which determines if the page has a controller
     associated with it to perform a specific action.
     * e.g. A page providing the edit action of an inventory item could have an `edit` value
       for the `data-ouia-page-action` attribute. This is mandatory if the page is providing an action
       or a specific view but not required when the page type has a lone page, for example
       an About page. 
  * `[OPTIONAL]` An `data-ouia-object-id` attribute, where the page is describing a specific instance
    of an object.
    * e.g. A page describing a food item that is being edited, could have an `id` field of
        142526.

Or

* A named `<data-ouia-page>` html tag with the following attributes:
  * A `page-type` attribute which determines the base content of the page
     * e.g. A page listing some inventory of food items could have `food-list` as its id
  * `[OPTIONAL]` A `page-action` attribute, which determines if the page has a controller
     associated with it to perform a specific action.
     * e.g. A page providing the edit action of an inventory item could have an `edit` value
       for the `page-action` attribute. This is mandatory if the page is providing an action
       or a specific view but not required when the page type has a lone page, for example
       an About page. 
  * `[OPTIONAL]` An `object-id` attribute, where the page is describing a specific instance
    of an object.
    * e.g. A page describing a food item that is being edited, could have an `id` field of
        142526.
* e.g. A page describing the edit action of a food item with the id 142526 could have an attribute
  looking like `<section page-type="food" page-action="edit" object-id="142526">`
  
