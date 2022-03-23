# first_tg_bot
const TelegramBot = require('node-telegram-bot-api')
const token = '5255533223:AAEjdJlT0pa3E-m7QOB--xrSZk_wZNmUClg'

const bot = new TelegramBot(token, {polling: true});
const keyboard = [
    [
      {
        text: 'НАЗВАНИЕ ФИЛЬМОВ ТУТ', // текст на кнопке
        callback_data: 'COMMAND_NUM'
      }
    ]
  ];
bot.on('message', (msg) => {
    const text = msg.text
    console.log(msg);
    const chatId = msg.chat.id; //получаем идентификатор диалога, чтобы отвечать именно тому пользователю, который нам что-то прислал
    const username = msg.from.first_name;
    bot.sendMessage(chatId,'<b>Добро пожаловать,</b>' + username ,{parse_mode : "HTML"});
    bot.sendPhoto(chatId, 'https://incatalog.kz/uploads/posts/2021-12/1639227376_0371eced14d3a73eef8f0f024132ab95.jpeg' ,{caption : '🥤<strong>Все фильмы из ТикТока</strong>\n\nЖми на кнопку чтобы узнать названия фильмов ⤵️',  // прикрутим клаву
    reply_markup: {
        inline_keyboard: keyboard
    }, parse_mode : "HTML"} 
    )
    const name = msg.from.username;
    //bot.sendMessage(chatId, 'Фильмы по этой кнопке')
});

bot.on('callback_query', (query) => {
    const chatId = query.message.chat.id;
    if (query.data === 'COMMAND_NUM') { 
       bot.sendMessage(chatId, '📝 Для использования бота, вы должны быть подписаны на наши каналы:', 
       {reply_markup: {
        "inline_keyboard": [
            [
                {
                    "text": "Подписаться на канал 1✅",
                    "url": "https://t.me/joinchat/WPMJiWCvQLQt3ke9"
                }
            ],
            [
                {
                    "text": "Я пописался(ась)",
                    "callback_data": "nunu"
                }
            ]
        ]
    }
    }) 
    }
    if (query.data === 'nunu'){
      bot.sendMessage(chatId, 'Молодец')
    } 
}
  )
