# Base-DeFi-Liquidity-Pool
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
contract LiquidityPool {
    IERC20 public token1;
    IERC20 public token2;
    uint256 public liquidity;
    uint256 public apr;
    constructor(address _token1, address _token2, uint256 _apr) {
        token1 = IERC20(_token1);
        token2 = IERC20(_token2);
    apr = _apr;
    }
    function addLiquidity(uint256 amount1, uint256 amount2) external {
        token1.transferFrom(msg.sender, address(this), amount1);
        token2.transferFrom(msg.sender, address(this), amount2);
        liquidity += amount1 + amount2;
    }
    function withdrawLiquidity(uint256 amount) external {
        require(liquidity >= amount, "Insufficient liquidity");
        liquidity -= amount;
        token1.transfer(msg.sender, amount);
        token2.transfer(msg.sender, amount);
    }
}
