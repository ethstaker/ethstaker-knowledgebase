# Slashing Protection

## Lighthouse Slashing Protection

The Lighthouse validator client includes a mechanism to protect its validators against accidental slashing, known as the slashing protection database. This database records every block and attestation signed by validators, and the validator client uses this information to avoid signing any slashable messages.

[Lighthouse Slashing Protection Documentation ↗](https://lighthouse-book.sigmaprime.io/slashing-protection.html)
