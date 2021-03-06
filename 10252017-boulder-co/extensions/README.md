Catalog Extensions
==================

History
-------

    Oct 23-25, 2017

    Constributers:

    Pramukta Kumar
    Robert St. John
    Ami Rahav
    Dan Lopez
    Ian Schneider

Goals
-----

The intention is that a default catalog might only contain high-level
metadata about the catalog but the extension mechanism allows description
of both catalog-level additions as well as catalog item additions.

For example, in addition to the core item fields, a vendor might have
additional fields of interest that can be described via the extension
mechanism.

Similarly, one catalog provided might provide a tile service using a standard protocol, such as WMTS, but another provider might only implement a non-standard service. The intention of service extensions is to allow discoverability of these services, both well-known or vendor specific, as well as related documentation, narrative or machine-readable.

Since services (or other links in general) might not directly support a simple link that responds to a GET request (e.g. all state is in the URL), we propose a means to describe more complex interactions that might be driven by one or more items in the catalog (for example, a composite tile-service that is capable of rendering pixels from multiple catalog items) or even requires a POST body using fields within a catalog record. In addition to supporting more complex protocols, this also allows reduction of 'inline' links - for example, a thumbnail link could be a direct property of an item OR describable as a service with URL variables that can be obtained using item fields.

Contents
========

Swagger Spec
------------

The specification at `extensions-swagger.yml` contains a single operation,
GetCapabilities, and attempts at modeling metadata and service extensions.

While valid, we have not attempted to implement a server or client.

Catalog Records
---------------

The `planet-` and `dg_` prefixed files contain records obtained directly from the respective APIs, a converter, and both minimal and extension records illustrating the process of 'converting' to a standard.

The `-minimal` extension represents the minimal data for a compliant catalog while the `-ext` extension demonstrates a response compliant with declared extensions (see the `planet-caps.json`, for example)

Example Capabilities Response
-----------------------------

The `planet-caps.json` file represents what an example response might look like. In this case, the interesting parts are the `services` and `extensions` properties.

The `extensions` property describes 2 simple catalog item field extensions. These additions are reflected in the `planet-search-results-ext.json` example response.

The `services` property is a bit more complex. This example declares a TMS service that is applicable for all catalog items. By using URL variables, a client could generate the URL for any single item in the catalog using values obtained from the record. While this example case could easily be represented as an inline 'link' (and in fact is - to support a simpler client), the more important part is that in Planet's case, this service actually supports 'composite' tiles - generated from multiple items. This means that such a link cannot be described inline but instead must be generated by the client based on the user's 'selection'.
