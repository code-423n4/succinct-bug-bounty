# SP1 Bug Bounty

| Risk Score |  Payout |
|------------|---------|
| Critical | &#36;10,000 - &#36;150,000 |
| High | &#36;5,000 - &#36;10,000 |
| Medium | &#36;1,000 - &#36;5,000 |
| Low | &#36;250 - &#36;1,000 |

## Background on SP1

### What Is SP1?

SP1 is a zero-knowledge virtual machine (zkVM) which allows developers to prove an execution of arbitrary Rust (or other LLVM-compiled language) programs. This means

- A developer can write a normal Rust code, which is then compiled to an ELF.
- Given the ELF, SP1 sets up a proving key and a verifying key.
- SP1 zkVM generates a proof on the execution of the Rust code using the proving key.
- The verifying key can be used to verify the generated proof.

### How Does It Work?

SP1's CLI tool will compile the Rust program into a RISC-V and generate an ELF. SP1 zkVM is composed of the various ZKP circuits, which prove the behavior of various opcodes of RISC-V. This creates a proof of execution based on STARK. SP1 then utilizes recursive STARKs as well as a STARK to SNARK wrapper to generate a small SNARK proof that can be verified on-chain. This recursion also allows SP1 to break an execution into smaller shards, which makes it possible to prove arbitrarily long program execution. 

### Further Technical Resources & Links

- **SP1 Docs**: Our system documentation, subject to change: [Link](https://docs.succinct.xyz/docs/sp1/introduction)
- **SP1 Memory Argument Docs**: [Link](https://docs.succinct.xyz/assets/files/SP1_Turbo_Memory_Argument-b042ba18b58c4add20a8370f4802f077.pdf)
- **SP1 Security Docs**: Our security model - [Link](https://docs.succinct.xyz/docs/sp1/security/security-model)
- **SP1 Security Advisories**: [Link](https://github.com/succinctlabs/sp1/security/advisories)
- **SP1 Audit Reports**: [Link](https://github.com/succinctlabs/sp1/tree/v6.0.0/audits)
- **Succinct Website**: [Link](https://www.succinct.xyz/)
- **Twitter**: [@SuccinctLabs](https://x.com/SuccinctLabs)
- **Other Links**: [Link](https://linktr.ee/succinctlabs)

# Scope & Severity Criteria

We mainly expect two types of vulnerabilities. 

**Soundness Bugs**: Issues where invalid execution can be proved to be correct.

The severity will be based on how high the impact of the invalid execution can be. 

| Severity level | Impact: High	| Impact: Medium |
|------|-------| -------------- |
| Likelihood: High	 | Critical | High |
| Likelihood: Medium | High | Medium |

**Completeness Bugs**: Issues where valid execution cannot be proved to be correct.

The impact is judged on the impact of the program where the completeness bug occur. The likelihood is judged based on the scenario where the completeness bug occur.

| Severity level | Impact: High	| Impact: Medium |
|------|-------| -------------- |
| Likelihood: High	 | Medium | Low |
| Likelihood: Medium | Low | Low |

For other class of vulnerabilities, the following criteria will be used.
| Severity level | Impact: High	| Impact: Medium | Impact: Low
|------|-------| -------------- |-------------- |
| Likelihood: High	 | Critical | Medium | Low |
| Likelihood: Medium | High | Medium | Low |
| Likelihood: Low    | Medium | Low | N/A |


## Assets in Scope

All reports **must be valid on SP1's latest release commit**, which can be found [here](https://github.com/succinctlabs/sp1/releases). 

**Source**: [SP1](https://github.com/succinctlabs/sp1)

| Name | Folder |
|------|-------|
| sp1-core-executor | github.com/succinctlabs/sp1/tree/v6.0.0/crates/core/executor |
| sp1-core-machine | github.com/succinctlabs/sp1/tree/v6.0.0/crates/core/machine |
| sp1-recursion | github.com/succinctlabs/sp1/tree/v6.0.0/crates/recursion |
| sp1-hypercube | github.com/succinctlabs/sp1/tree/v6.0.0/crates/hypercube |
| sp1-zkvm | github.com/succinctlabs/sp1/tree/v6.0.0/crates/zkvm/entrypoint |
| sp1-lib | github.com/succinctlabs/sp1/tree/v6.0.0/crates/zkvm/lib |
| slop | github.com/succinctlabs/sp1/tree/v6.0.0/slop |


## Out-of-Scope

### Known "Issues"

Bug reports covering previously-discovered bugs are not eligible for a reward within this program. This includes known "issues" that the project is aware of but has consciously decided not to “fix”, necessary code changes, or any implemented operational mitigating procedures that can lessen potential risk. Every issue opened in the repo, closed PRs, previous contests and audits are out of scope.

See our security related documentation for more details.
- [SP1 Security Model](https://docs.succinct.xyz/docs/sp1/security/security-model)
- [Safe Usage of SP1 Precompiles](https://docs.succinct.xyz/docs/sp1/security/safe-precompile-usage)

### Security Model 

Bug reports must be valid within SP1's [security model and program safety requirements](https://docs.succinct.xyz/docs/sp1/security/security-model). In summary, security issues that arise from user program itself rather than from SP1 are out of scope. All proof of concepts of issues must be done on user programs that are safe, which are then compiled with the correct toolchain. More details are in the our documentation linked above. We note that the documentation may be subject to change.

### Previous Audits

Any **previously reported** vulnerabilities mentioned in past audit reports are not eligible for a reward. Also, any vulnerabilities mentioned in the security advisories are not eligible. 

Previous audits can be found in [this link](https://github.com/succinctlabs/sp1/tree/v6.0.0/audits), and security advisories are in [this link](https://github.com/succinctlabs/sp1/security/advisories).


### Specific Types of Issues

**An example of out-of-scope issues are as follows:**

- Informational findings.
- Documentation errors.
- Issues in example or demo applications.
- Issues that take an infeasible amount of computation to exploit.
- Security issues that arise from vulnerable user programs.

# Additional Context

## Disclosure Guideline

All valid reports **must have valid proof of concept** included.

Do not disclose submitted bug reports without a clear consent from Succinct.

## Miscellaneous
Current and former employees and contractors of Succinct are ineligible for bounties.

Reward amounts may be displayed using a dollar sign for simplicity, but the underlying valuation is based on a USD-pegged digital asset such as USDC. Because the displayed figure reflects a USD reference value rather than a fiat currency payment, the final amount delivered in the corresponding token may differ slightly at the time of payout.
