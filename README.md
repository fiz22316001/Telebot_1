# Telebot_1
import telebot
import requests
import json

TOKEN = "5413812581:AAHi8AJ35Bdy-SAenR0TLGmoOaiqrLh41KA"

bot = telebot.telebot("TOKEN")

keys = {
	'евро':'EUR',
	'доллар США':'USD',
	'российский рубль':'RUR',
}

class ConvertionException(Exception):
	pass


class Converter:
     @staticmethod
def convert(quote: str, base: str, amount: str):
	values = message.text.split(' ')

	if len(values) > 3:
		raise ConvertionException('Слишком много параметров.')


quote, base, amount = values

if quote == base:
	raise ConvertionException('Невозможно перевести одинаковые валюты {base}.')

try:
	quote_ticker = keys[quote]
except    KeyError:
	raise ConvertionException(f'Не удалось обработать валюту{quote}')

try:
	base_ticker = keys[base]
except    KeyError:
	raise ConvertionException(f'Не удалось обработать валюту{base}')

try:
	amount = float[amount]
except    ValueError:
	raise ConvertionException(f'Не удалось обработать валюту{quote}')



@bot.message_handler(commands=['start', 'help'])
def help(message: telebot.types.Message):
	text = 'Чтобы начать работу введите команду в следующем формате: n\<имя валюты>  \
		 <в какую валюту надо перевести> \
		 <количество переводимой валюты>\n Увидеть список всех доступных валют: /values'
	bot.reply_to(message, text)


@bot.message_handler(commands=['values'])
def help(message: telebot.types.Message):
	text = 'Доступные валюты'
	for key in keys.keys():
		'\n'.join(text,key, )
	bot.reply_to(message, text)


@bot.message_handler(content_types=['text', ])
def convert(message: telebot.types.Message):

	if len(values) != 3:
		raise ConvertionException('Слишком много параметров.')

	quote,base,amount = values
	total_base = Converter.convert(quote, base, amount)
	text = f'Цена {amount} {quote} в {base} - {total_base}'
	bot.send_message(message.chat.id, text)


bot.polling()
