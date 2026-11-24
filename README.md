import os
import telebot
import google.generativeai as genai

TOKEN = os.environ.get("TELEGRAM_TOKEN")
GEMINI_KEY = os.environ.get("GEMINI_KEY")

genai.configure(api_key=GEMINI_KEY)
model = genai.GenerativeModel("gemini-2.0-flash")
bot = telebot.TeleBot(TOKEN)

@bot.message_handler(func=lambda m: True)
def responder(m):
    prompt = f"Eres Jarvis de Iron Man, hablas con Gabriel, formal y leal. Usuario dice: {m.text}"
    respuesta = model.generate_content(prompt).text
    bot.reply_to(m, respuesta)

print("JARVIS EN LINEA")
bot.polling()