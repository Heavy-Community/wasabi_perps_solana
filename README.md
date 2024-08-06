# Wasabi Perps implementation on Solana

# Roadmap
- This document outlines the roadmap and key tasks for our software project over a **six-week** period.

## Week 1
- Initialization of the repository.
- Dig even deeper in the business logic.
- Install the needed dependencies and setup the testing harness for the Solana programs.
- **Base Wasabi Pool**
  - Set up the foundational structure for the Wasabi long and short pools.
  - Implement the core logic of the program.
  - Isolated unit testing to some of the functions of the program.
- **Utils - Monolith program with utils for upgradability**
  - Develop utility functions and programs to ensure upgradability, incorporating several upgradeable programs and helper functions, including:
  - the program that is standardized as multicall aggregator function.
  - The rest of the utility programs will be completed in the second week.
- **WSOL**
  - Implement the WSOL contract.
  - This includes implementing an ERC20-like Token program for the Solana blockchain, which will serve as a blueprint for the WSOL contract.
  - The implementation will follow the one provided by SPL's token programs.

## Week 2
- **Base Wasabi Pool**
  - Apply final touches to the `wasabi_pool.rs` program.
  - Tests implementation.
  - By the end of the week, it should be ready to be inherited from this contract!
- **The rest of the upgradability utils for the pools**
  - Complete remaining utility functions required for pool management. Including:
  - needed functions from the universal upgradeable proxy standard contract.
  - needed functions from the ownable upgradeable contract.

## Week 3
- **Long pool**
  - Start the implementation of the Wasabi long pool program `wasabi_long_pool.rs`.
  - Setup up the dependencies that were implemented for the base contract from the first and second weeks.
  - Implement the core functions for opening, closing, liquidating and claiming positions.
  - Tests implementation.
- **Accounts/**
  - Monolith program `roles_and_upgreadability_management.rs` containing the implementation of roles and upgreadability management.

## Week 4
- **Short pool**
  - Start the implementation of the Wasabi short pool program `wasabi_short_pool.rs`.
  - Setup up the dependencies.(Previously mentioned in week 3 for Long pool).
  - Core functions implementation.
  - Tests implementation.
- **Accounts/**
  - Another monolith program `accounts_monolith.rs`

## Week 5
- **Vault/**
  - Deposit and Withdraw: Develop the deposit functionality to handle SOL deposits, convert to WSOL, and mint shares.
  - Update the total asset value based on interest earned or losses reported by the Wasabi pools.
  - Ensure accurate tracking of assets in the program and implement unit tests.
  - Implement the vault standartization with the help of SPL.

## Week 6
- **Debt/**
  - Implement the functions for computing the maximal principal and maximal intereset
  - Ensure that the maximum leverage and APY are tracked correctly and are in valid bounds.
- **Finalization of Product**
  - Finalize and polish the product.
  - Conduct final testing and prepare for audit.

-----
# Тechnical Stack
- **Anchor**
  - For testing and building efficiently and securely the programs.
- **SPL**
  - Using SPL for compatibility with token standards and for implementing upgradeability functions.
  - Some of the programs will be used for reference implementation.
-----
### Scope and Draft Architecture
```
contracts/
├── pools/
│   ├── wasabi_pool.rs
│   ├── wasabi_long_pool.rs
│   ├── wasabi_short_pool.rs
│   └── utils/
│      ├── hash.rs
│      ├── perp_utils.rs
│      ├── erc4626.rs
│      ├── weth.rs
│      └── monolith_upgradeable.rs // includes several upgradability contracts from openzeppelin + other helper functions from oz
│
└── vault/
│   └── wasabi_vault.rs
│
└── debt/
│   └── debt_controller.rs
│
└── accounts/
│    ├── accounts_monolith.rs
│    └── roles_and_upgreadability_management.rs
```

### The smart contracts that need to be implemented
-----

#### Important Notes:
- Both `wasabi_vault`, `WasabiShortPool`, `WasabiLongPool` and `BaseWasabiPool` inherit the `UUPSUpgradeable` smart contract and since openzeppelin provide the upgradability mechanism out of the box, we will have to implement the few functions on our own.

- `BaseWasabiPool` inherits from the `MulticallUpgradeable` standard contract. Since the `WasabiLongPool_validations.test` and `WasabiLongPool_tradeFlow.test` tests utilize the `multicall` function, we need to implement this contract.

- Additionally, the locations of functions from `PerpUtils`, `Hash`, and the `IWasabiPerps` interface are implementation details that will be addressed during development, and thus will be incorporated into the development process i.e. they will be included but if they will be standalone contracts or part of some other monolith contract will be a subject of discussion.

#### Accounts logic
* AddressProvider, PerpManager & Roles are helper contracts that can be combined in a monolith contract or kept as standalone contracts. It can be further discussed.
