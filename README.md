# SmartConract-Assesment-
This Solidity smart contract, named PharmacyInventory, is developed to establish an efficient inventory management system tailored for pharmacies, facilitating seamless tracking and handling of medicine stock on the Ethereum blockchain.

## Description

This contract demonstrates the usage of require(), assert(), and revert() statements for error handling.

### Requirements

- Contract successfully uses require()
- Contract successfully uses assert()
- Contract successfully uses revert() statements

### Component and Functionality

addMedicine: A function that adds a new medicine to the inventory. It takes parameters for the medicine's name, price, and initial stock, and it's accessible only by the owner.

purchaseMedicine: This function allows customers to buy medicine from the inventory. It takes the name of the medicine and the quantity to purchase as parameters. The function checks if the medicine exists and if there is enough stock available. If so, it deducts the purchased quantity from the stock and transfers the payment to the owner.

checkStock: A function that checks the stock of a specific medicine. It takes the name of the medicine as a parameter and returns the current stock level.

medicineCount: A public variable that keeps track of the total number of medicines in the inventory.

medicines: A mapping that stores information about each medicine, including its name, price, and current stock level.

owner: An address variable representing the owner or administrator of the Pharmacy Inventory system.

### Modifiers 

onlyOwner: A modifier that restricts certain functions to be callable only by the contract's administrator.


### Getting Started

To interact with this contract, you can deploy it on Remix Ethereum IDE or any Ethereum-compatible blockchain.
1. Open Remix Ethereum IDE.
2. Create a new file and paste the provided Solidity code.
3. Compile the code.
4. Deploy the contract.
5. Interact with the deployed contract by calling its functions.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract PharmacyInventory {
    address public owner;

    struct Medicine {
        string name;
        uint256 price; 
        uint256 stock;
    }

    mapping(string => Medicine) public medicines;
    uint256 public medicineCount;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can perform this action");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    // Add a new medicine to the inventory
    function addMedicine(string memory _medicineName, uint256 _price, uint256 _stock) public onlyOwner {
        medicines[_medicineName] = Medicine(_medicineName, _price, _stock);
        medicineCount++;
    }

    // Purchase medicine
    function purchaseMedicine(string memory _medicineName, uint256 _quantity) public payable {
        require(bytes(medicines[_medicineName].name).length > 0, "Medicine does not exist"); // Check if medicine exists
        Medicine storage medicine = medicines[_medicineName];

        require(_quantity > 0, "Quantity must be greater than zero");
        require(medicine.stock >= _quantity, "Not enough stock");

        medicine.stock -= _quantity;
        payable(owner).transfer(medicine.price * _quantity);
    }

   //  Check the stock of a medicine
    function checkStock(string memory _medicineName) public view returns (uint256) {
        require(bytes(medicines[_medicineName].name).length > 0, "Medicine does not exist"); // Check if medicine exists
        return medicines[_medicineName].stock;
    }
}

This is the whole functionality within the code itself and the generalization of how the code will run.

### Authors

Baquiran, Kristine Mae P. 
8215029@ntc.edu.ph
