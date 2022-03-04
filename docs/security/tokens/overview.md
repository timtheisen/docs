Token Authentication Overview
=============================



How to Tell When Incoming Jobs Are Using Tokens
-----------------------------------------------

If an incoming (pre-routed) pilot on a CE has a token, it will have the following classad attributes:

| Attribute        | Meaning                             |
|------------------|-------------------------------------|
| AuthTokenId      | A UUID of the token                 |
| AuthTokenIssuer  | The URL of the issuer of the token  |
| AuthTokenScopes  | Any scope restrictions on the token |
| AuthTokenSubject | The 'sub' field of the token        |

(A pre-routed job is a job without `RoutedJob=True` in its classad.)

!!! note
    A job may have both a token and an X.509 proxy.
    Presence of any `x509*` attributes does not indicate the absence of a token.

To see which authentication method was used for a job:
-   Examine the `/var/log/condor-ce/AuditLog*` files.
-   Find a line saying `Submitting new job <JOBID>` (where `<JOBID>` is a job ID like `21249.0`).
    The line before that should say what authentication method was used.
    -   Authentication via a token will say `AuthMethod=SCITOKENS`.
    -   Authentication via a proxy will say `AuthMethod=GSI`.


VOs Supporting Token Authentication for Pilot Submission
--------------------------------------------------------

These are the VOs that support or partially support using tokens for pilot submission:

| VO Name | Testing Tokens | Using Tokens in Production |
|:--------|----------------|----------------------------|
| ATLAS   | Yes            | No                         |
| EIC     | Yes            | No                         |
| CMS     | Yes            | No                         |
| CLAS12  | Yes            | No                         |
| GLOW    | Yes            | Yes                        |
| GlueX   | Yes            | No                         |
| IceCube | Yes            | No                         |
| LIGO    | Yes            | No                         |
| OSG     | Yes            | Yes                        |

Until all of the VOs you support are using tokens in production, your CE should remain on OSG 3.5,
with the 3.5-upcoming repositories enabled.
