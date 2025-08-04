# HomeFreely Plugin Wiki


---

## 🏠 Plugin Overview

**HomeFreely** is a powerful Minecraft Bukkit home teleportation plugin that supports multiple home points, permission group management, and a fully customizable message system.

- **Author**: Colpan
- **Version**: 1.0
- **Compatible Versions**: Minecraft 1.13+
- **Core Features**: Multiple home system, permission group management, custom messages

---

## ✨ Features

### 🎯 Core Features
- **Multiple Homes Support**: Players can set multiple home points
- **Permission Group System**: Different permission groups can set different numbers of homes
- **World Validation**: Ensures players can only teleport to homes in the same world
- **Fully Customizable**: All messages can be customized
- **Data Persistence**: Uses YAML files for safe home data storage

### 🔧 Administrative Features
- **Hot Reload**: Supports reloading configuration without server restart
- **Flexible Permissions**: Fine-grained permission control
- **Backward Compatibility**: Supports migration from old version home data

---

## 📦 Installation

### Step 1: Download Plugin
1. Download the `HomeFreely.jar` file
2. Place the file in your server's `plugins` folder

### Step 2: Start Server
1. Start or restart your Minecraft server
2. The plugin will automatically generate configuration files

### Step 3: Configure Plugin
1. Edit the `plugins/HomeFreely/config.yml` file
2. Adjust permission groups and message settings as needed
3. Use `/homeplugin reload` to reload configuration

---

## 🎮 Commands

### Basic Commands

#### `/sethome [name]`
Set a home point
- **Permission**: `home.set`
- **Usage**: 
  - `/sethome` - Set default home "home"
  - `/sethome mine` - Set a home named "mine"

#### `/home [name]`
Teleport to a home point
- **Permission**: `home.tp`
- **Usage**:
  - `/home` - Teleport to default home "home"
  - `/home mine` - Teleport to home named "mine"

#### `/delhome <name>`
Delete a specified home point
- **Permission**: `home.del`
- **Usage**: `/delhome mine` - Delete home named "mine"

#### `/homelist`
Display list of all home points
- **Permission**: `home.list`
- **Shows**: Home names, worlds, and coordinate information

### Administrative Commands

#### `/homeplugin reload`
Reload plugin configuration
- **Permission**: `home.admin`
- **Function**: Hot reload configuration files without server restart

---

## 🔐 Permissions

### Basic Permissions
| Permission Node | Description | Default |
|----------------|-------------|---------|
| `home.set` | Allows setting homes | true |
| `home.tp` | Allows teleporting to homes | true |
| `home.del` | Allows deleting homes | true |
| `home.list` | Allows viewing home list | true |
| `home.admin` | Allows using admin commands | op |

### Permission Group Permissions
| Permission Node | Description | Default |
|----------------|-------------|---------|
| `home.group.default` | Default group permission | true |
| `home.group.vip` | VIP group permission | false |
| `home.group.admin` | Admin group permission | false |

### Permission Configuration Example (LuckPerms)
```yaml
# Grant VIP permission group to player
/lp user <username> permission set home.group.vip true

# Grant admin permission group to player
/lp user <username> permission set home.group.admin true
```

---

## ⚙️ Configuration

### Complete config.yml Configuration
```yaml
# Message configuration (supports color codes & and placeholders)
messages:
  no-permission: "&cYou don't have permission!"
  home-set: "&aHome {name} set successfully!"
  home-deleted: "&aHome {name} deleted!"
  home-teleported: "&aTeleported to home {name}!"
  no-home: "&cYou haven't set a home named {name}!"
  home-list-header: "&aYour homes ({count}/{max}):"
  home-list-item: "&7- {name} in {world} at {x}, {y}, {z}"
  max-homes-reached: "&cYou can only set up to {max} homes in group {group}!"
  different-world: "&cYour home is in a different world!"
  world-not-found: "&cHome world not found!"
  reload-success: "&aPlugin reloaded successfully!"
  invalid-command: "&cInvalid command!"

# Permission group configuration
groups:
  default:
    max-homes: 1      # Default players can set 1 home
  vip:
    max-homes: 3      # VIP players can set 3 homes
  admin:
    max-homes: -1     # Admins have unlimited homes (-1 means unlimited)

# Group priority (highest to lowest priority)
group-priority:
  - admin
  - vip
  - default
```

---

## 👥 Permission Groups

### Default Permission Group Configuration

#### Default Group
- **Max Homes**: 1
- **How to Get**: All players have this by default
- **Permission Node**: `home.group.default`

#### VIP Group
- **Max Homes**: 3
- **How to Get**: Must be manually granted permission
- **Permission Node**: `home.group.vip`

#### Admin Group
- **Max Homes**: Unlimited
- **How to Get**: Must be manually granted permission
- **Permission Node**: `home.group.admin`

### Custom Permission Groups

You can add custom permission groups in `config.yml`:

```yaml
groups:
  default:
    max-homes: 1
  vip:
    max-homes: 3
  premium:          # New custom group
    max-homes: 5
  admin:
    max-homes: -1

group-priority:
  - admin
  - premium         # Add to priority list
  - vip
  - default
```

Remember to also create the corresponding permission node `home.group.premium` in your permission plugin.

---

## 💬 Custom Messages

### Message Placeholders

The plugin supports the following placeholders:

| Placeholder | Description | Usage Context |
|-------------|-------------|---------------|
| `{name}` | Home name | All home-related messages |
| `{max}` | Maximum home count | Home limit messages |
| `{group}` | Player permission group | Permission group related messages |
| `{count}` | Current home count | Home list messages |
| `{world}` | World name | Home location messages |
| `{x}` `{y}` `{z}` | Coordinates | Home location messages |

