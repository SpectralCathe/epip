# Net
The `Net` library offers wrapper methods to make working with network messages easier. Its main feature is automatically stringifying messages, removing the need to do so explicitly when using tables.

Additionally, `Net.RegisterListener()` provides a way to register net listeners with IDE hints for the function parameters. This is done by defining a class with the name of the net message, for example:
```lua
---@class EPIPENCOUNTERS_Vanity_ApplyAura : NetMessage, Net_SimpleMessage_NetID
---@field AuraID string
---@field BoneID string

Net.RegisterListener("EPIPENCOUNTERS_Vanity_ApplyAura", function(payload)
    -- The payload variable here will be of the type EPIPENCOUNTERS_Vanity_ApplyAura and offer auto-completion!
end)
```

Additionally, for purposes of semantic clarity, a `NetMessage` class exists for denoting net events. Several other net message classes are defined with commonly used fields like `CharacterNetID`. You may have your net message classes inherit from these to reduce annotation duplication and to clarify the class's purpose as a net message.

<doc package="NetLib">



## Methods

#### Broadcast



```lua
function Net.Broadcast(channel, message, excludedChar)
```



Sends a message to all peers.



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>channel</b> <code>`T`</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>message</b> <code>T?</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>excludedChar</b> <code>GUID?</code> </p>

#### PostToCharacter



```lua
function Net.PostToCharacter(char, channel, message)
```



Sends a message to the user that currently controls char. Fails if char is a summon.



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>char</b> <code>Character|GUID|NetId</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>channel</b> <code>`T`</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>message</b> <code>T?</code> </p>

#### PostToUser



```lua
function Net.PostToUser(user, channel, message, excludedChar)
```



Sends a message to a user.



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>user</b> <code>UserId</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>channel</b> <code>`T`</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>message</b> <code>T</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>excludedChar</b> <code>GUID?</code> </p>

#### PostToOwner



```lua
function Net.PostToOwner(char, channel, message)
```



Sends a message to the owner of char. Use if you suspect the char might be a summon.



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>char</b> <code>Character</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>channel</b> <code>string</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>message</b> <code>any</code> </p>

#### RegisterListener



```lua
function Net.RegisterListener(channel, func)
```



Wrapper for Ext.RegisterNetListener that parses json payloads and fires an event afterwards.



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>channel</b> <code>`T`</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>func</b> <code>fun(payload:`T`)</code> </p>

#### PostToServer



```lua
function Net.PostToServer(channel, message)
```



Sends a message to the server.



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>channel</b> <code>`T`</code> </p>



<p style="margin-bottom:0px;"><span style="color:#b04a6e;"><b><i>@param</i></b></span> <b>message</b> <code>T?</code> </p>
</doc>