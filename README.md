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
import disnake
from disnake.ext import commands
import datetime

bot = commands.Bot("!")

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
  embed=disnake.Embed(title="Title embed", description="Description embed", color=0xff0000, timestamp=datetime.datetime.now())
  embed.set_author(name="Name author", icon_url="https://discord.com/assets/e93667acdd3212c58dabd580cf175504.svg", url="https://github.com/timeigerpy")
  embed.set_footer(text="Text in footer", icon_url="https://discord.com/assets/e93667acdd3212c58dabd580cf175504.svg")
  embed.set_thumbnail(url="https://discord.com/assets/e93667acdd3212c58dabd580cf175504.svg")
  embed.add_field(name="Text for field", value="Description field", inline=True)
  embed.set_image(url="https://assets-global.website-files.com/5f9072399b2640f14d6a2bf4/615e08a57562b757afbe7032_TransparencyReport_BlogHeader.png")
  await ctx.send(content="text", embed=embed)
  
bot.run("place token you bot")
```





