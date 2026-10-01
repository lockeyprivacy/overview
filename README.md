<pre align="center">
██╗      ██████╗  ██████╗██╗  ██╗███████╗██╗   ██╗
██║     ██╔═══██╗██╔════╝██║ ██╔╝██╔════╝╚██╗ ██╔╝
██║     ██║   ██║██║     █████╔╝ █████╗   ╚████╔╝
██║     ██║   ██║██║     ██╔═██╗ ██╔══╝    ╚██╔╝
███████╗╚██████╔╝╚██████╗██║  ██╗███████╗   ██║
╚══════╝ ╚═════╝  ╚═════╝╚═╝  ╚═╝╚══════╝   ╚═╝
</pre>

<p align="center">
  <strong>Privacy infrastructure for onchain activity.</strong>
</p>

<p align="center">
  Private intent. Verifiable execution. Public settlement.
</p>

<p align="center">
  <a href="https://lockeyprivacy.com/">Website</a>
  ·
  <a href="https://lockeyprivacy.com/docs">Documentation</a>
</p>

---

## Overview

**Lockey** is open privacy infrastructure designed to create a controllable privacy boundary between **private intent** and **public settlement**.

Public blockchains are transparent and verifiable by design.

That transparency is useful for settlement, but not every part of an onchain action needs to be publicly exposed.

Information such as:

- balances
- counterparties
- transaction relationships
- execution strategies
- application state
- authorization context
- future transaction intent

may contain information that users or applications prefer to keep private.

Lockey explores an architecture where sensitive activity can remain inside a private execution boundary while the blockchain continues to provide public verification and settlement.

```text
Private Intent
      │
      ▼
Private State
      │
      ▼
Zero-Knowledge Proof
      │
      ▼
Verifiable Execution
      │
      ▼
Public Settlement
```

The goal is not to remove blockchain transparency.

The goal is to expose only what needs to be public.

---

## What Lockey Is Building

Lockey is building a modular privacy layer for Ethereum-compatible environments.

The architecture is centered around:

- shielded assets
- client-side private state
- cryptographic commitments
- zero-knowledge proofs
- private transfers
- viewing authority
- selective disclosure
- public settlement

At its core, Lockey introduces a lifecycle where assets can move between public and private states.

```text
PUBLIC
  │
  ▼
SHIELD
  │
  ▼
PRIVATE STATE
  │
  ├── Private Transfer
  ├── Private Actions
  ├── Private Intent
  └── Selective Disclosure
  │
  ▼
UNSHIELD
  │
  ▼
PUBLIC SETTLEMENT
```

---

# Privacy Lifecycle

## Shield

Assets begin in public blockchain state.

A user can move supported assets into the Lockey privacy boundary.

```text
Public Balance
      │
      ▼
    Shield
      │
      ▼
Private Balance
```

The blockchain records the required public state transition while the resulting private state is represented inside the privacy system.

Shielding forms the entry point between the public blockchain and private state.

---

## Private State

Inside Lockey, ownership does not need to be represented only as a directly readable public balance.

Private ownership can instead be represented through cryptographic state such as:

- commitments
- encrypted notes
- nullifiers
- private keys
- local wallet state
- zero-knowledge proofs

Conceptually:

```text
┌─────────────────────────────────────┐
│                                     │
│            PRIVATE STATE            │
│                                     │
│   Balance                           │
│   Ownership                         │
│   Transaction Intent                │
│   Transfer Relationships            │
│   Authorization                     │
│   Application State                 │
│                                     │
└─────────────────────────────────────┘
```

The objective is to minimize unnecessary public exposure while preserving verifiability.

---

## Private Transfer

Assets inside the privacy boundary can move between private states.

```text
Wallet A
Private State
     │
     │
     │ Private Transfer
     ▼
Wallet B
Private State
```

Instead of publishing every underlying relationship directly onchain, the protocol can verify that the requested state transition is valid.

A zero-knowledge proof can demonstrate properties such as:

