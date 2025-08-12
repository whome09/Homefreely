# 🏠 Homefreely - Advanced Home Teleport Plugin

**Homefreely** is a feature-rich Minecraft Bukkit home teleport plugin that supports multiple homes, permission groups, coordinate setting, safety checks, and PlaceholderAPI integration.

## 🌟 Core Features

### ✨ Main Features

- **Multiple Homes Support** - Players can set multiple home locations
- **Permission Group System** - Different groups can have different home limits
- **Coordinate Setting** - Support for precise home placement via coordinates
- **Safety Checks** - Intelligent detection of unsafe locations to prevent players from getting stuck in dangerous areas
- **PlaceholderAPI** - Complete placeholder support for displaying home information in other plugins
- **Hot Reload** - Update configuration without restarting the server
- **Backward Compatibility** - Support for migrating data from older versions

### 🔧 Advanced Features

- **World Restrictions** - Limit specific permission groups to specific worlds
- **Economy Integration** - Support for home setting costs (requires Vault)
- **Confirmation System** - Require player confirmation for dangerous locations
- **Range Limiting** - Limit maximum distance for coordinate setting
- **Hostile Mob Detection** - Automatically detect hostile mobs nearby

## 🚀 Quick Start

### 1. Install Plugin

```bash
# Download plugin
Download Homefreely-1.1.0.jar

# Place in server
Copy file to plugins/ folder

# Start server
Start or restart your Minecraft server
```

### 2. Basic Configuration

Plugin automatically generates configuration files on first startup:

- `plugins/Homefreely/config.yml` - Main configuration file
- `plugins/Homefreely/homes.yml` - Home data file

### 3. Basic Usage

```bash
# Set home
/sethome home

# Teleport to home
/home home

# View all homes
/homelist

# Delete home
/delhome home
```

## 📁 File Structure

```
Homefreely/
├── config.yml          # Main configuration file
├── homes.yml           # Home data file
├── README.md           # This documentation
├── CONFIG.md           # Detailed configuration guide
├── COMMANDS.md         # Command usage guide
├── PERMISSIONS.md      # Permission system guide
└── API.md             # Developer API documentation
```

## 🎯 Permission Group Examples

| Group       | Max Homes       | Special Permissions |
| ----------- | --------------- | ------------------- |
| **default** | 1 home          | Basic features      |
| **vip**     | 3 homes         | More homes          |
| **premium** | 5 homes         | World restrictions  |
| **admin**   | Unlimited homes | All permissions     |

## 🔗 Related Links

- [📋 Configuration Guide](CONFIG.md) - Detailed configuration instructions
- [⌨️ Commands Guide](COMMANDS.md) - All command usage methods
- [🔐 Permissions Guide](PERMISSIONS.md) - Permission system details
- [⚙️ API Guide](API.md) - Developer interface documentation

## 💡 Usage Recommendations

### Newbie Servers

- Use default configuration
- Give all players `home.set` permission
- Limit each player to 1-2 homes

### Medium Servers

- Create VIP permission groups with 3-5 homes
- Enable safety check features
- Use PlaceholderAPI to display home information

### Large Servers

- Set up multiple permission tiers
- Enable economy system integration
- Configure world restriction rules
- Use database storage (future version support)

## 🐛 Common Questions

**Q: What versions does the plugin support?**
A: Supports Minecraft 1.13 and above

**Q: Is PlaceholderAPI required?**
A: No, but PlaceholderAPI support is available for additional features

**Q: How to backup home data?**
A: Backup the `plugins/Homefreely/homes.yml` file

**Q: Does it support MySQL?**
A: Current version uses YAML file storage, database support will be added in future versions

# ⌨️ Homefreely Commands Documentation

This document provides detailed information about all commands in the Homefreely plugin.

## 📋 Command Overview

| Command       | Permission   | Description      |
| ------------- | ------------ | ---------------- |
| `/sethome`    | `home.set`   | Set a home       |
| `/home`       | `home.tp`    | Teleport to home |
| `/delhome`    | `home.del`   | Delete a home    |
| `/homelist`   | `home.list`  | View home list   |
| `/homeplugin` | `home.admin` | Admin commands   |

