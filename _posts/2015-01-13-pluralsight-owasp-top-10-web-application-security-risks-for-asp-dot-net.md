---
layout: post
title: "Pluralsight - OWASP Top 10 Web Application Security Risks for ASP.NET"
---
{% include JB/setup %}

## Injection


## XSS

### Output encode for the correct context
Ensure strings are output encoded correctly to mitigate XSS risks. Different outputs need to be encoded differently. Different outputs are required for: CSS, HTML, HTML attribute, HTML form URL, JavaScript, LDAP distinguished name, LDAP filter, URL, URL path, XML, XML attribute.

For example <i>Lager</i> is encoded in the following different ways:

Context | Encoded String
---|---
HTML | &lt;i&gt;Lager&lt;/i&gt;
JavaScript | \x3ci\x3eLager\x3c\x2fi\x3e
CSS | \00003Ci\00003ELager\00003C\00002F

### AntiXss Framework

In .NET applications the AntiXss framework contains some useful functions for output encoding HTML (in the `System.Web.Security.AntiXss` namespace)

    var searchTerm = Request.QueryString["q"];
    uxSearchTerm.Text = AntiXssEncoder.HtmlEncode(searchTerm, true); // use named entities

In order to output encode untrused data for the JavaScript context an additional library from NuGet is required also called AntiXss (also contains HTML encoders for pre 4.5 users)

    <script type="text/javascript">
        var q =  <% Microsoft class="Security Application Encoder JavaScriptEncoder(Request.QueryString["q"]) %>
    </script>

### Automatic output encoding

In ASP.NET web forms, the first example above, the label control's text attribute did not implement output encoding. This had to be added explicitly. However some controls and attributes do automatically include output encoding. Test this by outputting e.g. <i>Lager</i> and check if it is encoded correctly or not. 

In ASP.NET MVC the razor view engine automatically HTML encodes all output by default. The HtmlHelper (`@Html.Label("<i>Lager</i>")`) also encodes output. In order to stop the output encoding you need to use the Raw Html Helper (`@Html.Raw("<i>Lager</i>")`)

### Request validation

Explicitly whitelist data using a regex.

    if (!Regex.IsMatch(searchTerm, @"^[\p{L} \.\-]+$")) {
        throw new ApplicationException("Search term not allowed");
    }

ASP.NET by default uses RequestValidation which checks all untrused data for XSS. This can be configured in the web.config in the pages element:

    <pages validateRequest="false" />

On occasion, you may wish to POST html tags e.g. in a rich text editor. You can turn it off at the page level if necessary using `ValidateRequest="false"` in the page declaration of the code behind. (requestValidationMode needs to be set to 2.0 for this to work.)

As of .NET 4.5 the validation can only be turned off per control, but not per page. To do this:
1. Ensure requestValidationMode ( attribute of <system.web><httpRuntime> ) is set to 4.5
2. On the individual control set `ValidateRequestMode` attribute to `Disabled`

Additionally to access potentially dangerous query string requests use `Request.Unvalidated.QueryString`. In this way you can bespoke the request handling.

In ASP.NET MVC the `[AllowHtml]` attribute can be used to decorate the field in a model to e.g. allow special characters like `<` and `>` in a password field.

IMPORTANT. Always code as though request validation doesn't exist.

### Reflected XSS v Persisted XSS

So far all XSS examples have been reflected XSS. However, there may be persistant XSS in the database. In order to mitigate the risk of this running on the page, all data should be output encoded (e.g. using AntiXss.HtmlEncode at bind time)

### Browser behaviour

Different browsers may have their own defences against XSS. For example IE will post a message "Internet Explorer has modified this page to help prevent cross-site scripting" in the event of a potentially dangerous payload." This behaviour can be controlled via the use of custom headers e.g. in the web.config of the application.

    <system.webServer>
        <httpProtocol>
            <customHeaders>
                <clear/>
                <add name="X-XSS-Protection" value="0">
            </customHeaders>
        </httpProtocol>
    </system.webServer>

### Payload obfuscation

* URL encode the whole query string
* Use a service like bit.ly or tinyurl
