# Coris Frontiers public key sets

This repository publishes **public keys only**, as JSON Web Key Sets (JWKS,
RFC 7517), for systems that verify requests signed by Coris Frontiers
software, such as a health system's Epic backend-services app registration.

| File | Verifier | URL |
|---|---|---|
| `uchealth-nonprod.json` | UCHealth Epic, non-production | https://coris-frontiers.github.io/jwks/uchealth-nonprod.json |
| `uchealth-prod.json` | UCHealth Epic, production | https://coris-frontiers.github.io/jwks/uchealth-prod.json |

- The matching private keys are generated on, and never leave, the machine
  that signs the requests. They are never committed here.
- Each key carries a `kid`; every signed request names that `kid` in its
  JWT header, so the verifier picks the right key.
- A file with an empty `keys` list is a placeholder: no key is in use yet.

## Rotating a key

1. Add the new public key to the set next to the old one, and publish.
2. Switch the signer to the new `kid`.
3. Remove the old key once the verifier's cached copy has expired (a day
   is ample), and publish again.

The URLs must stay where they are for as long as a verifier uses them;
moving them means asking that verifier to update its registration.
