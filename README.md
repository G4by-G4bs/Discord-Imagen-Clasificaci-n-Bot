import discord 
from discord.ext import commands


# Configuración de Intents
intents = discord.Intents.default()  
intents.message_content = True  # Necesario para leer los contenidos de los mensajes


bot = commands.Bot(command_prefix="!", intents=intents)


# Diccionario de imágenes asociadas a palabras clave
imagenes = {
    "HOLA!": "images/hola.jpg",    # Imagen para "HOLA!"
    "ADIOS!": "images/adios.jpg",  # Imagen para "ADIOS!"
    "GRACIAS!": "images/gracias.jpg"  # Imagen para "GRACIAS!"
    "SALVENME!": "images/salvenme.jpg"  # Imagen para "SALVENME!"
    "XD!": "images/xd.jpg"  # Imagen para "XD!"
    
}


@bot.event
async def on_ready():
    print(f"¡Bot {bot.user.name} está listo y funcionando!")


@bot.event
async def on_message(message):
    if message.author == bot.user:
        return  # Ignorar mensajes enviados por el bot


    # Obtén el contenido del mensaje y conviértelo a mayúsculas para comparación
    contenido = message.content.upper()


    # Verifica si el mensaje corresponde a una imagen conocida
    if contenido in imagenes:
        # Envía la imagen asociada
        with open(imagenes[contenido], "rb") as img_file:
            imagen = discord.File(img_file)
            await message.channel.send(file=imagen)
    else:
        # Responde si no puede procesar la información
        await message.channel.send("Lo siento.. no puedo procesar esa información.")


# Reemplaza "TU_TOKEN_AQUI" con tu token
bot.run("token)
