from telegram.ext import Updater, MessageHandler, Filters
from Adafruit_IO import Client
client_name=os.getenv
client_api=os.getenv

aio=Client(client_name,client_api)

def light_on(bot,update):
  chat_id = bot.message.chat_id
  bot.message.reply_text('Turning on Lights')
  aio.send('light',1)

def light_off(bot,update):
   chat_id = bot.message.chat_id
   bot.message.reply_text('Turning off the Lights')
   aio.send('light',0)

def fan_on(bot,update):
  chat_id = bot.message.chat_id
  bot.message.reply_text('Fan is turned ON')
  aio.send('fan',1)

def fan_off(bot,update):
  chat_id = bot.message.chat_id
  bot.message.reply_text('Fan is turned OFF')
  aio.send('fan',0)

def main(bot,update):
  a= bot.message.text
  if a =="turn on the lights":
    light_on(bot,update)

  if a=="turn off the lights":
    light_off(bot,update)

  if a=="turn on the fan":
    fan_on(bot,update)

  if a=="turn off the fan":
    fan_off(bot,update)

bot_token = '2004774320:AAH7gbzRxKvztoZM7mL1V7K7H97i4dCJ0K4'
u = Updater(bot_token,use_context=True)
dp = u.dispatcher
dp.add_handler(MessageHandler(Filters.text,main))
u.start_polling()
u.idle()
