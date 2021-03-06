# Coding Our Discord Bot

## Discord Bot Applications

### Disregarding our own messages

A quirk of using an API that propagates every text message is that our bot will recieve its own messages! Before we add functionality to our bot, we will add a condition that ensures that we don't try to process the messages that we send ourselves.

```python
async def on_message(self, message):
    if message.author == self.user:
        return
```

This compares the snowflake ID of the message author to our bot ID. If the two are equal, we do nothing.

### Respond to messages from users

```python
async def on_message(message):
	if message.content.startswith('$hello'):
		await message.channel.send('Hello World!')
```

Another thing you can do with discord bots is use them to respond to messages from users based on what the message says. In this example, we are telling the bot to respond to a message beginning with "hello" with "Hello World!"


### Welcome new users to discord server

```python
async def on_member_join(member):
    await member.create_dm()
    await member.dm_channel.send(
        f'Hi {member.name}, welcome to my Discord server!'
    )
```

The other function here, `on_member_join()`, tells the program what to do when a new member joins the server. When the function is called, the program will wait for the member argument to create a direct message channel to communicate with the bot. When that's done, a greeting will be sent to the user before the function returns.

### Handling errors

```python
async def on_message(message):
    if message.author == client.user:
    if message.content == 'HackBU is the best club ever':
        response = "Duh"
        await message.channel.send(response)
    elif message.content == 'raise-exception':
        raise discord.DiscordException
```

Lastly, you can use the discord API to raise errors based on user input. In this example, if a user types 'raise-exception' in the chat bar and hits send, the bot will respond by raising an exception.

If you want to experiment, feel free to mess around with the message you use to raise an exception. You can also raise exceptions in any function by adding the line `raise discord.DiscordException` so have fun with it!


### If you're curious to check out some other things you can do with discord bots, feel free to check out the documentation here: https://discordpy.readthedocs.io/en/stable/api.html. Happy hacking!
