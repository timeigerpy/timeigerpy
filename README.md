# Hello my names is Vyacheslav, i delevoper on disnake.py
## Bio my
#### My project:
> Liquid bot
> 
> Liquid Tools

#### Contact me
>
>   Discord:  
>>    TimEiger#4524
>  


#### My server:

  - [`Liquid Community`](https://discord.gg/Tk9R9CH8Z3)

# Example bot on disnake.py
## pip

> write in console
>> `py -m pip install disnake`
> 

## Code
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
  
bot.run("place token you bot")
```





