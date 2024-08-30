
# Minicord.sh
**Minicord.sh** is a miniature shell-style language designed for AI LLMs such as ChatGPT, Gemini, Claude, and others to facilitate the operation of an AI server manager without the risk of the AI going rogue and executing `rm -rf` on the hosting server, which would result in the complete erasure of the bot. While this outcome is not guaranteed, it is the intended goal.

## Basics
### Formatting
The format for a single line generally follows this structure:
```
[class] [id] [action] [params]
```

- **[class]**: The type of the object being referred to. This can be `guild`, `channel`, `user`, `role`, or `message`.
- **[id]**: The ID of the object. This can be a name, an ID, or `ctx`. `ctx` automatically adjusts to the context of the user’s execution (this only works if Minicord.sh has a `ctx` attached to it).
- **[action]**: The action to perform on the object. This varies depending on the use case.
- **[params]**: Additional details for the action. This is usually required.

### What’s Up with `p`?
The `p` parameter is used to refer to the most recently created or modified object of a specified type. This allows for additional actions on the object without needing to re-specify its ID.

When using `p`, specify the object type first, followed by the action and its parameters. This enables efficient chaining of actions.
```
[object_type] p [action] [params]
```
`p` is temporary and is set to `None` when the execution is complete. If an action does not return a value to `p`, `p` remains unchanged.

### Limitations
- Regular `.sh` commands are not supported, as Minicord.sh is essentially translated into its interpreter’s actual language.
- File management is not supported, so you cannot execute `rm -rf` on the system.
- Information retrieval is not supported, as Minicord.sh is designed for executing actions rather than gathering data.

## Object Reference

### Guild
Represents a guild object.

**Actions:**
- **create_channel**: Creates a channel.
    **Parameters:**  
    `--name`: The name of the channel  
    `--type`: The type of the channel. Valid options are: `text`, `voice`  
    `--category`: The ID of the category under which the channel should be created (optional)  
    `--position`: The position of the channel in the channel list (integer)  
    `--nsfw`: Whether the channel is marked as age-restricted (true or false)  
    `--slowmode`: The slowmode setting in seconds  
    **`voice` exclusive:**
    `--bitrate`: The bitrate of the voice channel in **bits per second** (only for voice channels)  
    `--userlimit`: The maximum number of users allowed in the voice channel (only for voice channels)  
    **`p`:**
    The channel that has been created.
- **create_role**: Creates a role.
    **Parameters:**
	`--name`: The name of the role  
	`--color`: The color of the role in decimal format (e.g., `16711680` for red)  
	`--permissions`: The permissions bitmask (integer)  
	**`p`:**
	The role that has been created.

### Channel
Represents a channel object.

**Actions:**
- **send**: Sends a message to the channel.
    **Parameters:**
    `-m`: The content of the message (string)  
	**`p`:**
	The message sent.
- **edit**: Edits the channel's settings.
    **Parameters:**
    `--slowmode`: The slowmode setting in seconds (optional)  
    `--topic`: The new topic for the channel (optional)  
    `--name`: The new name of the channel (optional)  
    `--position`: The new position of the channel in the channel list (integer) (optional)  
    `--nsfw`: Whether the channel is marked as age-restricted (true or false) (optional)  
    `--category`: The new category ID for the channel (optional)  
    `--bitrate`: The new bitrate of the voice channel in **bits per second** (optional, only for voice channels)  
    `--userlimit`: The new maximum number of users allowed in the voice channel (optional, only for voice channels)  
	**`p`:**
	The channel that was edited.
- **delete**: Deletes the channel.
	**`p`:**
	Nothing.

### User
Represents a user object.

**Actions:**
- **ban**: Bans a user from the guild.
    **Parameters:**
    `-r`: The reason for banning (string)  
	**`p`:**
	Nothing.
- **kick**: Kicks a user from the guild.
    **Parameters:**
    `-r`: The reason for kicking (string)  
	**`p`:**
	Nothing.
- **timeout**: Times out a user.
    **Parameters:**
    `-d`: Duration of the timeout in minutes (integer)  
    `-r`: The reason for the timeout (string)  
    **`p`:**
	Nothing.

### Role
Represents a role object.

**Actions:**
- **assign**: Assigns a role to a user.
    **Parameters:**
    `-u`: The ID of the user to assign the role to  
	**`p`:**
	The assigned role.
- **revoke**: Revokes a role from a user.
    **Parameters:**
    `-u`: The ID of the user to revoke the role from  
	**`p`:**
	The revoked role.
- **edit**: Edits a role's settings.
    **Parameters:**
    `--name`: The new name of the role (optional)  
    `--color`: The new color of the role in decimal format (optional)  
    `--permissions`: The new permissions bitmask (integer) (optional)  
	**`p`:**
	The edited role.
- **delete**: Deletes the role.
	**`p`:**
	Nothing.

### Message
Represents a message object.

**Actions:**
- **edit**: Edits the content of a message.
    **Disclaimer:** You may only edit messages from the bot user, not from anyone else.
    **Parameters:**
    `-m`: The new content of the message (string)  
	**`p`:**
	The modified message.
- **delete**: Deletes a message.
	**`p`:**
	Nothing.

---
### Summary
That’s it! Feel free to subscribe to my YouTube channel.
