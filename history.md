History
=======

The OUIA specification project was created after years of work automating the
ManageIQ project. The project had a very basic SOAP API that did not have feature
parity with the UI. As such, despite the difficulty in creating such automation,
in order to have a full regression suite of tests, the UI was the only option.

Several consistent themes emerged from the five years of efforts. These themes
were distilled down into a wishlist. If only the UI could provide us with X.
When the ManageIQ project started standardising on Patternfly, and with a new
version of Red Hat Insights also using the Paternfly library, it felt like the
right time to start looking at solidifying some of these requests and pushing them
as upstream as we could.

Specifically we were looking for:

 * Notification that any items had finished animating
 * Notification that the page was considered safe to touch
 * Web Components to declare themselves on the page

Though HTML elements can often be inferred, it is far easier to find them if there
are explicit standard attributes to look for. The OUIA requests that framework component
developers specifically include certain attributes to assist in the discovery of their
elements on the page.

Developers of the site/application are required to adhere to certain other standards
to assist in page function discovery, as well as to provide notification of the page
being in an unsafe state.
