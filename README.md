# H




# from telebot import types
# import telebot
# import webbrowser
# import random
# import requests
# import re
# from bs4 import BeautifulSoup
# import click

# URL = "http://94.237.50.242:53878"
# def get_html_of(url):
#     resp = requests.get(url)

#     if resp.status_code != 200:
#         print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
#         exit(1)

#     return resp.content.decode() #контент


# def get_all_words_from(url):
#     test = get_html_of(url)
#     soup = BeautifulSoup(test, 'html.parser')
#     raw_text = soup.get_text()
#     return re.findall(r'\w+', raw_text)


# def count_occurrences_in(word_list, min_length):
#     word_count = {}

#     for word in word_list:
#         if len(word) < min_length:
#             continue
#         if word not in word_count:
#             word_count[word] = 1
#         else:
#             current_count = word_count.get(word)
#             word_count[word] = current_count + 1
#     return word_count

# text = get_all_words_from(URL)
# text1 = count_occurrences_in(text,4)
# fin = sorted(text1.items(), key=lambda item:item[1], reverse=True)
# print(fin)



# @click.command()
# @click.option('--url', '-u', prompt='Web URL', help='URL of webpage to extract from.')
# @click.option('--length', '-l', default=0, help='Minimum word length (default: 0, no limit).')
# def main(url, length):
#     text1 = count_occurrences_in(text,4)
#     fin = sorted(text1.items(), key=lambda item:item[1], reverse=True)

#     for i in range(10):
#         print(fin[i][0])

# if __name__ == '__main__':
#     main()


import click 
import requests
from bs4 import BeautifulSoup
import re



def get_text(url):
    res = requests.get(url)
    if res.status_code != 200:
        print(f'Status error {res.status_code}')
        exit(1)
    return res.content.decode()
    

def clean_text(url):
    text = get_text(url)
    clean_texts = BeautifulSoup(text, 'html.parser')
    final = clean_texts.get_text()
    result = re.findall(r'\w+',final)
    return result


def count_count_occurrences_in(wordlist,min_length):
    word_count = {}
    for word in wordlist:
        if len(word) < min_length:
            continue
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count[word]
            word_count[word] = current_count + 1
    return word_count
    

@click.command()
@click.option('--url','-u',prompt='Select the URL', help='You need to choise --url')
@click.option('--length','-l',default=4, help='Default is 1 ')

def main(url,length):
    a = clean_text(url)
    c = count_count_occurrences_in(a,length)
    sss = sorted(c.items(),key=lambda item: item[1], reverse=True)
    print(sss)

if __name__ == '__main__':
    main()








# def get_html_of(url):
#     resp = requests.get(url)

#     if resp.status_code != 200:
#         print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
#         exit(1)

#     return resp.content.decode()

# html = get_html_of(PAGE_URL)
# soup = BeautifulSoup(html, 'html.parser')
# raw_text = soup.get_text()
# all_words = re.findall(r'\w+', raw_text)

# word_count = {}

# for word in all_words:
#     if word not in word_count:
#         word_count[word] = 1
#     else:
#         current_count = word_count.get(word)
#         word_count[word] = current_count + 1

# top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True) 

# for i in range(10):
#     print(top_words[i][0])


# bot = telebot.TeleBot('7607757986:AAFsXtKEPWFCzQDJONsQTfb0hU4EerJg154')


# @bot.message_handler(commands=['start'])
# def main(message):
#     markup = types.InlineKeyboardMarkup()
#     btn1 = types.InlineKeyboardButton('Игра=±±Орел и Решка±±', callback_data='play')
#     markup.row(btn1)
#     btn2 = types.InlineKeyboardButton('Удалить последнее сообщение:', callback_data='delete')
#     btn3 = types.InlineKeyboardButton('Изменить текст', callback_data='edit')
#     markup.row(btn2,btn3)
#     bot.send_message(message.chat.id, 'Привет, вот список команд', reply_markup=markup)
#     file = open('./photo.jpeg', 'rb')
#     bot.send_photo(message.chat.id, file)
#     bot.register_next_step_handler(message,on_click)

# def on_click(message):
#     if message.text == 'плей':
#         bot.send_message(message.chat.id, 'Игра запущена')
#     elif message.text == 'edit':
#                 bot.send_message(message.chat.id, 'Текст изменен')



# @bot.callback_query_handler(func=lambda callback:True)
# def flip_coin(callback):
#     result = random.choice(['Орел','Решка'])
#     if callback.data == 'play':
#         bot.send_message(callback.message.chat.id, f'Результат: {result}' )



# bot.polling(non_stop=True)
    
# @bot.message_handler(commands=['start'])
# def start_game(message):
#     markup = types.InlineKeyboardMarkup()
#     play_button = types.InlineKeyboardButton('Играть', callback_data='play')
#     markup.add(play_button)
#     bot.send_message(message.chat.id, "Привет! Нажми 'Играть', чтобы подбросить монетку.", reply_markup=markup)

# @bot.callback_query_handler(func=lambda callback: True)
# def flip_coin(callback):
#     markup = types.InlineKeyboardMarkup()
#     play_button = types.InlineKeyboardButton('Играть', callback_data='play')
#     markup.add(play_button)
#     result = random.choice(['Орел', 'Решка'])
#     if callback.data == 'play':
#         bot.send_message(callback.message.chat.id, f"Результат: {result}", reply_markup=markup)

# bot.polling(non_stop=True)



# @bot.message_handler(commands=['start'])
# def button(message):
#     markup = types.ReplyKeyboardMarkup()
#     btn1 = types.KeyboardButton('Перейти на сайт')
#     markup.row(btn1)
#     btn2 = types.KeyboardButton('Удалить фото ')
#     btn3 = types.KeyboardButton('Изменить')
#     markup.row(btn2,btn3)
#     bot.send_message(message.chat.id, 'Привет', reply_markup=markup)



# @bot.message_handler(content_types=['photo'])
# def get_picture(message):
#     markup = types.InlineKeyboardMarkup()
#     btn1 = types.InlineKeyboardButton('Перейти на сайт ', url='http://pornhub.com/')
#     markup.row(btn1)
#     btn2 = types.InlineKeyboardButton('Удалить фото ', callback_data='delete')
#     btn3 = types.InlineKeyboardButton('Изменить', callback_data='edit')
#     markup.row(btn2,btn3)
#     bot.reply_to(message, 'Какое красиво фото!', reply_markup=markup)

# @bot.callback_query_handler(func=lambda callback: True)
# def callback_func(callback):
#     if callback == 'delete':
#         bot.delete_message(callback.message.chat.id, callback.message.message_id)
#     elif callback == 'edit':
#         bot.edit_message_text('Edit message',callback.message.chat.id, callback.message.message_id -1) 

# # @bot.message_handler(commands=['start'])
# # def main(message):
# #     bot.send_message(message.chat.id, f'Hello! {message.from_user.first_name}')

# @bot.message_handler(commands=['whoami'])
# def main(message):
#     bot.send_message(message.chat.id, f'Hello {message.from_user.first_name} I\'m bot who created from Max!')

# @bot.message_handler()
# def main(message):
#     if message.text.lower == 'привет':
#         bot.send_message(message.chat.id, f'Hello {message.from_user.first_name}')

# bot.polling(non_stop=True)
    