```text
Valid Ownership
      +
Valid Balance
      +
Valid Authorization
      +
No Double Spend
      │
      ▼
  Valid Proof
```

without necessarily exposing all of the underlying private state.

---

## Unshield

Users can move assets from private state back into public blockchain state.

```text
Private State
      │
      ▼
   Unshield
      │
      ▼
Public Address
```

Unshielding creates the exit boundary between private execution and public settlement.

The resulting public asset can then interact with the wider onchain ecosystem.

---

## Selective Disclosure

Privacy should not have to be all-or-nothing.

Lockey is exploring a separation between:

```text
                    PRIVATE STATE
                          │
               ┌──────────┴──────────┐
               │                     │
               ▼                     ▼

          Spending Key           Viewing Key
               │                     │
               ▼                     ▼

         Control Assets        Inspect State
                               No Spend Access
```

A viewing authority can potentially allow specific information to be inspected without granting permission to spend the underlying assets.

This model can support use cases such as:

- auditing
- accounting
- compliance workflows
- application permissions
- proof of funds
- delegated viewing
- user-controlled disclosure

The user remains in control of what information is revealed and to whom.

---

# Architecture

At a high level, Lockey separates **private state** from **public verification**.

```text
                         LOCKEY

┌───────────────────────────────────────────────────────┐
│                                                       │
│                     CLIENT SIDE                       │
│                                                       │
│  Private Keys                                         │
│  Private State                                        │
│  Commitments                                          │
│  Transaction Construction                             │
│  Proof Generation                                     │
│                                                       │
└──────────────────────────┬────────────────────────────┘
                           │
                           │
                           │ ZK Proof
                           │
                           ▼
┌───────────────────────────────────────────────────────┐
│                                                       │
│                    PUBLIC CHAIN                       │
│                                                       │
│  Proof Verification                                   │
│  Commitment Roots                                     │
│  Nullifier Validation                                 │
│  Contract State                                       │
│  Settlement                                           │
│                                                       │
└───────────────────────────────────────────────────────┘
```

Where possible, sensitive operations can occur client-side.

The blockchain remains responsible for publicly verifiable protocol state and settlement.

---

# Public vs Private State

Lockey treats privacy as a boundary rather than a separate world.

```text
                     PUBLIC

             Wallet / Application
                       │
                       ▼
                    Shield
                       │
                       ▼

              ┌─────────────────┐
              │                 │
              │  PRIVATE STATE  │
              │                 │
              │  Balance        │
              │  Ownership      │
              │  Intent         │
              │  Authorization  │
              │                 │
              └─────────────────┘

                       │
                       ▼
                   Unshield
                       │
                       ▼

                     PUBLIC

                    Settlement
```

The system can therefore move between public and private execution contexts depending on what the user needs.

---

# Zero-Knowledge Verification

Privacy does not mean removing verification.

Lockey is designed around cryptographic verification where a user can prove that a state transition is valid without necessarily revealing the information used to generate that proof.

```text
Private Information
        │
        │
        ▼
┌──────────────────┐
│ Proof Generation │
└────────┬─────────┘
         │
         ▼
    ZK Proof
         │
         ▼
┌──────────────────┐
│ Public Verifier  │
└────────┬─────────┘
         │
         ▼
 Valid / Invalid
```

This separation allows:

```text
PRIVATE DATA
     │
     ▼
VERIFIABLE PROOF
     │
     ▼
PUBLIC VERIFICATION
```

---

# Core Principles

## Privacy Should Be a State

Privacy should not require permanently leaving the onchain environment.

Assets should be able to move between:

```text
PUBLIC STATE
     ↕
PRIVATE STATE
```

depending on the action being performed.

---

## Verification Should Remain Public

Private execution should remain verifiable.

A privacy system should not require users to blindly trust an intermediary to determine whether a state transition is legitimate.

Cryptographic proofs provide a mechanism for separating:

```text
What happened
```

from:

```text
Everything required to produce it
```

---