---

## 🏠 /sethome - Set Home

### Basic Usage

```bash
# Set default home
/sethome

# Set named home
/sethome <name>

# Set coordinate home
/sethome <name> <x> <y> <z>

# Confirm setting unsafe location
/sethome <name> confirm
```

### Parameter Description

| Parameter     | Optional | Description        | Example                |
| ------------- | -------- | ------------------ | ---------------------- |
| `<name>`      | ✅        | Home name          | `home`, `base`, `mine` |
| `<x> <y> <z>` | ✅        | Exact coordinates  | `100 64 200`           |
| `confirm`     | ✅        | Force confirmation | `confirm`              |

### Usage Examples

#### Example 1: Basic Setting

```bash
# Set current location as default home
/sethome

# Set current location as "base"
/sethome base

# Set current location as "mine"
/sethome mine
```

#### Example 2: Coordinate Setting

```bash
# Set home at coordinates (100, 64, 200)
/sethome base 100 64 200

# Set precise coordinate home
/sethome precise 123.5 67.2 456.8
```

#### Example 3: Force Setting

```bash
# Attempt to set home but prompted as unsafe
/sethome danger
# System prompt: "Location danger is unsafe!"

# Force set unsafe location
/sethome danger confirm
```

### Limitations

- **Permission Limit**: Requires `home.set` permission
- **Quantity Limit**: Limited by permission group maximum homes
- **World Limit**: Limited by permission group world restrictions
- **Economy Limit**: Requires sufficient coins (if enabled)
- **Distance Limit**: Coordinate setting has maximum distance limit

---

## 🚀 /home - Teleport to Home

### Basic Usage

```bash
# Teleport to default home
/home

# Teleport to specific home
/home <name>
```

### Parameter Description

| Parameter | Optional | Description | Example        |
| --------- | -------- | ----------- | -------------- |
| `<name>`  | ✅        | Home name   | `home`, `base` |

### Usage Examples

```bash
# Teleport to default home
/home

# Teleport to "base"
/home base

# Teleport to "mine"
/home mine
```

### Limitations

- **Permission Limit**: Requires `home.tp` permission
- **World Limit**: Can only teleport to homes in current world
- **Existence Check**: Home must exist
- **World Existence**: Target world must exist

---

## 🗑️ /delhome - Delete Home

### Basic Usage

```bash
# Delete specific home
/delhome <name>
```

### Parameter Description

| Parameter | Optional | Description         | Example        |
| --------- | -------- | ------------------- | -------------- |
| `<name>`  | ❌        | Home name to delete | `base`, `mine` |

### Usage Examples

```bash
# Delete "base"
/delhome base

# Delete "mine"
/delhome mine

# Delete default home
/delhome home
```

### Notes

- **Irreversible**: Cannot be recovered after deletion
- **Permission Required**: Requires `home.del` permission
- **Existence Check**: Can only delete existing homes

---

## 📋 /homelist - View Home List

### Basic Usage

```bash
# View all homes
/homelist
```

### Display Content

After execution, displays:

```
Your homes (3/5):
- home at world (100.5, 64.0, 200.3)
- base at world_nether (50.0, 70.5, 150.2)
- mine at world (-120.3, 45.0, 300.7)
```

### Information Description

- **Count**: Current homes/maximum allowed
- **Location**: World name and precise coordinates
- **Format**: Coordinates displayed with one decimal place

---

## ⚙️ /homeplugin - Admin Commands

### Subcommands

```bash
# Reload plugin configuration
/homeplugin reload

# View plugin version
/homeplugin version
```

### Usage Examples

```bash
# Reload configuration file
/homeplugin reload
# Returns: "Plugin reloaded successfully!"

# View version information
/homeplugin version
# Returns: "Homefreely v1.1.0 by Colpan"
```

### Admin Features

- **Hot Reload**: Update configuration without restarting server
- **Version Check**: View current plugin version
- **Debug Info**: Get plugin status information

---

## 🎯 Practical Usage Scenarios

### Scenario 1: New Player Setting Home

```bash
# 1. Find suitable location
# 2. Set first home
/sethome

# 3. View setting result
/homelist
```

