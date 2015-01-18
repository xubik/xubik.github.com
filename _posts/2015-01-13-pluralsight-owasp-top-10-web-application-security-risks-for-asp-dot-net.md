---
layout: post
title: "Pluralsight - OWASP Top 10 Web Application Security Risks for ASP.NET"
---
{% include JB/setup %}

## Injection


## XSS

Ensure strings are output encoded correctly to mitigate XSS risks. Different outputs need to be encoded differently. Different outputs are required for: CSS, HTML, HTML attribute, HTML form URL, JavaScript, LDAP distinguished name, LDAP filter, URL, URL path, XML, XML attribute.

For example <i>Lager</i> is encoded in the following different ways:

Context | Encoded String
---|---
HTML | &lt;i&gt;Lager&lt;/i&gt;
JavaScript | \x3ci\x3eLager\x3c\x2fi\x3e
CSS | \00003Ci\00003ELager\00003C\00002F

In .NET applications the `AntiXssEncoder` class contains some useful functions for output encoding HTML (in the `System.Web.Security.AntiXss` namespace)

    var searchTerm = Request.QueryString["q"];
    uxSearchTerm.Text = AntiXssEncoder.HtmlEncode(searchTerm, true);

In order to 