## Disclosure Should Be Selective

Different actors may require different levels of visibility.

A user should be able to expose specific information without revealing their complete private state.

```text
Private State
     │
     ├── Keep Private
     │
     ├── Reveal Specific State
     │
     └── Provide Viewing Authority
```

---

## Settlement Should Remain Composable

Private systems should still be able to interact with public blockchain infrastructure.

Lockey therefore treats public settlement as part of the architecture rather than something that needs to disappear.

```text
Private Execution
       │
       ▼
Public Settlement
       │
       ▼
Onchain Ecosystem
```

---

# Current Focus

Current development focuses on validating the fundamental privacy lifecycle.

```text
Shield
  │
  ▼
Private State
  │
  ▼
Private Transfer
  │
  ▼
Unshield
  │
  ▼
Selective Disclosure
```

The project is currently experimental infrastructure.

Contracts, proof systems, interfaces, SDKs, relayers, and protocol architecture may change during development.

Experimental deployments should not be considered production-ready unless explicitly stated otherwise.

---

# Core Modules

Lockey is being developed as modular privacy infrastructure.

## Private ETH

A private state lifecycle for ETH.

```text
ETH
 │
 ▼
Shield
 │
 ▼
Private ETH
 │
 ├── Transfer
 │
 └── Private Actions
 │
 ▼
Unshield
 │
 ▼
ETH
```

---

## Private Transfer

Transfer assets between participants inside the privacy boundary.

```text
Private Wallet A
       │
       ▼
   ZK Transfer
       │
       ▼
Private Wallet B
```

---

## Viewing Authority

Separate visibility from spending authority.

```text
Private Account
      │
      ├──────── Spending Authority
      │
      └──────── Viewing Authority
```

---

## Selective Disclosure

Allow users to reveal specific private information when necessary.

```text
Private State
      │
      ▼
Disclosure Permission
      │
      ▼
Selected Information
```

---

# Extended Modules

Additional areas being explored include:

- Multi-Asset Privacy
- Private NFTs
- Private Swaps
- Private Staking
- Private Lending
- Private Gas
- Private Application State
- Private Intent
- Agent Authorization
- Private Autonomous Execution
- Interoperability with other privacy systems

Not every module is currently implemented.

Repository documentation and deployed contract information should be treated as the source of truth for implementation status.

---

# Private Intent

Lockey's direction extends beyond private transfers.

A privacy boundary can also protect transaction intent before execution.

Instead of publishing the complete intended action before it is executed, a user or autonomous system can construct the intent privately.

```text
USER / AGENT
      │
      ▼
Private Intent
      │
      ▼
Private Authorization
      │
      ▼
Proof Generation
      │
      ▼
Verifiable Execution
      │
      ▼
Public Settlement
```

This architecture creates a foundation for applications where an action can remain private while the resulting state transition remains publicly verifiable.

---

# Agent Authorization

As autonomous agents become capable of interacting directly with blockchain infrastructure, privacy also becomes relevant to authorization.

An agent may need permission to perform a specific action without receiving unrestricted access to all user state.

Conceptually:

```text
User
 │
 ▼
Private Authorization
 │
 ▼
Agent
 │
 ▼
Restricted Intent
 │
 ▼
Proof
 │
 ▼
Execution
```

Potential authorization constraints could include:

- specific assets
- specific actions
- spending limits
- expiration
- destination rules
- application scope
- disclosure permissions

This area remains exploratory.

---

# Verifiable Execution

Lockey does not treat privacy and verification as opposing ideas.

The architecture is based on separating sensitive information from the information required to validate an action.

```text
              PRIVATE

        Intent
        State
        Ownership
        Authorization
        Relationships
        Strategy

              │
              │
              │ ZK Proof
              ▼

            VERIFIABLE

        Valid State Transition
        Valid Authorization
        Protocol Rules
        No Double Spend

              │
              ▼

              PUBLIC

        Blockchain State
        Proof Verification
        Final Settlement
```

