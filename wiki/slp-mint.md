# SLP MINT Transaction

**Summary**: Detailed specification of the SLP MINT transaction, used to increase the supply of an existing token by spending the "minting baton."

**Sources**: mint.md

**Last updated**: 2026-04-18

---

The **MINT Transaction** allows for subsequent increases in the supply of an SLP token. This process is controlled by the possession of the "minting baton"—a specific UTXO established during the [slp-genesis](slp-genesis.md) or a previous MINT transaction (source: mint.md).

## The Minting Baton

The minting baton is the authority to create more tokens. 
- **Requirement**: A valid MINT transaction must include a "baton" input (source: mint.md).
- **Transferability**: If the baton minting authority was transferred to another address, someone other than the original GENESIS issuer can perform a MINT transaction (source: mint.md).
- **Ending Minting**: If the `mint_baton_vout` in a MINT transaction is empty or refers to a nonexistent output, the baton is lost. This proves that no further tokens can be minted, as the baton cannot be duplicated without double-spending the associated BCH output (source: mint.md).

## Transaction Structure

### The OP_RETURN Output (vout=0)
The first output must be an `OP_RETURN` output containing the following data:
1. **Lokad ID**: `'SLP\x00'` (4 bytes).
2. **Token Type**: (1 to 2 byte integer).
3. **Transaction Type**: `'MINT'` (4 bytes).
4. **Token ID**: (32 bytes) The hash of the Genesis transaction.
5. **Mint Baton Vout**: (0 or 1 byte, 0x02-0xff) Specifies which output will receive the baton for future mints.
6. **Additional Token Quantity**: (8 byte integer) The number of new base units being created.

### Other Outputs
- **vout=1**: The receiver of the `additional_token_quantity` of new tokens.
- **vout=M (mint_baton_vout)**: The receiver of the minting baton, allowing for future minting operations (source: mint.md).

## Related pages

- [simple-ledger-protocol](simple-ledger-protocol.md)
- [slp-genesis](slp-genesis.md)
- [transaction](transaction.md)
- [locking-script](locking-script.md)
