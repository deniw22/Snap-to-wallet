# Mobile Devnet Integration Progress

**Status date:** August 7, 2026  
**Environment:** Android physical-device testing + Solana Devnet

This is a public, intentionally limited engineering update. It describes the
modules that have been integrated and physically verified without publishing
application code, APK files, private infrastructure, wallet addresses, keys,
product flows, or unreleased product logic.

## Redacted Physical Test Screens

These screenshots come from a physical Android test run. Personal imagery,
environment details, event artwork and selected branding have been deliberately
blurred. No recovery material, public account address, transaction identifier or
private infrastructure value is shown.

<img src="assets/android-camera-redacted.png" width="360" alt="Redacted Android camera integration test" />

*CameraX running on a physical Android device; the live personal preview is
irreversibly redacted.*

<img src="assets/devnet-demo-redacted.png" width="360" alt="Redacted Devnet visual-only policy test" />

*Visual-only policy test showing a ready local account while explicitly making
no NFT mint claim.*

## Integrated Modules

### Native Android Client

- Portrait-oriented native Android application tested on a physical device.
- Independent build variants allow experimental flows to be tested without
  modifying the baseline application.
- Clean-install, permission, app-link and recovery-state paths are covered.

### Camera And Local Media

- CameraX front-camera capture is integrated.
- Single-photo and short burst modes are supported.
- Local static and animated media artifacts can be created and stored privately
  on the device.
- Personal media is not published automatically.

### Local Cryptographic Initialization

- A media-derived digest is used as one input to a device-local derivation
  pipeline.
- It is combined with Android cryptographic randomness; the media is not the
  sole source of entropy and cannot recover the account by itself.
- SHA-256, HKDF-SHA-256 and BIP-39 are used in the tested derivation path.
- Recovery material is masked by default.

### Secure Storage And Authorization

- Sensitive local state is protected through Android Keystore-backed storage.
- Fingerprint authentication is integrated for protected operations.
- Public account data is separated from recovery and signing material.

### Solana Devnet Integration

- Account generation, balance lookup, transaction signing and Devnet transfer
  verification are working on a physical Android device.
- Transaction results can be checked through the Solana explorer.
- Mainnet is not enabled in the current test package.

### Compressed NFT Pipeline

- A sponsored compressed-NFT path is integrated on Solana Devnet.
- The current test path uses Bubblegum V2-compatible compressed assets.
- Ownership, compression tree, collection and metadata were independently
  verified through DAS after mint confirmation.
- Mint authority and sponsorship credentials remain outside the mobile client.

### Versioned Configuration Packs

- A versioned QR-delivered configuration selects approved visual and execution
  policies.
- Visual demo mode and real Devnet mint mode are explicit, separate policies.
- Demo mode has been physically verified to produce zero mint submissions.
- Devnet mint mode has been physically verified to create exactly one confirmed
  compressed asset for one approved action.

### Media And Asset Surfaces

- Private captured media and confirmed on-chain assets have separate states.
- A local gallery can present static media, animated media and confirmed asset
  records without claiming that demo artwork is an NFT.
- Publication to a shared event feed requires an explicit user action.

## How The Modules Connect

At a high level, the Android client receives a validated configuration, captures
media locally and prepares secure account state. Visual processing can run while
the cryptographic work completes. An on-chain request becomes eligible only
after a public address exists and the active configuration explicitly permits a
Devnet mint. Confirmed blockchain data is then reconciled into the asset and
gallery surfaces.

The same build can therefore run a visual-only test or an approved sponsored
Devnet test without confusing one state with the other.

## Physical Verification Completed

- Camera permission and capture from a clean installation.
- New local account generation and recovery masking.
- Fingerprint-protected operations.
- Solana Devnet balance and transfer flow.
- One sponsored compressed NFT with verified owner and metadata.
- One visual-only run with no mobile mint journal and no server submission.
- Local photo, animated media and gallery presentation.
- QR-selected configuration and policy separation.

## Android Compatibility Fix

A clean-install camera permission failure was traced to an outdated transitive
Android Fragment dependency. The old dependency generated an incompatible
permission request code on the physical test device. The dependency was pinned
to a current compatible release, and the complete QR-to-app camera permission
flow was retested successfully.

## Current Engineering State

The mobile prototype now has verified boundaries between local media,
cryptographic identity, biometric authorization, Solana Devnet transactions,
demo artwork and confirmed compressed assets. Current work remains development
and Devnet-only. Production deployment, public sponsorship infrastructure and
Mainnet activation are intentionally outside this public progress milestone.
