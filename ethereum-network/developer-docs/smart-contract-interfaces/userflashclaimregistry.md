# UserFlashclaimRegistry

UserFlashclaimRegistry.sol is used for deploying AirdropFlashClaimReceiver for Omni money market user.

## Write Functions <a href="#write-functions" id="write-functions"></a>

### createRecevier <a href="#createrecevier" id="createrecevier"></a>

1function createReceiver() external;Copied!Main function of the contract, deploy a AirdropFlashClaimReceiver.sol for user who call the function.​

## Read Functions <a href="#read-functions" id="read-functions"></a>

### getUserReceivers <a href="#getuserreceivers" id="getuserreceivers"></a>

1function getUserReceivers(address user) external view returns (address)Copied!Fetch AirdropFlashClaimReceiver contract address deployed by the user.

#### Call params <a href="#call-params" id="call-params"></a>

NameTypeDescriptionuseraddressuser EOA address.

#### Return value <a href="#return-value" id="return-value"></a>

TypeDescriptionaddressuser's AirdropFlashClaimReceiver contract address
