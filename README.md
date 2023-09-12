# Enterprise-Ready SSO Profile for OpenID Connect and SAML

## Authentication Contexts

* MFA Any Two Factors
* MFA Phishing Resistant



### OpenID Connect

#### MFA Phishing Resistant

`phr`

* Defined in https://openid.net/specs/openid-connect-eap-acr-values-1_0.html

#### MFA Any Two Factors

`urn:okta:loa:2fa:any`


### SAML

#### MFA Phishing Resistant

```xml
<samlp:AuthnRequest ...>
  ...
  <samlp:RequestedAuthnContext Comparison='exact'>
    <saml:AuthnContextClassRef>http://idmanagement.gov/ns/assurance/aal/2?phishing_resistant=true</saml:AuthnContextClassRef>
  </samlp:RequestedAuthnContext>
</samlp:AuthnRequest>
```

#### MFA Any Two Factors

[Section 3.3 Extensibility](http://docs.oasis-open.org/security/saml/v2.0/saml-authn-context-2.0-os.pdf)

> Additional authentication context classes MAY be developed by groups other than the Security Services Technical Committee. 

> Guidelines for the specification of new context classes are as follows:
> • Specify a URI that uniquely identifies the context class.
> • Provide contact information for the author of the class.
> • Provide a textual description of the circumstances under which this class should be used.
> • Provide a valid XML schema [Schema1] document implementing the class. 
> Authors of new classes are encouraged to review the classes defined within this specification in order to guide their work.


### Existing acr_values


* Okta ([Docs](https://developer.okta.com/docs/guides/step-up-authentication/main/#predefined-parameter-values))
  * `urn:okta:loa:1fa:any`
  * `urn:okta:loa:1fa:pwd`
  * `urn:okta:loa:2fa:any`
  * `urn:okta:loa:2fa:any:ifpossible`
  * `phr`
  * `phrh`
* NHS ([Docs](https://digital.nhs.uk/services/care-identity-service/applications-and-services/cis2-authentication/guidance-for-developers/detailed-guidance/acr-values#requesting-specific-acr-values))
  * `AAL3_ANY`
  * `AAL3_IOS`
    * `AAL3_IOS` authenticates the user using the NHS Care application
  * `AAL3_FIDO2`
  * `AAL3_N3_SMARTCARD`
  * `AAL1_USERPASS`
* Login.gov ([Docs](https://developers.login.gov/oidc/#request-parameters))
  * `http://idmanagement.gov/ns/assurance/ial/1`
  * `http://idmanagement.gov/ns/assurance/ial/2`
  * `urn:gov:gsa:ac:classes:sp:PasswordProtectedTransport:duo`
  * `http://idmanagement.gov/ns/assurance/aal/2`
  * `http://idmanagement.gov/ns/assurance/aal/2?phishing_resistant=true`
  * `http://idmanagement.gov/ns/assurance/aal/2?hspd12=true`



## Session Expiration


### SAML

SAML defines `SessionNotOnOrAfter` as:

> Indicates an upper bound on sessions with the subject derived from the enclosing assertion. The time value is encoded in UTC, as described in Section 1.3.3. There is no required relationship between this attribute and a NotOnOrAfter condition attribute that may be present in the assertion. It's left to profiles to provide specific processing rules for relying parties based on this attribute.

### OpenID Connect

[Draft 12 of OpenID Connect Session Management](https://openid.net/specs/openid-connect-session-1_0-12.html#ChangeNotification) said:

> ID Token typically comes with the expiry date. The RP MAY rely on it to expire the RP session.

However, that has been removed from the latest version:

https://openid.net/specs/openid-connect-session-1_0.html#ChangeNotification

There is an open request for Spring Security to support this behavior: https://github.com/spring-projects/spring-security/issues/6814






