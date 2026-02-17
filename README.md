# EDMD Token – Full Guide (From Remix to BaseScan)
_A complete beginner-friendly walkthrough for creating, deploying, verifying, and updating a token on the Base network._

This repository explains **step-by-step** how the **EDMD Token** was created and deployed — including verifying the contract and adding the logo + social information on BaseScan.

Everything you see here can be repeated by anyone, even with **zero experience**.

---

# 📌 Token Details.

- **Token Name:** 0xEdmundo  
- **Symbol:** EDMD  
- **Decimals:** 18  
- **Network:** Base  
- **Contract Address:** `0xE776B4771ADBa8E43554DC3b4FA84Ff66c011478`  
- **BaseScan Page:** https://basescan.org/address/0xE776B4771ADBa8E43554DC3b4FA84Ff66c011478  

This README shows:

1. How the contract was written in **Remix**
2. How it was deployed to **Base mainnet**
3. How to verify the contract on **BaseScan**
4. How to upload token **logo**, **website**, **X profile**, **GitHub**, etc.

---

# 1️⃣ Writing the Contract in Remix

## ✔ Step 1 – Open Remix  
Go to: https://remix.ethereum.org

## ✔ Step 2 – Create the contract file  
Left sidebar → **File Explorer** → “New File” → name it:

```
EdmundoToken.sol
```

## ✔ Step 3 – Paste the token code below

This is a simple ERC-20 style contract with a fixed supply of **10 billion EDMD**, exactly like the real deployment.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EdmundoToken {
    string public name = "0xEdmundo";
    string public symbol = "EDMD";
    uint8 public decimals = 18;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    constructor() {
        uint256 initialSupply = 10_000_000_000 * 10 ** uint256(decimals);
        totalSupply = initialSupply;
        balanceOf[msg.sender] = initialSupply;
        emit Transfer(address(0), msg.sender, initialSupply);
    }

    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(_to != address(0), "Invalid address");
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");

        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
        emit Transfer(msg.sender, _to, _value);
        return true;
    }

    function approve(address _spender, uint256 _value) public returns (bool success) {
        allowance[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
        require(_to != address(0), "Invalid address");
        require(balanceOf[_from] >= _value, "Insufficient balance");
        require(allowance[_from][msg.sender] >= _value, "Allowance exceeded");

        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
        allowance[_from][msg.sender] -= _value;
        emit Transfer(_from, _to, _value);
        return true;
    }
}
```

## ✔ Step 4 – Compile  
Left sidebar → **Solidity Compiler** →  
- Version: **0.8.20**  
- Click **Compile EdmundoToken.sol**

---

# 2️⃣ Deploying the Contract to Base Mainnet

## ✔ Step 1 – Ensure Base Network is in MetaMask  
If not, add:

- **Network Name:** Base  
- **Chain ID:** 8453  
- **Explorer:** https://basescan.org  

## ✔ Step 2 – Connect Remix to Wallet  
Left sidebar → **Deploy & Run Transactions**  
- Environment: `Injected Provider – MetaMask`  
- Wallet must be on **Base Mainnet**

## ✔ Step 3 – Deploy  
Constructor takes no parameters.  
Click **Deploy**, sign the transaction.

The deployed EDMD token address:

```
0xE776B4771ADBa8E43554DC3b4FA84Ff66c011478
```

---

# 3️⃣ Verifying the Contract on BaseScan

## ✔ Step 1 – Open BaseScan  
Search your contract:

https://basescan.org/address/0xE776B4771ADBa8E43554DC3b4FA84Ff66c011478

Go to **Contract** tab → click **Verify and Publish**.

## ✔ Step 2 – Fill required fields
- Compiler Type: **Solidity – Single file**
- Compiler Version: **0.8.20**
- License: **MIT**

Paste the exact contract code (same as deployed).

Submit → wait → BaseScan shows **green verified badge**.

---

# 4️⃣ Adding Token Logo & Socials

Once verified, open your token page on BaseScan.

Click:

```
Update Token Info
```

Upload or link:

- Logo  
- Website  
- X (Twitter)  
- GitHub repo (this one)  
- Telegram / Discord  
- Description  

### ✔ Tip  
You can upload your logo to GitHub and use the **raw file URL**.

Example Token name etc. edit as per your own

```
https://raw.githubusercontent.com/0xEdmundo/edmd-token/main/assets/edmd-logo-32x32.png
```

---

# 5️⃣ (Optional) Hosting Token Logo in This Repo

1. Create folder:  
   `assets/`
2. Upload logo file  
3. Click logo → “View raw” → copy URL  
4. Use in BaseScan / wallets

---

# 6️⃣ Full Flow Summary

1. Write contract in Remix  
2. Compile  
3. Deploy to Base  
4. Verify contract on BaseScan  
5. Add logo + socials  
6. Host logo in repo if needed  

Your EDMD token is now:

- Fully deployed  
- Fully verified  
- Fully branded  
- Fully documented  

---

# 🎉 Done  

This README contains everything needed for someone to repeat the entire EDMD token creation + deployment + verification process.

If you'd like, I can generate:  
- A logo  
- A better repo banner  
- JSON metadata for CMC/CG listings  
- Airdrop scripts  
- Token distribution docs  

Just tell me!