### Scenario 2: Establish Base Network

```bash
# 1. Set home at main base
/sethome mainbase

# 2. Set home at mine
/sethome mine

# 3. Set home at farm
/sethome farm

# 4. Quick teleport between bases
/home mainbase
/home mine
```

### Scenario 3: Admin Setting Precise Homes

```bash
# 1. Get precise coordinates
# 2. Set home for player
/sethome spawn 0 64 0

# 3. Notify player to use
# Tell player: Use /home spawn to teleport to spawn point
```

### Scenario 4: Cleaning Unneeded Homes

```bash
# 1. View all homes
/homelist

# 2. Delete unneeded homes
/delhome temp
/delhome oldbase

# 3. Confirm deletion result
/homelist
```

---

## 🔍 Error Handling

### Common Error Messages

#### Insufficient Permission

```
Error: "You don't have permission!"
Solution: Contact admin to grant appropriate permissions
```

#### Home Doesn't Exist

```
Error: "You haven't set a home named base!"
Solution: Use /sethome base to set home first
```

#### Reached Quantity Limit

```
Error: "You can only set 3 homes in default group!"
Solution: Delete old homes or upgrade permission group
```

#### World Mismatch

```
Error: "Your home is in a different world!"
Solution: Go to correct world or use /sethome to reset
```

#### Location Unsafe

```
Error: "Location skybase is unsafe!"
Solution: Choose safe location or use confirm to force set
```

---

## 💡 Usage Tips

### 1. Home Naming Conventions

```bash
# Use meaningful names
/sethome mainbase
/sethome netherfarm
/sethome endportal

# Avoid special characters
# Recommended: letters, numbers, Chinese
# Not recommended: spaces, symbols
```

### 2. Coordinate Recording

```bash
# Record important coordinates
/sethome village -200 70 300
/sethome temple 1200 65 -800

# Use F3 to view coordinates
# Press F3 to show debug screen, record XYZ coordinates
```

### 3. Home Management

```bash
# Regular cleanup
/homelist  # View all homes
/delhome oldhome  # Delete unneeded ones

# Reasonable naming
/sethome home-overworld
/sethome home-nether
/sethome home-end
```

### 4. Admin Tips

```bash
# Set home for player
# First teleport to target location
/tp playername 100 64 200
# Then have player set
/sethome public
```

---

## 📊 Command Permission Comparison

| Command       | Basic Permission | Extra Permission    | Description    |
| ------------- | ---------------- | ------------------- | -------------- |
| `/sethome`    | `home.set`       | `home.bypass.*`     | Set home       |
| `/home`       | `home.tp`        | `home.bypass.world` | Teleport home  |
| `/delhome`    | `home.del`       | -                   | Delete home    |
| `/homelist`   | `home.list`      | -                   | View list      |
| `/homeplugin` | `home.admin`     | -                   | Admin commands |

### Bypass Permissions

- `home.bypass.safety` - Bypass safety checks
- `home.bypass.world` - Bypass world restrictions
- `home.bypass.cost` - Bypass economy restrictions

# ⚙️ Homefreely Configuration Guide

This document provides detailed information about all configuration options for the Homefreely plugin.

## 📋 Configuration File Structure

### Main Configuration File (`config.yml`)