This leads to the broader Lockey model:

```text
PRIVATE INTENT
      │
      ▼
VERIFIABLE EXECUTION
      │
      ▼
PUBLIC SETTLEMENT
```

---

# Long-Term Direction

Lockey's long-term objective is to become a general privacy execution layer for onchain applications.

The privacy boundary can potentially extend beyond simple transfers toward:

- private payments
- private asset management
- private DeFi interactions
- private application state
- private transaction intent
- viewing authority
- selective disclosure
- private autonomous agents
- agent authorization
- verifiable autonomous execution

The objective is simple:

> **Keep intent private while keeping outcomes verifiable.**

---

# Example Protocol Flow

```text
┌──────────────┐
│ Public Wallet│
└──────┬───────┘
       │
       │ Shield
       ▼
┌───────────────────────────┐
│                           │
│       PRIVATE STATE       │
│                           │
│  commitments              │
│  encrypted notes          │
│  ownership                │
│  balances                 │
│  authorization            │
│                           │
└────────────┬──────────────┘
             │
             │
       ┌─────┴─────┐
       │           │
       ▼           ▼
   Transfer      Action
       │           │
       └─────┬─────┘
             │
             ▼
       ZK Proof Generation
             │
             ▼
       Public Verification
             │
             ▼
         Settlement
```

---

# Repository Structure

Depending on the repository, a Lockey implementation may contain components such as:

```text
lockey/
│
├── contracts/
│   ├── pool/
│   ├── verifier/
│   ├── commitments/
│   ├── nullifiers/
│   └── disclosure/
│
├── circuits/
│   ├── shield/
│   ├── transfer/
│   ├── unshield/
│   └── disclosure/
│
├── sdk/
│   ├── wallet/
│   ├── state/
│   ├── proofs/
│   └── transactions/
│
├── relayer/
│
├── app/
│
├── scripts/
│
├── test/
│
└── docs/
```

The exact architecture can differ between Lockey repositories.

---

# Development Status

Lockey is under active development.

Expect:

```text
Experimental Contracts
        │
Experimental Circuits
        │
Changing Interfaces
        │
Test Deployments
        │
Protocol Iteration
        │
Security Review
        │
        ▼
Production Readiness
```

Current implementations should be treated as experimental unless a release explicitly states otherwise.

---

# Security

Privacy infrastructure introduces significant cryptographic and implementation risk.

Before production usage, relevant components should undergo:

- smart contract review
- zero-knowledge circuit review
- cryptographic review
- threat modeling
- fuzz testing
- integration testing
- adversarial testing
- independent security audits

Do not use experimental deployments with assets you cannot afford to lose.

If you discover a potential security vulnerability, avoid publishing exploit details publicly before maintainers have had an opportunity to investigate.

---

# Contributing

Lockey is being developed as open infrastructure.

Contributions are welcome across areas including:

- zero-knowledge systems
- smart contracts
- privacy protocols
- client-side cryptography
- wallet architecture
- relayer infrastructure
- selective disclosure
- developer tooling
- security research
- privacy UX
- documentation

Contribution guidelines can evolve together with the protocol.

---

# Philosophy

Public blockchains make global settlement verifiable.

Lockey explores how that settlement layer can coexist with user-controlled privacy.

```text
TRANSPARENCY
does not require
TOTAL EXPOSURE

PRIVACY
does not require
UNVERIFIABLE EXECUTION
```

Instead:

```text
Private Intent
      +
Cryptographic Proof
      +
Public Verification
      =
Verifiable Privacy
```

---

# Resources

**Website**

https://lockeyprivacy.com/

**Documentation**

https://lockeyprivacy.com/docs

**Playground**

Available through the Lockey website.

---

<pre align="center">
PRIVATE INTENT
      │
      ▼
VERIFIABLE EXECUTION
      │
      ▼
PUBLIC SETTLEMENT
</pre>

<p align="center">
  <strong>Build privately. Settle openly.</strong>
</p>
