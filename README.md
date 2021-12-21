# HARDHAT_TESTNET

Use HARDHAT as a REUSABLE TESTNET.

## zero to crypto...

With OpenZeppelin Smart Contracts.
- Unit Tests - from OpenZeppelin
- Private Testnet - Hardhat Network
- Rinkaby, Robsten, Mumbai.
## OPENZEPPELIN STUDY LINKS 
Smart Contract Development Best Practices.
- derived from https://docs.openzeppelin.com/learn/
- and https://wizard.openzeppelin.com
- also HARDHAT: https://hardhat.org/getting-started/
### INDEX (below): 
1) QUICK START (existing PROJECT), 
2) CREATE NEW (CRYPTO-PROJECT, HARDHAT scaffold),
3) ERC721 Standard Review
- ADVANCED ASSERTIONS
----
### QUICK START (existing project): 
- compile, ganache, migrate, exec, test,
```JavaScript
> npm install
> npx hardhat compile
> npx hardhat node
> npx hardhat test
```
----
## CREATE NEW (CRYPTO-PROJECT, HARDHAT scaffold)
### 1) Build a SCAFFOLD:
```JavaScript
> mkdir PROJECTS/CRYPTO/EXAMPLE && cd PROJECTS/CRYPTO/EXAMPLE
> npm init -y
> code .
> create README.md
> create ./scripts
> npm install --save-dev hardhat
> npx hardhat    //creates config
> npx hardhat compile
> npx hardhat node    //Hardhat Network, similar to ganache
> npx hardhat run scripts/sample-script.js --network localhost
```
- expose JSON-RPC interface. 
- Connect wallet or app to http://localhost:8545.
### HARDHAT
- Hardhat Network, uses @ethereumjs/vm
- Hardhat Runner, extensible TASK RUNNER
- tasks and plugins, tasks call tasks.

- Hardhat uses /scripts to DEPLOY
`> npm install --save-dev @nomiclabs/hardhat-ethers ethers`
RESULT:
crypto project ready to rock,
with /contracts, /scripts,
/migrations, and /test. 
`> git init`
GitHub with LICENSE MIT
```JavaScript
> git remote paste.git
> git push, git pull.
> create s3cr3tz.json
.gitignore s3cr3tz.json
```
-----
### 2) SOLIDITY PROJECT!
`> npm install --save-dev truffle`
- Truffle or Hardhat. 
- Truffle uses Web3.js. Hardhat uses ethers.js
- Platforms for compile and migrate 
- (to various TEST NETS)
- Like Ganache (local) or Rinkeby, public.
-----
### 3) CONTRACTS!!
`> create /contracts/BASIC_721_oz.sol`
- go to Open Zeppelin Wizard to get code.
- compile SOL into BYTECODE for EVM
- configure truffle-config to use solc compiler.
- will compile all contracts into 
- /build/contracts/artifacts
`> .gitignore `
artifacts
cache
---
#### HARDHAT NETWORK CONSOLE
```JavaScript
> npx hardhat console --network localhost
> const Box = await ethers.getContractFactory('Box');
> const box = await Box.attach('0x5FbDB2315678afecb367f032d93F642f64180aa3')
```
#### HARDHAT by SCRIPT
```JavaScript
> npx hardhat run --network localhost ./scripts/index.js
> const address = '0x5FbDB2315678afecb367f032d93F642f64180aa3';
> const Box = await ethers.getContractFactory('Box');
> const box = await Box.attach(address); //get address from DEPLOY
```
#### HARDHAT UNIT TESTS
```JavaScript
> npm install --save-dev chai
> npx hardhat test
> npm install --save-dev @openzeppelin/test-helpers
```
-----
### 4) ERC20, ERC721, ERC1155
OpenZeppelin Contract Wizard
https://wizard.openzeppelin.com/
MAX ANNOTATED EXAMPLES in /contracts
```JavaScript
> npm install --save-dev @openzeppelin/contracts
> npx truffle compile
```
----
### 5) DEVNET (testnet local)
- with Ganache-CLI
`> npm install --save-dev ganache-cli`
- DEPLOY / migrate
- DEV by CONSOLE
- TEST RUN by scripts
- No METAMASK
- GR8 for UNIT-TESTS (next)
- RUN GANACHE
`> npx ganache-cli --deterministic`
- configure connection with ganache (geth,parity)
`> create // migrations/2_deploy.js`
- and configure truffle-config
`> networks:development:host:127.0.0.1:8545:*`
- standard ETH PORT 8545
- DEPLOY contracts to DEVELOPMENT NETWORK, on GANACHE:8545
`> npx truffle migrate --network development``
- puts BYTECODE artifacts and ABI to ganache
- if ERROR, update migrate, or restart GANACHE
----
### 6) PROTOTYPE-TEST (local network - truffle CONSOLE)
`> npx truffle console --network development`
- now INIT CONTRACT VARIABLE (charged 0.008 ETH)
`> accounts`

`> const BASIC_oz = await BASIC_oz.deployed();`
- CALL TRANSACTION
`> await BASIC_oz.store(42)`
- GET a RECEIPT BACK (charged 43755)
`> (await BASIC_oz.retrieve()).toString()  //42`
- no receipt, no transaction.
- CMD-LINE-QUERY
----
### 7) SCRIPT-DEV ( /script/js with Web3.js)
- Truffle executes ./scripts
- once deployed, any library sees contract
- in scripts-index:
// const accounts = await web3.eth.getAccounts();
// console.log(accounts)
`> npx truffle exec --network development ./scripts/index.js`
----
### 8) JS instance of CONTRACT ( Web3.js)
- Truffle CONTRACT, as JSON.
// const BASIC_oz = artifacts.require('BASIC_oz');
// const _basic_oz = await BASIC_oz.deployed();
- CALL THE CONTRACT
// const value = await _basic_oz.retrieve();
// console.log('State value is', value.toString());
- CALL TRANSACTION
// await _basic_oz.store(23);
----
### 9) UNIT-TESTS ( chai.js)
`> npm install --save-dev chai`
- /tests mirror /contracts 1 to 1.
`> create test/BASIC_oz.test.js`