```yaml
# Message configuration (supports color codes & and placeholders)
messages:
  # Basic messages
  no-permission: "&cYou don't have permission!"
  home-set: "&aHome {name} set successfully!"
  home-deleted: "&aHome {name} deleted!"
  home-teleported: "&aTeleported to home {name}!"
  no-home: "&cYou haven't set a home named {name}!"
  home-list-header: "&aYour homes ({count}/{max}):"
  home-list-item: "&7- {name} at {world} ({x}, {y}, {z})"
  max-homes-reached: "&cYou can only set {max} homes in {group} group!"
  different-world: "&cYour home is in a different world!"
  world-not-found: "&cHome world not found!"
  reload-success: "&aPlugin reloaded successfully!"
  invalid-command: "&cInvalid command!"
  
  # New messages (v1.1.0+)
  unsafe-location: "&cLocation {name} is unsafe! Use /sethome {name} confirm to force set"
  confirm-set: "&aConfirmed setting home {name}!"
  coordinate-set: "&aCoordinate home {name} set!"
  out-of-range: "&cCoordinates out of range! Max distance: {blocks} blocks"
  invalid-coordinates: "&cInvalid coordinate format!"
  condition-world: "&cNot allowed to set homes in {world} world!"
  condition-cost: "&cSetting home requires {cost} coins!"

# Permission group configuration
groups:
  default:
    max-homes: 1           # Maximum homes (-1 = unlimited)
    cost: 0.0             # Home setting cost (requires Vault)
    allowed-worlds: []    # Allowed worlds (empty = all worlds)
  
  vip:
    max-homes: 3
    cost: 0.0
    allowed-worlds: []
  
  premium:
    max-homes: 5
    cost: 100.0           # 100 coins per home
    allowed-worlds: ["world", "world_nether"]
  
  admin:
    max-homes: -1         # -1 means unlimited
    cost: 0.0
    allowed-worlds: ["*"] # * means all worlds

# Group priority (from high to low)
group-priority:
  - admin
  - premium
  - vip
  - default

# Coordinate setting configuration
coordinate-settings:
  max-distance: 32        # Maximum coordinate setting distance (blocks)
  require-exact: false    # Whether exact coordinates are required

# Safety check configuration
safety-check:
  enable: true            # Enable safety checks
  check-height: true      # Check height limits
  min-y: 5               # Minimum safe height
  max-y: 250             # Maximum safe height
  check-void: true        # Check for void
  check-hostile: true     # Check for hostile mobs
  hostile-radius: 8       # Hostile mob detection radius (blocks)

# Economy system configuration
economy:
  enable: false           # Enable economy system (requires Vault)
  currency: "coins"        # Currency name
```

## 🎯 Configuration Details

### 1. Message Configuration

#### Supported Placeholders

| Placeholder       | Description           | Example           |
| ----------------- | --------------------- | ----------------- |
| `{name}`          | Home name             | `home`, `base`    |
| `{max}`           | Maximum homes         | `3`, `unlimited`  |
| `{group}`         | Permission group name | `vip`, `admin`    |
| `{count}`         | Current home count    | `2`               |
| `{world}`         | World name            | `world`, `nether` |
| `{x}` `{y}` `{z}` | Coordinates           | `100.5`, `64.0`   |
| `{blocks}`        | Distance value        | `32`              |
| `{cost}`          | Cost value            | `100.0`           |

#### Color Codes

Supports standard Minecraft color codes:

- `&a` - Green
- `&c` - Red
- `&e` - Yellow
- `&7` - Gray
- `&l` - Bold
- `&o` - Italic

### 2. Permission Group Configuration

#### Group Parameters

```yaml
groups:
  groupname:
    max-homes: number      # Maximum homes (-1 = unlimited)
    cost: cost            # Home setting cost (0 = free)
    allowed-worlds:       # Allowed worlds list
      - "world"          # Specific world
      - "world_nether"   # Nether
      - "*"              # All worlds (wildcard)
```

#### Group Priority

The system checks player permissions in the order of `group-priority`:

1. Check from top to bottom
2. First matching group takes effect
3. Use `default` if no group matches

### 3. Safety Check Configuration

#### Check Types

- **Height Check**: Prevent setting in too low or high locations
- **Void Check**: Prevent setting in void or suspended locations
- **Hostile Mob Check**: Detect hostile mobs nearby

#### Hostile Mob List

Default hostile mobs detected:

- Zombie (ZOMBIE)
- Skeleton (SKELETON)
- Creeper (CREEPER)
- Spider (SPIDER)
- Enderman (ENDERMAN)
- Witch (WITCH)
- Blaze (BLAZE)
- Ghast (GHAST)
- Phantom (PHANTOM)
- Husk (HUSK)
- Drowned (DROWNED)

### 4. Coordinate Setting Configuration

#### Usage Scenarios

- Admins setting precise locations for players
- Building servers requiring exact coordinates
- Limiting players from setting homes too far away

#### Configuration Example

