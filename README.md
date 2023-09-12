# Enterprise-Ready SSO Profile for OpenID Connect and SAML

## Authentication Contexts

* MFA Any Two Factors
* MFA Phishing Resistant


## OIDC

### MFA Phishing Resistant

`phr`

* Defined in https://openid.net/specs/openid-connect-eap-acr-values-1_0.html

### MFA Any Two Factors

`urn:okta:loa:2fa:any`


## SAML

### MFA Phishing Resistant

```xml
<samlp:AuthnRequest ...>
  ...
  <samlp:RequestedAuthnContext Comparison='exact'>
    <saml:AuthnContextClassRef>http://idmanagement.gov/ns/assurance/aal/2?phishing_resistant=true</saml:AuthnContextClassRef>
  </samlp:RequestedAuthnContext>
</samlp:AuthnRequest>
```

### MFA Any Two Factors



## Existing acr_values


* Okta (Docs)[https://developer.okta.com/docs/guides/step-up-authentication/main/#predefined-parameter-values]
  * `urn:okta:loa:1fa:any`
  * `urn:okta:loa:1fa:pwd`
  * `urn:okta:loa:2fa:any`
  * `urn:okta:loa:2fa:any:ifpossible`
  * `phr`
  * `phrh`
* NHS (Docs)[https://digital.nhs.uk/services/care-identity-service/applications-and-services/cis2-authentication/guidance-for-developers/detailed-guidance/acr-values#requesting-specific-acr-values]
  * `AAL3_ANY`
  * `AAL3_IOS`
    * `AAL3_IOS` authenticates the user using the NHS Care application
  * `AAL3_FIDO2`
  * `AAL3_N3_SMARTCARD`
  * `AAL1_USERPASS`
* Login.gov (Docs)[https://developers.login.gov/oidc/#request-parameters]
  * `http://idmanagement.gov/ns/assurance/ial/1`
  * `http://idmanagement.gov/ns/assurance/ial/2`
  * `urn:gov:gsa:ac:classes:sp:PasswordProtectedTransport:duo`
  * `http://idmanagement.gov/ns/assurance/aal/2`
  * `http://idmanagement.gov/ns/assurance/aal/2?phishing_resistant=true`
  * `http://idmanagement.gov/ns/assurance/aal/2?hspd12=true`


