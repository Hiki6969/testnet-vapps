# vApp Submission: **zkBeacon Fair Draw**

## Verification
```yaml
github_username: "Hiki6969"
discord_id: "864532768201769041"
timestamp: "2025-08-23"
```

## Developer
- **Name**: Hiki Komori
- **GitHub**: @Hiki6969
- **Discord**: hikikomori6969
- **Experience**: Early-stage Web3 developer exploring zero-knowledge proofs and the Soundness ecosystem. 

## Project

### Name & Category
- **Project**: zkBeacon Fair Draw  
- **Category**: Social  

### Description
**Problem**: Traditional online lotteries or draws rely heavily on trusting the organizer’s code execution or random number generator. This creates opportunities for manipulation, lack of transparency, and loss of user trust.  

**Solution**: zkBeacon Fair Draw introduces a **verifiable, zero-knowledge powered draw system**. Winners are selected deterministically using a mix of a secret seed and an unpredictable public randomness beacon (e.g., drand).  
- Zero-knowledge proofs guarantee that winners are computed correctly.  
- Participants and observers can independently verify fairness through published proofs and attestations.  
- Personal data and the organizer’s private seed remain confidential.  

### SL Integration  
zkBeacon Fair Draw leverages the **Soundness Layer** to:  
- Verify zk proofs that winners were computed correctly from `{secret, public_beacon, participant_list}`.  
- Store and verify artifacts (participant list hash, proof, public inputs) using SL validators.  
- Issue decentralized attestations confirming the fairness of each draw.  

Key SL features:  
- **Proof-agnostic verification** (supporting SNARKs/STARKs depending on prover).  
- **Blob storage integration with Walrus** for participants and proofs.  
- **Attestation IDs** for traceability and independent verification.  

## Technical  

### Architecture  
1. Organizer commits to a participant list and private seed.  
2. After registration closes, an unpredictable beacon (e.g., drand output) is published.  
3. A zk prover calculates the winner indices using the formula:   index_i = SHA256(secret || beacon || i) mod N
with rejection sampling to avoid duplicates.  
4. Proof and public inputs are uploaded to Walrus.  
5. Soundness Layer verifies the zk proof and issues an attestation ID.  
6. Frontend displays winners along with verifiable proof artifacts.  

### Stack  
- **Frontend**: React + Vite  
- **Backend/Prover**: Rust (SP1 zkVM with Groth16 BN254 export)  
- **Blockchain / Verification**: Soundness Layer  
- **Storage**: Walrus (proofs, inputs, participant CSV), IPFS (optional backup)  

### Features  
1. Transparent winner selection using public randomness  
2. zk-proof based verification of results  
3. Decentralized attestation for trustless validation  

## Timeline  

### PoC (2–4 weeks)  
- Prototype the draw algorithm inside SP1 zkVM (hash → mod → uniqueness check).  
- Produce initial zk proofs and run verification through local tooling.  
- Store early artifacts (proof + participant commitments) in Walrus.  
- Connect output to Soundness Layer for a first attestation.  
- Deliver a bare-bones results page to showcase proof + winners.  

### MVP (4–8 weeks)  
- Introduce participant explorer: map indices back to entries in the committed list.  
- Wrap the proving + upload process into a one-step organizer command.  
- Enrich developer docs with flow diagrams and sample runs.  
- Run a small closed test with mock participants to validate end-to-end flow.  


## Innovation  
zkBeacon Fair Draw combines **commit–reveal** with **public randomness** and zero-knowledge verification, eliminating trust in the organizer’s execution environment.  
- Proofs are validator-verified and stored permanently.  
- Results are reproducible, censorship-resistant, and bias-free.  
- Unlike typical online giveaways, it guarantees transparency and auditability through cryptography.  

## Contact  
- **Discord**: @hikikomori6969  
- **Email**: 3rdgenerationgodeaterjulius@gmail.com 