```yaml
coordinate-settings:
  max-distance: 50      # Admins can set homes within 50 blocks
  require-exact: true   # Must provide exact coordinates
```

## 📝 Configuration Examples

### Example 1: Basic Server

```yaml
# Suitable for small servers
groups:
  default:
    max-homes: 2
    cost: 0.0
    allowed-worlds: []
  
  vip:
    max-homes: 5
    cost: 0.0
    allowed-worlds: []

group-priority:
  - vip
  - default
```

### Example 2: RPG Server

```yaml
# Suitable for RPG servers
groups:
  adventurer:
    max-homes: 1
    cost: 50.0
    allowed-worlds: ["world", "world_nether"]
  
  knight:
    max-homes: 3
    cost: 100.0
    allowed-worlds: ["world", "world_nether", "world_the_end"]
  
  lord:
    max-homes: 5
    cost: 200.0
    allowed-worlds: ["*"]
  
  admin:
    max-homes: -1
    cost: 0.0
    allowed-worlds: ["*"]

group-priority:
  - admin
  - lord
  - knight
  - adventurer
  - default
```

### Example 3: Creative Server

```yaml
# Suitable for creative servers
groups:
  builder:
    max-homes: 10
    cost: 0.0
    allowed-worlds: ["*"]
  
  architect:
    max-homes: -1
    cost: 0.0
    allowed-worlds: ["*"]

group-priority:
  - architect
  - builder
  - default
```

## 🔧 Advanced Configuration Tips

### 1. World Restriction Strategy

```yaml
# Restrict survival world homes to survival world only
groups:
  survival:
    max-homes: 3
    allowed-worlds: ["world", "world_nether", "world_the_end"]
  
  creative:
    max-homes: 5
    allowed-worlds: ["creative", "creative_nether"]
```

### 2. Economy Balance

```yaml
# Progressive cost based on home count
economy:
  enable: true
  currency: "coins"

groups:
  default:
    max-homes: 3
    cost: 100.0  # 1st home costs 100 coins
  
  # Actual cost = cost * (current homes + 1)
  # 2nd home costs 200 coins, 3rd home costs 300 coins
```

### 3. Safety Check Optimization

```yaml
# Adjust safety checks based on server type
safety-check:
  enable: true
  check-height: false    # Creative servers can disable height check
  min-y: -64            # 1.18+ supports lower heights
  max-y: 320            # 1.18+ supports higher heights
  check-void: true
  check-hostile: false   # PVP servers can disable hostile mob check
  hostile-radius: 5      # Reduce detection range
```

## 🔄 Configuration Reload

After modifying configuration, use the following command to reload:

```bash
/homeplugin reload
```

Reload will:

- Reload all messages
- Update permission group configuration
- Apply new safety check rules
- Not affect stored home data

---

**💡 Tip**: Always backup original files before modifying configuration to prevent errors from causing plugin issues.

# 🔐 Homefreely Permission System Documentation

This document provides detailed information about the Homefreely plugin's permission system, including permission nodes, group configuration, and permission management.

## 📋 Permission Overview

### Basic Permission Nodes

| Permission Node | Description                | Default | Target      |
| --------------- | -------------------------- | ------- | ----------- |
| `home.set`      | Allow setting homes        | `true`  | All players |
| `home.tp`       | Allow teleporting to homes | `true`  | All players |
| `home.del`      | Allow deleting homes       | `true`  | All players |
| `home.list`     | Allow viewing home list    | `true`  | All players |
| `home.admin`    | Allow admin commands       | `op`    | Admins      |

### Permission Group Permissions

| Permission Node      | Description              | Default | Example         |
| -------------------- | ------------------------ | ------- | --------------- |
| `home.group.default` | Default permission group | `true`  | 1 home          |
| `home.group.vip`     | VIP permission group     | `false` | 3 homes         |
| `home.group.premium` | Premium permission group | `false` | 5 homes         |
| `home.group.admin`   | Admin permission group   | `false` | Unlimited homes |

### Bypass Permissions

