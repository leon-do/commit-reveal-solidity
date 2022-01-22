# commit-reveal-solidity

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract CommitReveal {

    // first commit is a hash
    bytes32 public commit;

    function Commit(bytes32 _commit) public {
        commit = _commit;
    }

    function Reveal(string memory _reveal) public view returns (bool){
        return keccak256(bytes(_reveal)) == commit;
    }

    function TestBadCommit() public returns (bool) {
        Commit("0x0");
        return Reveal("0x1");
    }

    function TestGoodCommit() public returns (bool) {
        string memory myCommit = "0x0";
        Commit(keccak256(bytes(myCommit)));
        return Reveal(myCommit);
    }
}
```
