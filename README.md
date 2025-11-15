# Vault Exploit — ICE_404 Breach

## Overview
This exploit demonstrates a full breach of the Vault contract using a hijacked locker callback. The test confirms callback control, drain flow via `settleFor()`, and ownership transfer using `Ownable2Step` mechanics.

## Exploit Flow
1. Deploy `Vault` and `MaliciousLocker`
2. Patch locker slot manually using `vm.store()`
3. Transfer ownership to locker and accept it
4. Trigger `lock()` from locker
5. Callback fires: `settleFor()` drains funds, `transferOwnership()` sets `pendingOwner`
6. Attacker accepts ownership

## Key Contracts
- `Vault.sol` — target contract  
- `MaliciousLocker.sol` — hijacked callback logic  
- `VaultExploit.t.sol` — full exploit test

## Reproducibility Ritual
- Solc version: `0.8.26`  
- `forge-std` used for logging and testing  
- `vm.store()` used to patch locker slot  
- `vm.prank()` used to simulate attacker claim

## Logs
- Callback triggered  
- Settle succeeded  
- Ownership transferred
