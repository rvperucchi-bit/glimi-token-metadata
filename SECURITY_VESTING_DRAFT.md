# GLIMI ($GLMI) | Security, Custody & Vesting 1.0

**STATUS: PUBLIC TECHNICAL DRAFT — NOT IMPLEMENTED — NO TRANSACTIONS EXECUTED**  
**Date: 16 October 2026**  
**Scope: hypothetical future Solana Mainnet launch.**  
**Related document:** [Tokenomics 1.0 draft](TOKENOMICS_DRAFT.md)

> These are proposed controls, not deployed contracts or guaranteed protections. The GLIMI Devnet token is a non-financial test artifact and remains unchanged. No Mainnet token, funded liquidity pool, vesting contract, or multisig vault is claimed to exist.

## 1. Design goals

- Keep the proposed **1,000,000,000 GLMI** total supply accountable and, after verified issuance, revoke Mint Authority and (subject to review) Freeze Authority on Mainnet.
- Prevent founder allocations from becoming liquid earlier than a publicly disclosed schedule.
- Avoid a single operational wallet controlling the treasury and partnership budgets.
- Make relevant vault and escrow addresses, authority status, token balances, release terms, and any changes publicly verifiable.
- Avoid hidden discretionary overrides, misleading claims of locked liquidity, or early-transfer privileges.
- Budget **R$0 for this research phase**. Mainnet implementation will require real SOL for fees/rent and potentially provider charges; no transaction is authorized yet.

## 2. Proposed founder vesting: 50,000,000 GLMI (5%)

| Property | Proposed rule |
| --- | --- |
| Allocation | 50,000,000 GLMI |
| Start date (T0) | Defined and disclosed before Mainnet issuance and escrow funding. No date has been set. |
| Initial unlocked allocation | 0 GLMI |
| First 12 months | 0 GLMI claimable, including at the cliff unless separately disclosed |
| Next 24 months | 24 periodic releases, intended as equal as possible within 6 decimal places |
| At end of month 36 | 50,000,000 GLMI claimable in aggregate |
| Early cancellation by sender | **Disabled** (subject to protocol verification) |
| Early cancellation by recipient | **Disabled** (subject to protocol verification) |
| Recipient reassignment | Neither party may unilaterally redirect (subject to recovery design and protocol verification) |
| Sale/transfer of vesting claim | Prefer disabled where supported |
| Auto-claim | Not required; assess manual claim to avoid optional automation fees |
| Hosting / contract | Streamflow is a candidate, **not yet chosen or audited specifically for GLIMI** |

**Exact arithmetic:** With six decimals, each of the first 23 monthly tranches can be 2,083,333.333333 GLMI; the final tranche would be 2,083,333.333341 GLMI (an eight-unit adjustment at 10^-6 GLMI). The contract must reproduce the intended schedule; do not assume an on-chain "month" is a calendar month. Streamflow documentation currently describes a month as 30.4 days for its interface. Final release timestamps must be reviewed and displayed publicly.

**Critical vesting nuance:** Streamflow distinguishes cliff releases (sometimes a portion unlocked at a cliff) from an initial allocation. The intended GLIMI policy is **zero** claimable during the initial 12 months and only then progressive release. Before funding, verify this exact result in the contract review chart and decoded on-chain parameters. A 12-month label alone is insufficient.

**Security limitation:** Vendors may offer separate cancelability, recipient-transfer, top-up, or administrative controls. Independently inspect and test them. Marketing claims about audits are not equivalent to an independent GLIMI security assessment.

## 3. Proposed treasury custody: 100,000,000 GLMI (10%)

- Candidate: **Squads** multisig vault with **2-of-3 approvals**, three separately controlled signers and secure offline backup strategies.
- A multisig is an **authorization requirement**, not a time lock. The two authorized signers can move funds immediately unless additional explicit restrictions are deployed. Never advertise treasury holdings as time-locked solely because they are in a multisig.
- Consider internal allocation limits and public expense records before first treasury use.
- Use **Squads Vault address**, never send assets or assign a token authority to the multisig configuration account address.
- The signers, recovery procedure, quorum, upgrade/config authority, and fees must be checked before implementation. If the project has only one trusted operator, do not misrepresent three wallets controlled by that operator as independent governance.
- No signer keys have been generated and no multisig has been deployed.

## 4. Partnerships: 50,000,000 GLMI (5%)

