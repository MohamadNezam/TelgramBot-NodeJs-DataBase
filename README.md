# TelgramBot-NodeJs-DataBase
 
# Setting up the bot

First, go to the telegram search bar and search **@botfather**. 
We are going to use this to get a token for our new bot.

There are several commands associated with **@botfather**, we are going to start with **/newbot** then provide the desired name for the bot. The name must always end with **‘bot’**. Now that we have the token we can write the code.

# The coding

Let’s first create a folder for our new project. 
Open the command line and navigate to the folder. 
Initialize the project by running the following commands to install telegraf:

```
npm init -y
```
```
npm install telegraf
```

Create a javascript file, app.js

```
const Telegraf = require('telegraf');

const bot = new Telegraf('insert_bot_token_here');
```
Let’s write a simple script that will welcome us every time we start the bot.
```
//method for invoking start command
 
bot.command('start', ctx => {
    console.log(ctx.from)
    bot.telegram.sendMessage(ctx.chat.id, 'hello there! Welcome to my new telegram bot.', {
    })
})
```

To add more functionality let’s write code that shows you images of animals when you click inline keyboard buttons. Create a res folder and add images into it.


```
//method that displays the inline keyboard buttons 

bot.hears('animals', ctx => {
    console.log(ctx.from)
    let animalMessage = `great, here are pictures of animals you would love`;
    ctx.deleteMessage();
    bot.telegram.sendMessage(ctx.chat.id, animalMessage, {
        reply_markup: {
            inline_keyboard: [
                [{
                        text: "dog",
                        callback_data: 'dog'
                    },
                    {
                        text: "cat",
                        callback_data: 'cat'
                    }
                ],

            ]
        }
    })
})

//method that returns image of a dog

bot.action('dog', ctx => {
    bot.telegram.sendPhoto(ctx.chat.id, {
        source: "res/dog.jpeg"
    })

})

//method that returns image of a cat 

bot.action('cat', ctx => {
    bot.telegram.sendPhoto(ctx.chat.id, {
        source: "res/cat.jpeg"
    })

})

```
