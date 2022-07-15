# Example bot on disnake.py

## Pages:
- [`Downlad python`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#download-python)
  - [`Pip`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#pip)
- [`Docs`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#documentation)
- [`Code bot`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#code)
  - [`Cogs bot`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#code)
  - [`Sub command`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#sub-commands)
- [`Author`](https://github.com/timeigerpy/timeigerpy/blob/main/example-bot.md#authors)

## Download python
 - `Windows`
   - [`Windows 64-bit`](https://www.python.org/ftp/python/3.10.4/python-3.10.4-amd64.exe)
   - [`Windows 32-bit`](https://www.python.org/ftp/python/3.10.4/python-3.10.4.exe)
 - `macOS`
   - [`macOS 64-bit universal`](https://www.python.org/ftp/python/3.10.4/python-3.10.4-macos11.pkg)
 - `Other`
   - [`More links`](https://www.python.org/downloads/release/python-3912/)

## pip

> write in console
>> `py -m pip install disnake`

## Documentation
[`Click here`](https://docs.disnake.dev/en/latest/api.html)

## Code
```py
#import
import disnake
from disnake.ext import commands
import datetime
from disnake.utils import format_dt
#virable bot
bot = commands.Bot("!")

#on_ready
@bot.event
async def on_ready():
  print("bot is online")

#error handler
@bot.event
async def on_slash_command_error(interaction, error)
  await interaction.response.send_message(error)

@bot.event
async def on_command_error(ctx, error):
  await ctx.reply(error)

#slash command

@bot.slash_command(name="ping", description="Description about command")
async def command_1(inter):
  ping = int(bot.latency * 1000)
  await inter.response.send_message(f"🏓 Pong!\nMy ping: *{ping}*")
 
#simple command

@bot.command()
async def ping(ctx):
  ping = int(bot.latency * 1000)
  await ctx.reply(f"🏓 Pong!\nMy ping: *{ping}*")

#embed
@bot.command()
async def embed_command(ctx):
  embed=disnake.Embed(title="Title embed",
  description="Description embed",
  color=0xff0000,
  timestamp=datetime.datetime.now())
  
  embed.set_author(name="Name author",
  icon_url="https://images-ext-1.discordapp.net/external/Yi1GiOrRbG2DjdrOmkBygRriz1LCjk4FMyoD7ZJBlgw/%3Fv%3D4/https/avatars.githubusercontent.com/u/100599959", url="https://github.com/timeigerpy")
  
  embed.set_footer(text="Text in footer",
  icon_url="https://discord.com/assets/e93667acdd3212c58dabd580cf175504.svg")
  
  embed.set_thumbnail(url="https://images-ext-1.discordapp.net/external/Yi1GiOrRbG2DjdrOmkBygRriz1LCjk4FMyoD7ZJBlgw/%3Fv%3D4/https/avatars.githubusercontent.com/u/100599959")
  
  embed.add_field(name="Text for field",
  value="Description field",
  inline=True)
  
  embed.set_image(url="https://assets-global.website-files.com/5f9072399b2640f14d6a2bf4/615e08a57562b757afbe7032_TransparencyReport_BlogHeader.png")
  
  await ctx.send(content="text", embed=embed)
  
#ephemeral command
@bot.slash_command(name="ephemeral_command")
async def command_2(inter):
  embed=disnake.Embed(title="Example command", description="Example ephemeral command", color=0x0000ff)
  await inter.response.send_message(content="ephemeral command!", embed=embed, ephemeral=True)
    
#option command
@bot.slash_command(name="option_command", description="Example option command")
async def command_3(inter, string: str, number: int, ephemeral: bool):
    embed=disnake.Embed(title="Example Option command", description=f"str: {string}\nnumber: {number}")
    if ephemeral == True:
        await inter.response.send_message(embed=embed, ephemeral=True)
    elif ephemeral == False:
        await inter.response.send_message(embed=embed, ephemeral=False)
    else:
        return
        
#virable command
@bot.slash_command(name="virable_example", description="Example virable command")
async def command_4(inter, member: disnake.User):
  name_author = member
  date_cr1 = format_dt(member.created_at, 'D')
  date_cr = format_dt(member.created_at, 'R')
  embed=disnake.Embed(title=f"Info {name_author}", description=f"Created date: {date_cr1}({date_cr})")
  embed.set_thumbnail(url=member.avatar)
  await inter.response.send_message(embed=embed)
  

bot.run("place token you bot")
```
## Cogs bot
### main.py
```py
#import
import disnake
from disnake.ext import commands
import datetime
#virable bot
bot = commands.Bot("!")

#on_ready
@bot.event
async def on_ready():
  print("bot is online")

#error handler
@bot.event
async def on_slash_command_error(interaction, error)
  await interaction.response.send_message(error)

@bot.event
async def on_command_error(ctx, error):
  await ctx.reply(error)

bot.load_extension('command.test')

bot.run("place token you bot")
```
### command/test.py
```py
import disnake
from disnake.ext import commands
import datetime



bot = commands.Bot("!")

class TestCommand(commands.Cog):
  def __init__(self, bot: commands.Bot):
        self.bot = bot

  @bot.slash_command(name="cogs_example", description="Example cogs command")
  async def command(self, inter):
    await inter.response.send_message("Example cogs command!")
    

def setup(bot: commands.Bot):
    bot.add_cog(TestCommand(bot))
print(f"> Extension {__name__} is ready\n----------\n")
```

### Sub commands
```py
import disnake
from disnake.ext import commands

bot = commands.Bot("!")

@bot.command(name="sub_example", description="Sub command example")
async def test(inter):
  print("!")
  
@test.sub_command(name="sub_commands", description="Sub command example")
async def commands1(inter):
  embed=disnake.Embed(title="Example sub command", description="it's sub command")
  await inter.response.send_message(embed=embed)

bot.run('place token your bot')

```

### Command "Bot thinks"
```py
import disnake
from disnake.ext import commands

bot = commands.Bot("!")
  
@bot.command(name="Bot thihks", description="Example!!")
async def commands_bot(inter):
  await inter.response.defer()
  
  #here you can do anything while the bot is thinking
  
  embed=disnake.Eembed(description="Example!", color=0x6a00ff)
  await inter.followup.send(content=f"{inter.author}", embed=embed)

bot.run('place token your bot')

```

### Economy command
```py
#import
import sqlite3
import disnake
import random
from disnake.ext import command

bot = commands.Bot("!", test_guild=[id_you_server])

db = sqlite3.connect("db.db")
saa = db.cursor()

sql.execute(f"""CREATE TABLE IF NOT EXISTS users (
    id BIGINT,
    cash BIGINT,
)""")

def create(id: int):
    sql.execute(f"SELECT id FROM users WHERE id = ?", (id,))
    if sql.fetchone() is None:
        sql.execute(f"INSERT INTO users VALUES (?, ?,)", (id, 10))
        db.commit()
    else:
        return
    db.commit()

@bot.slash_command(description="Check you balance!")
async def balance(inter):
  id = inter.author.id
  create(id)
  for value in sql.execute("SELECT cash FROM users WHERE id = ?", (id,))
    embed=disnake.Embed(title=f"Balance: {inter.author.name}", description=f"{value[0]}")
    await inter.response.send_message(embed=embed)

@bot.slash_command(description="Casino")
async def casino(inter, money: int):
  if money < 0:
    await inter.response.send_message("Please enter a number greater than `0`")
  else:
    id = inter.author.id
    create(id)
    for value in sql.execute("SELECT cash FROM users WHERE id = ?", (id,))
      if value[0] < money:
        await inter.response.send_message("you don't have that much money!")
      else:
          rand = random.randint(1,2)
          if rand == 1:
            value1 = value[0] + money
            sql.execute("UPDATE users SET bit = {int(value1)} WHERE id = '{id}'")
            await inter.response.send_message("Congratulations you have won!")
          elif rand == 2:
            value1 = value[0] - money
            sql.execute("UPDATE users SET bit = {int(value1)} WHERE id = '{id}'")
            await inter.response.send_message("Alas, you lost :(")
          else:
            await inter.response.send_message("Error!")
     
```

## Authors:
> Main delevopers:
>> TimEiger#4524
>
> Comming soon...