`> npx truffle test`

----
### 10) OZ TEST-HELPERS ( complex assertions )
`> npm install --save-dev @openzeppelin/test-helpers`
- EXTRAs like
- veryify revert, exact balances, events emitted, time.
// const { BN, expectEvent, expectRevert } = require('@openzeppelin/test-helpers');
- EXAMPLES: 
- https://github.com/OpenZeppelin/openzeppelin-test-helpers/tree/master/test/src
----
### 11) ERC20, ERC721, ERC1155 ( standards )
## ERC20
----
## ERC721
- MINIMUM interface for SMARTCONTRACTS 
- managed, owned, traded - TOKENS.
- unrestricted functions and metadata(!)
- multiple optional packages.
LINK:https://eips.ethereum.org/EIPS/eip-721
ERC721 is ERC165 - NFT deed w/ unique ID. uint256
```JavaScript
> event Transfer - ownership transfer: created, distroyed
> event Approval - set approved address
> event ApprovalForAll - operator enabled, disabled, management.
> fn balanceOf - num NFTs owned by _owner
> fn ownerOf - _owner address
> fn safeTransferFrom - nft new _owner address confirm receiver.
> fn safeTransferFrom - additional data param
> fn transferFrom - unsafe caller nft ready 'to' assumed.
> fn approve - approved controller address, payable
> fn setApprovalForAll - authorized operators
> fn getApproved - get approved address
> fn isApprovedForAll -is authorized operator?
ERC165, supportsInterface - wallet interface, safe trans
> ERC721TokenReceiver - after transfer receipt, allows transfer.
> onERC721Received - receipt hash
*ERC721Metadata (optional) - name and details
> fn name
> fn symbol
> fn tokenURI - ipfs, metadata schema
*ERC721Enumerable (optional)
- incremental and discoverable (full list)
> fn totalSupply - count of nfts tracked
> fn tokenByIndex - enum item
> fn tokenByOwnerIndex - all assigned to _owner
> *ERC721URIStorage (optional)
ERC721 is Context,IERC721,IERC721Metadata
> tokenId - must exist to verify allowed
> fn name
> fn symbol
> fn tokenURI
> fn _baseURI
> fn _safeTransfer - emit transfer event
> fn _exists
> fn _isApprovedOrOwner
> fn _safeMint
> fn _safeMint
> fn _mint
> fn _burn
> fn _transfer
> fn _approve - allows transfer, if not from
> fn _setApprovalForAll
> fn _checkOnERC721Received
> fn _beforeTokenTransfer
```
----
### ERC721-OPENZEPPELIN
LINK: https://docs.openzeppelin.com/contracts/4.x/api/token/erc721
- INTERFACES, CONTRACTS, UTILITIES.
- Unopinion, Opinion: ERC721PresetMinterPauserAutoId
```JavaScript
> IERC721 - required to be ERC721 compliant.
> IERC721Metadata *
> IERC721Enumerable *
> IERC721Receiver - prevent locked tokens (verify receiver)
> ERC721Pausable - pause transfer
> ERC721Burnable - destroy
#### CORE IERC721
> event Transfer
> event Approval
> event ApprovalForAll
> fn balanceOf(owner), fn ownerOf(tokenId)
> fn safeTransferFrom(data), fn transferFrom
> fn approve - owner or operator
> fn getApproved - emits Approval Event 
> fn setApprovalForAll, operator transfer
> fn isApprovedForAll, is operator allowed.
#### IERC165 - supportsInterface
#### IERC721Metadata
> name, symbol, tokenURI
#### IERC721Enumerable
> totalSupply - total tokens
> tokenOfOwnerByIndex - tokenId by _owner at index
- use with balanceOf to enumerate all of owners tokens
- TODO similar mechanism to enumerate all creator tokens
> tokenByIndex - tokenID at Index
- use with totalSupply to enum all tokens.
## ERC721
constructor(name_, symbol_)
supportsInterface(interfaceId)
balanceOf(owner)
ownerOf(tokenId)
name()
symbol()
tokenURI(tokenId)
_baseURI()
approve(to, tokenId)
getApproved(tokenId)
setApprovalForAll(operator, approved)
isApprovedForAll(owner, operator)
transferFrom(from, to, tokenId)
safeTransferFrom(from, to, tokenId)
safeTransferFrom(from, to, tokenId, _data)
_safeTransfer(from, to, tokenId, _data)
> _exists(tokenId) - tokenId exists? mint, exist, burn.
> _isApprovedOrOwner(spender, tokenId) - spender allowed?
> _safeMint(to, tokenId) - must be receiver
_safeMint(to, tokenId, _data)
> _mint(to, tokenId) - unsafe use _safeMint
_burn(tokenId)
_transfer(from, to, tokenId)
_approve(to, tokenId)
_setApprovalForAll(owner, operator, approved)
> _beforeTokenTransfer(from, to, tokenId)
> HOOKS - called before and after (simplifies override)
> hook into original behavior - so far the only one!
- Rules of Hooks
> virtual, always call parent hook using super.
#### ERC721Enumerable 
#### ERC721Receiver
#### ERC721Pausable - freezing all transfers.
> _beforeTokenTransfer - becomes pausible
> event Paused
> event Unpaused
> fn paused, _pause, _unpause
#### ERC721Burnable
#### ERC721URIStorage
> fn tokenURI
> fn setTokenURI
> fn burn
#### ERC721PresetMinterPauserAutoId (opinion)
- Roles with AccessControl
- ROLES: ADMIN_ROLE, MINTER_ROLE, PAUSER_ROLE 
TODO: (CREATOR_ROLE)
- Deployer granted minter and pauser
TODO: look to make this creator role.
- ACCESS CONTROL
> fn getRoleMember
> fn getRoleMemberCount
> fn _grantRole
> fn _revokeRole
> fn hasRole
> fn _checkRole
> events roleChange, RoleGranted, RoleRevoked
### UTILITIES
### ERC721Holder
> fn onERC721Received.
```
----
## ERC1155
----
# CRYPTO-USE-CASES
### ERC721
- UNIQUE TOKENS.
- mint burn
- transfer and track
- sell token: 
- auction, english, dutch
- buy token:
- ownership in wallet
- operators: brokers/auctioneers (consignment)
- Physical, Virtual, Negative

---
## Thank you crypto community.
- contact netcinematics(at)protonmail(dot)com
