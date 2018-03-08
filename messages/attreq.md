# Attestation Request

The Attestation Request is created by a client app and sent to a user's mobile app during the [Attestation request flow](../flows/attestation.md).

The request can be either signed or unsigned.

#### Attributes

The JWT shares these attributes with the [Share Request](sharereq.md): `iss`, `iat`, `exp`.

The following additional attributes of the JWT are supported:

Name | Description | Required
---- | ----------- | --------
`type` | MUST have the value `attReq` | yes
`unsignedClaims` | A list of unsigned claims that the user is requested to sign, in the form of JSON objects that form part of the payload of the attestation. A mandatory field is the `claim` itself, and a common field would be `sub` for the subject. | yes
`sub` | The DID of the identity you want the user to sign the claims with | no
`callbackUrlWhitelist` | (Optional) A list of URLs specifying where the responder is allowed to send the response. | no
`callback` | Callback URL for returning the response to a request (may be deprecated in future) | no
`challenge` | A nonce randomly generated by the requestor.  | no

## Unsigned Requests

To perform an unsigned attestation request append the unsigned claims as URL encoded query parameters to one of the above endpoints and open it. Eg.:

`me.uport:attReq?unsignedClaims=[...]&callback_url=https://mysite.com/callback&label=My%20Site`

The following additional parameters are supported:

Name | Description | Required
---- | ----------- | --------
`callback_url` | The URL that receives the response | yes
`callback_type` | Valid values `post` or `redirect`. Determines if callback should be sent as a HTTP POST or open the link (`redirect`). If unspecified, the mobile app will attempt to pick the correct one| no
`client_id` | The [MNID](https://github.com/uport-project/mnid) of the requesting identity | no
`label` | Plain text name of client to be displayed to user | no
