# Chaincast Core Contract

The Chaincast Core contract is responsible for the bulk of the chaincast operations.

## Terminology and Notation

- **Broadcaster**: Represents a broadcasting entity, can be a protocol or a DAO or any other entity.
- **End User**: Represents the end-user consuming the service.
- **=**: An equals sign on the type definitions means the property is optional.

## Core Models

### Network Types Schema

Network types are the networks' top-most classification. For example helping differentiate between Ethereum clones and Solana or Cosmos.

- `id` **uint16** - The unique identifier of the network type.
- `name` **string** - The name of the network type.

### Networks Schema

- `id` **uint32** - The unique identifier of the network.
- `networkTypeId` **uint16** - Reference to the network type.
- `name` **string** - Network Name.
- `chainId` **uint32=** - Chain ID if applicable.
- `networkId` **uint32=** - Network ID if applicable.

### Categories

Each broadcast needs to belong to a category.

- `id` **uint32** - The unique identifier of the category.
- `name` **bytes32** - Category name.
- `duration` **uint16** - Duration threshold for fees.
- `enabled` **boolean** Enabled state of category.

## Registering New Broadcasters

### Broadcaster Schema

The following properties describe a broadcaster object:

- `id` **uint256** - The unique identifier of the broadcaster.
- `name` **string** - The name of the broadcaster.
- `primaryNetworkId` **uint256** - The primary network of this broadcaster.
- `secondaryNetworkIds` **uint[]=** - All networks the broadcaster has presense with.
- `website` **string=** - Primary broadcaster's website.
- `discord` **string=** - Discord invitation link.
- `owner` **address** Address that owns this broadcaster entity and can post broadcasts on their behalf.
- `active` **boolean** Indicates if the broadcaster entity is active and can perform broadcasts.
- `isApplication` **boolean** Indicates if the broadcaster entity is in application state pending approval.

### broadcasterApply(broadcastStruct)

- Create an application to become a broadcaster.
- Can be called by anyone
- Application should remain pending till admin approves it.

### broadcasterDecline(applicationId)

- Can only be called by admin.
- Declines a broadcaster application.

### broadcasterApprove(applicationId)

- Can only be called by admin.
- Approves a broadcaster application.

### broadcasterSuspend(broadcasterId)

- Can only be called by admin.
- Will suspend a broadcaster entity.

### broadcasterActivate(broadcasterId)

- Can only be called by admin.
- Will activate a suspended broadcaster entity.

### broadcasterUpdate(broadcastStruct)

- Can only be called by admin or broadcaster owner.
- Updates the properties of a broadcaster.

## Publishing Broadcasts

### Broadcasts Schema

The following properties describe a broadcast object:

- `id` **uint256** - The unique identifier of the broadcast.
- `categoryId` **uint32** - The category id this broadcast belongs to.
- `broadcasterId` **uint256** - The broadcaster this broadcast belongs to.
- `broadcastUrl` **string** - The url pointing to the broadcast.
- `checksum` **string** The checksum of the broadcast contents.
- `createdAt` **Date** When the broadcast was created at.

### castPublish(broadcasterId, url, checksum, category, fee)

- Can only be called by broadcaster owner address.

### castDeprecate(broadcasterId, broadcastId)

- Can only be called by broadcaster owner address.

## Querying Functions

- `getByBroadcasterId(broadcasterId, optOffset, optLimit)`
- `getByCategoryId(categoryId, optNetworkIds[], optOffset, optLimit)`
- `getCategories(optOffset, optLimit)` Get a list of all categories.

## Admin Functions

- `setTokenAddress(address)` Will define which ERC20 token to be used for fees.
- `setBaseFee(uint256)` Will define the base fee.
- `categoryCreate(string)` Will create a category.
- `categoryEdit(categoryId, duration)` Will update the duration threshold of a category.
- `categoryDisable(categoryId)` Will disable a category.