- Hold in a segregated vault with auditable 2-of-3 authorization after multisig readiness.
- Release only against publicly described deliverables, with staged transfers, published recipient addresses (subject to privacy/legal review), and disclosures of promotional consideration.
- A staged release policy written in this document is **not** technically enforced unless future contracts implement it.

## 5. Community: 500,000,000 GLMI (50%)

- Reserve for future community programs. No airdrop, eligibility event, snapshot or entitlement is currently announced.
- Proposal: release progressively across approximately 36 months, with published budgets and anti-abuse conditions.
- Consider a separate verifiable release mechanism before launch. **A community reserve held in a normal wallet or multisig is not inherently locked**.

## 6. Liquidity: 300,000,000 GLMI (30%)

- Keep this as an **unfunded reserve** until a budget exists for the other side of the pool (e.g. USDC/SOL), launch fees and operational costs.
- **Do not confuse:** locking reserved GLMI is not equivalent to locking a liquidity pool's LP ownership tokens or position. Security controls must match the actual DEX/pool design (fungible LP receipts versus concentrated-liquidity positions).
- A liquidity lock may restrict withdrawals but does **not** prevent token price declines, slippage, trading risk, or all forms of rug-pull risk.
- Confirm vesting/locking contract compatibility with the eventual pool and publish verifiable proof if used.
- No pool, LP tokens, price, or liquidity exists on Mainnet at present.

## 7. Launch-security sequence (proposed only)

1. **Agree on policy and budget**, including a legal review for the eventual token offering and operational activities.
2. Choose independent custodians, establish offline key management and test recovery. Avoid reusing the browser-based Devnet keypair for Mainnet treasury.
3. Validate contract versions, support, audit reports, permissions, costs, emergency capabilities and public verifiability.
4. Simulate the vesting schedule with explicit dates and token units; test on Devnet or a local validator **if the actual provider/program supports that environment**.
5. Create the Mainnet mint and issue only the approved supply, once authorized and funded; verify total supply.
6. Fund founder vesting escrow and future reserve vaults; validate that the escrow is funded and cannot release early. Confirm beneficiary, cancellation and transfer rights.
7. Revoke mint/freeze authorities according to the approved policy and verify their absence on-chain.
8. Publish every actual address and contract link, with dated, transparent communication.
9. Only consider a trading pool once it has *real funded liquidity* and a verified liquidity-position management/lock policy.

## 8. Open gates / decisions before execution

- Confirm final beneficiaries and whether genuinely independent 2-of-3 signers exist.
- Pick actual calendar start date and verify how monthly intervals are represented by provider contracts.
- Validate Streamflow contract fees and permissions in its current user interface, especially cancellation, transfer and automatic withdrawal.
- Check Squads deployment charges and program settings at the time of use; neither setup is assumed free on Mainnet.
- Obtain an independent security review and appropriate legal advice before Mainnet implementation.
- Decide liquidity pool type and risk policy only after funding exists.

## 9. Sources / technical references

- Streamflow: [create vesting contract](https://docs.streamflow.finance/en/articles/9670413-create-a-vesting-contract); [cancellation rules](https://docs.streamflow.finance/en/articles/9674831-cancel-contract); [token locks and LP tokens](https://docs.streamflow.finance/en/articles/9339705-token-lock).
- Squads: [create 2-of-3 multisig](https://docs.squads.so/main/getting-started/create-a-squad); [vault versus multisig account caution](https://docs.squads.so/main/navigating-your-squad/settings).
- Solana: [set / revoke token authority](https://solana.com/docs/tokens/basics/set-authority).

---

## Resumo em português

**Decisão em estudo, não implantação:** reservar 50 milhões de GLMI dos fundadores com **12 meses sem saque + 24 liberações mensais**, via contrato auditável, sem cancelamento antecipado. Proteger tesouraria (100 milhões) e parcerias (50 milhões) preferencialmente com **2 de 3 aprovadores realmente independentes**, lembrando que multisig **não cria bloqueio temporal** por si só. Comunidade (500 milhões) terá critérios públicos de distribuição a definir. Liquidez (300 milhões) é **reserva de tokens, não liquidez real**; a futura posição do pool exige política de custódia/bloqueio própria.

**Inalterado:** o token atual na Devnet, com 1 milhão de unidades de teste e o mesmo mint. **Nenhuma transação, chave ou carteira foi criada ou alterada por este documento.** O estudo e a documentação permanecem com orçamento de R$0. Todas as regras definitivas dependem de validações, recursos, decisões e análise jurídica.