| Permission Node      | Description                 | Default | Use Case                          |
| -------------------- | --------------------------- | ------- | --------------------------------- |
| `home.bypass.safety` | Bypass safety checks        | `op`    | Admin setting dangerous locations |
| `home.bypass.world`  | Bypass world restrictions   | `op`    | Cross-world teleportation         |
| `home.bypass.cost`   | Bypass economy restrictions | `op`    | Free home setting                 |

---

## 🎯 Permission Group System

### Permission Group Priority

The system checks permission groups in the following order (from high to low):

1. **admin** - Admin group
2. **premium** - Premium user group
3. **vip** - VIP user group
4. **default** - Default user group

### Permission Group Configuration Example

#### Default Configuration

```yaml
groups:
  default:
    max-homes: 1
    cost: 0.0
    allowed-worlds: []
  
  vip:
    max-homes: 3
    cost: 0.0
    allowed-worlds: []
  
  premium:
    max-homes: 5
    cost: 100.0
    allowed-worlds: ["world", "world_nether"]
  
  admin:
    max-homes: -1
    cost: 0.0
    allowed-worlds: ["*"]

group-priority:
  - admin
  - premium
  - vip
  - default
```

---

## 🔧 Permission Management

### LuckPerms Configuration

#### 1. Basic Permission Settings

```bash
# Give player basic permissions
/lp user <player> permission set home.set true
/lp user <player> permission set home.tp true
/lp user <player> permission set home.del true
/lp user <player> permission set home.list true
```

#### 2. Permission Group Settings

```bash
# Set VIP permission group
/lp user <player> permission set home.group.vip true

# Set premium permission group
/lp user <player> permission set home.group.premium true

# Set admin permission group
/lp user <player> permission set home.group.admin true
```

#### 3. Admin Permissions

```bash
# Give admin permissions
/lp user <player> permission set home.admin true

# Give bypass permissions
/lp user <player> permission set home.bypass.safety true
/lp user <player> permission set home.bypass.world true
/lp user <player> permission set home.bypass.cost true
```

### GroupManager Configuration

#### 1. Create Permission Groups

```yaml
# groups.yml
groups:
  Default:
    permissions:
    - home.set
    - home.tp
    - home.del
    - home.list
    - home.group.default
    
  VIP:
    permissions:
    - home.set
    - home.tp
    - home.del
    - home.list
    - home.group.vip
    
  Admin:
    permissions:
    - home.*
    - home.group.admin
    inheritance:
    - VIP
```

### PermissionsEx Configuration

#### 1. Permission Configuration

```yaml
# permissions.yml
users:
  <player>:
    permissions:
    - home.set
    - home.tp
    - home.del
    - home.list
    - home.group.vip
    
groups:
  Default:
    permissions:
    - home.group.default
    
  VIP:
    permissions:
    - home.group.vip
    
  Admin:
    permissions:
    - home.*
```

---

## 🏗️ Permission Architecture Design

### Small Server Architecture

#### Permission Tiers

```
Guest
├── No home permissions
└── Can only visit

Member
├── home.set
├── home.tp
├── home.del
├── home.list
└── home.group.default

VIP
├── All basic permissions
└── home.group.vip

Admin
├── home.*
└── home.group.admin
```

#### Configuration Example

```bash
# Guest group
/lp group guest permission unset home.*

# Member group
/lp group member permission set home.set true
/lp group member permission set home.tp true
/lp group member permission set home.del true
/lp group member permission set home.list true
/lp group member permission set home.group.default true

# VIP group
/lp group vip permission set home.group.vip true

# Admin group
/lp group admin permission set home.admin true
/lp group admin permission set home.group.admin true
```

### Medium Server Architecture

#### Permission Tiers

```
Newbie
├── home.set (limited to 1)
├── home.tp
├── home.del
└── home.list

Resident
├── home.group.default (3 homes)

Builder
├── home.group.vip (5 homes)

Elite
├── home.group.premium (8 homes)

Moderator
├── home.admin
├── home.bypass.*
└── home.group.admin
```

### Large Server Architecture

#### Complex Permission System

```
Tourist
├── No permissions

Citizen
├── home.set
├── home.tp
├── home.del
├── home.list
└── home.group.citizen

Merchant
├── home.group.merchant

Noble
├── home.group.noble

Lord
├── home.group.lord

Staff
├── home.admin
├── home.bypass.*
└── home.group.staff
```

