import os, datetime, asyncio, requests, random
from bs4.element import TemplateString
from bs4 import BeautifulSoup
from dotenv import load_dotenv
from discord.ext import commands 
from discord import ButtonStyle, Member, Embed, Interaction, SelectOption
from discord.ui import Button, View

load_dotenv() ### loads the .env file containing the token
client = commands.Bot()

@client.event ### shows if rosabot is connected 
async def on_ready(): ### if this doesn't print then there is an error
    print(f'{client.user} has connected to Discord!')

### list of commands 
@client.slash_command(name="rosa",
description="rosa")
async def rosa(ctx):
    await ctx.response.send_message("rosa")
@client.slash_command(name='trans',
description='trans rights!!!',)
async def trans(ctx):
    await ctx.response.send_message(
    ':transgender_flag: :transgender_flag: :transgender_flag:')
@client.slash_command(name="rosa_daily",
descripton='sends rosa daily')
async def schedule_daily_message(ctx):
	await ctx.response.send_message('rosa set')
	while True:
		now = datetime.datetime.now()
		then = now+datetime.timedelta(days=1)
		#then = now.replace(hour=10, minute=6) ### for testing
		wait_time = (then-now).total_seconds()
		await asyncio.sleep(wait_time)
		await ctx.send('rosa')
		break
@client.slash_command(name='rosa_git',
description='provides a link to rosabot\'s git')
async def git(ctx):
	await ctx.response.send_message("rosa")
	git_link = Button(label='github', style=ButtonStyle.link, 
	url='https://github.com/rosa4646/rosabot')
	myview = View(timeout=180)
	myview.add_item(git_link)
@client.slash_command(name='user',
description='gives stats and data for a user')
async def Profile(ctx, user: Member=None):
	await ctx.response.send_message("rosa")
	if user == None:
		user = ctx.author
	inline = True
	embed=Embed(title=user.name+'#'+user.discriminator, color=0x0080ff)
	userData = {
		'Mention' : user.mention,
		'Username': user.display_name,
		'Created at' : user.created_at.strftime('%b %d, %Y, %T'),
		'Joined at' : user.joined_at.strftime('%b %d, %Y, %T'),
		'Server' : user.guild,
		'Top Role' : user.top_role
	}
	for [field_name, field_val] in userData.items():
		embed.add_field(name=field_name+':', value=field_val, inline=inline)
	embed.set_footer(text=f'id: {user.id}')
	embed.set_thumbnail(url=user.display_avatar)
	await ctx.send(embed=embed)
@client.slash_command(name='server',
description='displays stats of the server')
async def server(ctx):
	await ctx.response.send_message("rosa")
	guild = ctx.author.guild
	embed=Embed(title=guild.name, color=0x0080ff)
	server_data = {
		'Owner' : guild.owner.mention,
		'Channels' : len(guild.channels),
		'Members' : guild.member_count,
		'Created at' : guild.created_at.strftime('%b %d, %Y, %T')
	}
	for [field_name, field_val] in server_data.items():
		embed.add_field(name=field_name+':', value=field_val, inline=True)
	embed.set_footer(text=f'id: {guild.id}')
	embed.set_thumbnail(url=guild.icon)
	await ctx.send(embed=embed)
@client.slash_command(name='google',
description='displays the most googled thing as of today')
async def google(ctx):
	url = f"https://trends.google.com/trends/trendingsearches/daily?geo=US"
	req = requests.get(url)
	soup = BeautifulSoup(req.text, "lxml")
	most_googled = soup.find('span', attrs={"title": "titlePart in titleArray"})
	searches =  soup.find('div', attrs={"class": "search-count-title"})
	message = (f'the most googled thing is {most_googled} with {searches}')
	await ctx.response.send_message(message) 
	print(requests.get(url).text)
@client.slash_command(name='cat',
description='displays the cat')
async def cat(ctx):
	images = [
		'https://media.discordapp.net/attachments/756726989439893584/1009570778355859466/20220817_171143.jpg?width=349&height=465',
		'https://media.discordapp.net/attachments/979044087640510496/1010220300077641888/20220816_140937.jpg?width=349&height=465',
		'https://cdn.discordapp.com/attachments/979044087640510496/1010220357527027722/20220814_105435.jpg',
		'https://media.discordapp.net/attachments/979044087640510496/1010220392293601340/20220813_135352.jpg?width=349&height=465',
		'https://media.discordapp.net/attachments/979044087640510496/1010220452003721397/20220811_101043.jpg?width=349&height=465'
	]
	response = random.choice(images)
	await ctx.response.send_message(response)
	
if __name__ == '__main__': ### gets the discord token and runs it
    client.run(os.getenv("BOT_TOKEN"))
