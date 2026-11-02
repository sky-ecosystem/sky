# SKY Token and contract associated

This repository includes 2 smart contracts:

- SKY token
- MkrSky Converter

### SKY token

This is a standard erc20 implementation with regular `permit` functionality + EIP-1271 smart contract signature validation.

### MkrSky

A permissionless converter of `Mkr` to `Sky`.
Upon initialization, an amount of `Sky` equivalent to the total supply of `Mkr` is minted to it.
It is then assumed that further minting of `Mkr` will not happen.
In case the `Sky` amount in the converter later exceeds the `Mkr` supply, governance can use the `burn` function to reduce the `Sky` balance. 
The above can happen for example because of burning of `Mkr` outside of the converters, using the `mkrToSky` path in the old converter, or because of `Sky` donations to the new converter. 

The exchange rate is generally 1:`rate` (value defined as `immutable`), while there is also a configureable fee.
The swap `mkrToSky` function receives `Mkr`, burns it and sends the equivalent amount in `Sky` from the balance, minus the fee.
The accumulated fees can be collected by governance.

### Legacy MkrSky

The legacy MkrSky converter supported bi-directional conversions.
Upon initialization of the new converter, only the `mkrToSky` path will be supported.
It is expected that once the new converter fee becomes non-zero, the `mkrToSky` path in the old converter will also be disabled.

## Audits

Audit reports are hosted on the auditors' public portfolio pages:

| Auditor | Report | Date |
| --- | --- | --- |
| ChainSecurity | [Sky smart contracts](https://www.chainsecurity.com/security-audit/makerdao-sky-smart-contracts/) | 2025-06-06 |
| Cantina | [Sky Protocol Token Conversion Audit](https://cantina.xyz/portfolio/5afcb016-c1e8-4e42-8245-87857f8e1e1a) | 2025-04-17 |
| ChainSecurity | [MakerDAO Sky Deployment Scripts](https://www.chainsecurity.com/security-audit/makerdao-sky-deployment-scripts/) | 2024-09-30 |
| Cantina | [sky](https://cantina.xyz/portfolio/713d3c41-6380-4cac-93d8-bca7b4c8a0eb) | 2024-09-17 |
| Cantina | [ngt](https://cantina.xyz/portfolio/1ea14693-a6ba-4793-9bd0-41d7dd3981ce) | 2023-09-19 |

ChainSecurity reports are cumulative: each portfolio page hosts the latest version of the report, which covers all previously reviewed versions.

### Other reports

The following reports are not available on an auditor portfolio page and are kept in this repository:

- [Sherlock (20240917-Sherlock_MakerDAO_Endgame_Audit_Report.pdf)](./audit/20240917-Sherlock_MakerDAO_Endgame_Audit_Report.pdf)