### Color Code Support

The plugin supports standard Minecraft color codes:

```yaml
messages:
  home-set: "&a&l[SUCCESS] &r&aHome &e{name} &aset successfully!"
  no-permission: "&c&l[ERROR] &r&cYou don't have permission to do this!"
```

### Multi-Language Examples

#### English Configuration
```yaml
messages:
  no-permission: "&cYou don't have permission!"
  home-set: "&aHome {name} set successfully!"
  home-teleported: "&aTeleported to home {name}!"
```

#### Spanish Configuration
```yaml
messages:
  no-permission: "&c¡No tienes permisos!"
  home-set: "&a¡Casa {name} establecida con éxito!"
  home-teleported: "&a¡Teletransportado a casa {name}!"
```

#### French Configuration
```yaml
messages:
  no-permission: "&cVous n'avez pas la permission!"
  home-set: "&aMaison {name} définie avec succès!"
  home-teleported: "&aTéléporté à la maison {name}!"
```

---

## ❓ FAQ

### Q: How do I assign different permission groups to players?
**A**: Use a permission plugin (like LuckPerms) to assign corresponding permission nodes to players:
```
/lp user <username> permission set home.group.vip true
```

### Q: Players can't teleport to homes in other worlds?
**A**: This is a safety feature of the plugin. Players can only teleport to homes in their current world to prevent accidental cross-world teleportation.

### Q: How do I give admins unlimited homes?
**A**: Make sure admins have the `home.group.admin` permission, with `max-homes` set to -1 for that group.

### Q: Which Minecraft versions does the plugin support?
**A**: The plugin supports Minecraft 1.13 and above.

### Q: How do I backup home data?
**A**: Home data is stored in the `plugins/HomeFreely/homes.yml` file. Regularly backup this file.

### Q: Do I need to restart the server after changing configuration?
**A**: No, use the `/homeplugin reload` command to hot reload the configuration.

### Q: How can I view all homes of a specific player?
**A**: Currently, the plugin doesn't support admins viewing other players' homes. This feature may be added in future versions.

### Q: Where are the plugin's data files located?
**A**: 
- Configuration file: `plugins/HomeFreely/config.yml`
- Home data: `plugins/HomeFreely/homes.yml`

### Q: Can players have homes with the same name?
**A**: Each player can have multiple homes, but each home must have a unique name for that player. Different players can have homes with the same names.

### Q: What happens if I delete a world that has player homes?
**A**: The plugin will show a "world not found" error when players try to teleport to homes in deleted worlds. The home data remains in the file but becomes inaccessible.

### Q: How do I migrate from another home plugin?
**A**: Currently, there's no automatic migration tool. You'll need to ask players to reset their homes after installing HomeFreely.

---

## 🛠️ Troubleshooting

### Common Issues and Solutions

#### Issue: Plugin doesn't load
**Solution**: 
1. Check server console for error messages
2. Ensure you're using Minecraft 1.13+
3. Verify the plugin file isn't corrupted

#### Issue: Commands don't work
**Solution**: 
1. Check if players have the required permissions
2. Verify the plugin is properly loaded with `/plugins`
3. Check for any conflicts with other plugins

#### Issue: Configuration changes don't apply
**Solution**: 
1. Use `/homeplugin reload` after making changes
2. Check YAML syntax in config.yml
3. Restart server if hot reload fails

#### Issue: Homes disappear after server restart
**Solution**: 
1. Check if `homes.yml` file has proper write permissions
2. Look for errors in server console during shutdown
3. Ensure no other plugins are interfering with the data folder

---

## 🔧 Advanced Configuration

### Creating Custom Group Hierarchies

You can create complex permission hierarchies:

```yaml
groups:
  guest:
    max-homes: 0      # Guests can't set homes
  member:
    max-homes: 1
  trusted:
    max-homes: 2
  vip:
    max-homes: 5
  premium:
    max-homes: 10
  staff:
    max-homes: 20
  admin:
    max-homes: -1

group-priority:
  - admin
  - staff
  - premium
  - vip
  - trusted
  - member
  - guest
```

### Custom Message Formatting

You can create elaborate message formats:

```yaml
messages:
  home-set: "&8[&aHomeFreely&8] &7Home &f{name} &7has been set at &f{x}&7, &f{y}&7, &f{z} &7in &f{world}&7!"
  home-teleported: "&8[&aHomeFreely&8] &7Whoosh! Teleported to &f{name}&7!"
  home-list-header: "&8▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬\n&a&lYour Homes &8(&f{count}&8/&f{max}&8)\n&8▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬"
```

---

## 📋 Changelog

### Version 1.0
- ✅ Initial release
- ✅ Multiple home system
- ✅ Permission group management
- ✅ Custom message system
- ✅ World validation feature
- ✅ Hot reload support
- ✅ Backward compatibility with old version data

---

## 🤝 Support & Feedback

If you encounter issues or have feature suggestions, please contact the plugin author Colpan.

### Useful Links
- **Plugin Author**: Colpan
- **Plugin Version**: 1.0
- **Minimum Requirements**: Minecraft 1.13+

### Getting Help
1. Check this wiki for common solutions
2. Review the FAQ section
3. Check server console for error messages
4. Contact the plugin author with detailed information about your issue

---

## 📝 License & Credits

### Credits
- **Developer**: Colpan
- **Framework**: Bukkit/Spigot API
- **Storage**: YAML Configuration

### Usage Rights
This plugin is provided as-is. Please respect the author's work and provide proper attribution when sharing or modifying.

---

*Thank you for using HomeFreely plugin! Enjoy your gaming experience!* 🎮
