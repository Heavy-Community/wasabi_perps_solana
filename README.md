# Wasabi Perps implementation on Solana

# Roadmap
- This document outlines the roadmap and key tasks for our software project over a **six-week** period.

## Week 1
- Initialization of the repository.
- Dig even deeper in the business logic.
- Install the needed dependencies and setup the testing harness for the Solana programs.
- **Wasabi Pool**
  - Set up the foundational structure for the Wasabi long and short pools.
  - Implement the core logic of the program in `wasabi_pool.rs`.
  - Isolated unit testing to some of the functions of the program.
- **Utils - Monolith program with utils for upgradability**
  - Develop utility functions and programs to ensure upgradability, incorporating several upgradeable programs and helper functions in `monolith_upgradeable.rs`, including:
  - the program that is standardized as multicall aggregator function.
  - The rest of the utility programs will be completed in the second week.
- **WSOL**
  - Implement the WSOL program.
  - This includes implementing an ERC20-like Token program for the Solana blockchain, which will serve as a blueprint for the WSOL program.
  - The implementation blueprint will adhere to the guidelines provided by SPL's token programs.

## Week 2
- **Base Wasabi Pool**
  - Apply final touches to the `wasabi_pool.rs` program.
  - Finish implementation of any left out utility functions.
  - Tests implementation.
  - By the end of the week, it should be ready to be used from the short and long pools!

## Week 3
- **Long pool**
  - Start the implementation of the Wasabi long pool program `wasabi_long_pool.rs`.
  - Setup up the dependencies that were implemented for the `wasabi_pool.rs` program from the first and second weeks.
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
- **Vault/** - `wasabi_vault.rs`
  - Deposit and Withdraw: Develop the deposit functionality to handle SOL deposits, convert to WSOL, and mint shares.
  - Update the total asset value based on interest earned or losses reported by the Wasabi pools.
  - Ensure accurate tracking of assets in the program and implement unit tests.
  - Implement the vault standartization with the help of SPL.

## Week 6
- **Debt/** - `debt_controller.rs`
  - Implement the functions for computing the maximal principal and maximal intereset
  - Ensure that the maximum leverage and APY are tracked correctly and are in valid bounds.
- **Finalization of Product**
  - Finalize and polish the product.
  - Conduct final testing and prepare for audit.

-----
# Тechnical Stack
- **Anchor**
  - Using Anchor, which offers abstractions for common patterns and streamlines program deployment, thus enhancing the overall development process. Additionally, it provides a suitable testing harness for our needs.
- **SPL**
  - Using SPL for compatibility with token standards and for implementing upgradeability functions.
  - Some of the programs will be used for reference implementation.
- **Solana CLI**
  - Solana CLI is used for deploying programs, managing accounts, and interacting with the network from the terminal.
-----
### Scope and Draft Architecture
```
programs/
├── pools/
│   ├── wasabi_pool.rs
│   ├── wasabi_long_pool.rs
│   ├── wasabi_short_pool.rs
│   └── utils/
│      ├── wsol.rs
│      └── monolith_upgradeable.rs
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