#### Configuration File

```yaml
groups:
  citizen:
    max-homes: 2
    cost: 0.0
    allowed-worlds: ["world"]
  
  merchant:
    max-homes: 4
    cost: 50.0
    allowed-worlds: ["world", "world_nether"]
  
  noble:
    max-homes: 7
    cost: 100.0
    allowed-worlds: ["world", "world_nether", "world_the_end"]
  
  lord:
    max-homes: 12
    cost: 200.0
    allowed-worlds: ["*"]
  
  staff:
    max-homes: -1
    cost: 0.0
    allowed-worlds: ["*"]

group-priority:
  - staff
  - lord
  - noble
  - merchant
  - citizen
  - default
```

---

## 🔍 Permission Debugging

### 1. Check Player Permissions

```bash
# LuckPerms
/lp user <player> info
/lp user <player> permission check home.set
/lp user <player> permission check home.group.vip

# PermissionsEx
/pex user <player> list
/pex group <group> list
```

### 2. Permission Testing

```bash
# Test permission groups
/lp user <player> permission set home.group.vip true
# Have player execute /homelist to see if it takes effect

# Test bypass permissions
/lp user <player> permission set home.bypass.safety true
# Try setting home in dangerous location
```

### 3. Permission Inheritance

```
Admin permission inheritance:
├── home.* (includes all permissions)
├── home.group.admin (unlimited homes)
├── home.bypass.* (all bypass permissions)
└── Inherits VIP permissions
```

---

## 🛡️ Security Permission Configuration

### 1. Prevent Abuse

```bash
# Restrict regular players
/lp group default permission unset home.bypass.*
/lp group default permission unset home.admin

# Only give necessary permissions
/lp group default permission set home.set true
/lp group default permission set home.tp true
/lp group default permission set home.del true
/lp group default permission set home.list true
```

### 2. Admin Permissions

```bash
# Full admin permissions
/lp group admin permission set home.* true
/lp group admin permission set home.bypass.safety true
/lp group admin permission set home.bypass.world true
/lp group admin permission set home.bypass.cost true
```

### 3. Permission Templates

#### Newbie Template

```yaml
# Suitable for newly registered players
permissions:
- home.set
- home.tp
- home.del
- home.list
- home.group.default
```

#### VIP Template

```yaml
# Suitable for paid players
permissions:
- home.set
- home.tp
- home.del
- home.list
- home.group.vip
```

#### Admin Template

```yaml
# Suitable for server administrators
permissions:
- home.*
- home.bypass.*
- home.group.admin
```

---

## 📊 Permission Best Practices

### 1. Permission Assignment Principles

- **Principle of Least Privilege**: Only give necessary permissions
- **Hierarchical Management**: Use permission groups instead of individual settings
- **Regular Review**: Periodically check player permissions
- **Documentation**: Record permission changes

### 2. Permission Group Naming Conventions

```
Recommended naming:
├── default (default)
├── vip (paid users)
├── premium (advanced users)
├── moderator (moderators)
├── admin (administrators)
└── owner (server owner)
```

### 3. Permission Testing Checklist

- [ ] Can new players set homes normally
- [ ] Do VIP players have correct home limits
- [ ] Can admins bypass restrictions
- [ ] Does permission inheritance work
- [ ] Does permission revocation work normally

---

## 🔧 Common Questions

### Q: Permissions not working?

**A**: Check steps:

1. Confirm permission plugin loaded correctly
2. Check permission node spelling
3. Use `/lp user <player> info` to view permissions
4. Check permission group priority

### Q: How to set permissions in bulk?

**A**: Use permission groups:

```bash
# Set permissions for entire group
/lp group vip permission set home.group.vip true
```

### Q: How to resolve permission conflicts?

**A**: Check priority:

1. View `group-priority` configuration
2. Confirm player's permission group
3. Check for conflicting permission settings

### Q: How to temporarily grant permissions?

**A**: LuckPerms supports temporary permissions:

```bash
/lp user <player> permission set home.group.vip true temporary 1h
```

---

**🔐 Reasonable permission configuration is the foundation for stable server operation!**
