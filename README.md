import discord
import time

client = discord.Client()
bot = discord.Client()

@client.event
async def on_ready():
    print("ON")
    await client.change_presence(game=discord.Game(name='Heróis do Olimpo', type=1, url='https://www.twitch.tv/hentai%27),status=%27streaming%27)
    print("Nome do bot{}".format(client.user.name))
    print("Logado em {} servidores".format(len(client.servers)))
    print("---By Mahara----")
    @client.event
async def on_message(message):
    if message.content.lower().startswith('?msg'):
        role = discord.utils.get(message.server.roles, name='HeroisOlimpo')
        if not role in message.author.roles:
            embed1 = discord.Embed(title="SEM PERMISSÃO", description="Você precisa do cargo HeroisOlimpo", color = 0xff9c00)
            embed1.set_author(name="Heróis do Olimpo", icon_url="https://cdn.discordapp.com/attachments/457692671931056129/518579901947838474/tlx1.png%22)
            embed1.set_thumbnail(url="https://cdn.discordapp.com/attachments/449756826074873866/523624481827061761/HDO-ICON-B.png%22)

            embed1.set_footer(text="Heróis do Olimpo")
            return await client.send_message(message.channel, embed=embed1)
        msg = message.content.strip('?msg')
        x = list(message.server.members)
        s = 0
        for member in x:
            embed1 = discord.Embed(title="Aviso Do Servidor:Heróis do Olimpo", url="", color=0xff0000,description=' <@{}> {}'.format(member.id, msg))
            embed1.set_author(name="", icon_url="https://cdn.discordapp.com/attachments/449756826074873866/523624481827061761/HDO-ICON-B.png%22)
            embed1.set_thumbnail(url="https://cdn.discordapp.com/attachments/449756826074873866/523624481827061761/HDO-ICON-B.png%22)
            embed1.set_image(url="https://media.giphy.com/media/TTONt7IeqcGKQ/giphy.gif%22)try:
                await client.send_message(member, embed=embed1)
                print(member.name)
                s += 1
            except:
                pass
        print('\nAviso enviado para {} membros de {}'.format(s, len(x)))
    elif message.content.lower().startswith('?avatar'):
        try:
            membro = message.mentions[0]
            avatarembed = discord.Embed(
                title="",
                color=0xff9c00,
                description="[Clique aqui para baixar a imagem](" + membro.avatar_url + ")"
            )
            avatarembed.set_author(name=membro.name)
            avatarembed.set_image(url=membro.avatar_url)
            avatarembed.set_footer(text="Heróis do Olimpo",
                                   icon_url="https://cdn.discordapp.com/attachments/449756826074873866/523624481827061761/HDO-ICON-B.png%22)
            await client.send_message(message.channel, f"{message.author.mention}", embed=avatarembed)
        except:
            avatarembed2 = discord.Embed(title="", color=0xff9c00,
                                         description="[Clique aqui para baixar a imagem](" + message.author.avatar_url + ")")
            avatarembed2.set_author(name=message.author.name)
            avatarembed2.set_image(url=message.author.avatar_url)
            avatarembed2.set_footer(text="Heróis do Olimpo",
                                    icon_url="https://cdn.discordapp.com/attachments/449756826074873866/523624481827061761/HDO-ICON-B.png%22)
            await client.send_message(message.channel, f"{message.author.mention}", embed=avatarembed2)
if message.content.lower().startswith("?info"):
            embed = discord.Embed(title="Heróis do Olimpo", description="", color=0xff7200)
            embed.add_field(name="Criador", value="Mahara#0286")
            embed.add_field(name='Server count', value='{}'.format(str(len(client.servers))))
            embed.add_field(name="Convite",
                            value="[:six_pointed_star:](https://discordapp.com/oauth2/authorize?client_id=442084326142771201&scope=bot&permissions=8)")
            await client.send_message(message.channel, embed=embed)


    if message.content.startswith('?server'):
        role = discord.utils.get(message.server.roles, name='❲:wrench:❯❯❯ BOT')
        serverinfo_embed = discord.Embed(color=0xff9c00)
        serverinfo_embed.set_thumbnail(url=message.server.icon_url)
        serverinfo_embed.set_footer(text=client.user.name, icon_url=client.user.avatar_url)
        serverinfo_embed.add_field(name="Nome:", value=message.server.name, inline=True)
        serverinfo_embed.add_field(name="Dono:", value=message.server.owner.mention)
        serverinfo_embed.add_field(name="ID:", value=message.server.id, inline=True)
serverinfo_embed.add_field(name="Cargos:", value=len(message.server.roles), inline=True)
        serverinfo_embed.add_field(name="Membros:", value=len(message.server.members), inline=True)
        serverinfo_embed.add_field(name="Criado em:", value=message.server.created_at.strftime("%d %b %Y %H:%M"))
        serverinfo_embed.add_field(name="Região:", value="Brazil")
        serverinfo_embed.set_footer(text="Mahara#0286",icon_url="https://cdn.discordapp.com/attachments/449756826074873866/523624481827061761/HDO-ICON-B.png%22)
        await client.send_message(message.channel, embed=serverinfo_embed)
    if message.content.lower().startswith('?ping'):
        timep = time.time()
        emb = discord.Embed(title='Aguarde', color=0xff9c00)
        pingm0 = await client.send_message(message.channel, embed=emb)
        ping = time.time() - timep
        pingm1 = discord.Embed(title='Pong!', description=':ping_pong: Ping - %.01f segundos' % ping,color=0xff9c00)
        await client.edit_message(pingm0, embed=pingm1)

    if message.content.lower().startswith('?perfil'):
        user = message.author
        server = message.server
        embedinfo = discord.Embed(title='Suas informaçoes:', color=0xff9c00, description='\n')
        embedinfo.set_thumbnail(url=user.avatar_url)
        embedinfo.add_field(name='Nome', value=user.name)
        embedinfo.add_field(name='Id usuario', value=user.id)
        embedinfo.add_field(name='Entrou em', value=user.joined_at.strftime("%d %b %Y %H:%M"))
        embedinfo.add_field(name='Jogando', value=user.game)
        await client.send_message(message.channel, embed=embedinfo)
    if message.content.lower().startswith('?ban'):
try:

        if not message.author.server_permissions.administrator:
            return await client.send_message(message.channel, ':warning:️Permissão insuficiente')
        author = message.author.mention
        user = message.mentions[0]
        await client.ban(user)
        await client.send_message(message.channel,"Usuario: {} Punido Pelos Deuses {}".format(user.mention, author))


      except  discord.errors.Forbidden:
          return await client.send_message(message.channel,':warning:️ Nao posso banir o administrador :{}'.format(user.mention))

client.run('NTIzNjI2MTE3OTU4MjA1NDUw.DvcRHA.YTw9Ve2e6WgiiBV3cyAK5sUYWaQ')
