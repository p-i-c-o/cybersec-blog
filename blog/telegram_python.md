# USING TELEGRAM FOR PYTHON
_Author: p-i-c-o_

## INTRO
_Telegrams' api gives hackers a new way to communicate with computers_

Telegrams' api has been used for many things, for example: Chat Bots, News and Updates, Content Delivery, and much much more. However, using Python and a small computer, a hacker can create a bot that can run malicious code.
Let's create one together.

### INSTALLATION
Because there are some issues with the current pip distribution of the python-telegram-bot, we need to install version 13.13 specifically:
`pip3 install python-telegram-bot==13.13`

### USAGE
We need a bot to use, start a new chat on telegram with the BotFather, and create a new bot and get its bot token. Make sure no one gets it as it would give them access to your bot. Save your chat id and your bot token somewhere safe.

Using a simple script, we can now create a script that communicates with a chat bot. Here it is:
```
# ---------------------------------------------
token = "INSERT YOUR TOKEN HERE"
correct_chat_id = "INSERT YOUR CHAT ID HERE"

from telegram import Bot, Update
from telegram.ext import Updater, MessageHandler, filters
import os, subprocess


help_count = 0



avail_commands = """Available commands:
*Test 1:* Tests the script
*Run <command>:* runs a command through the terminal on the host"""

# ------------------ FUNCTIONS ------------------
def run_shell_command(command):
  result = subprocess.run(command, shell=True, capture_output=True, text=True)
  return result.stdout

def echo(update: Update, context) -> None:
    message = update.message
    reply = None
    # ------------------ Predefined Responses ------------------
    if message.text == "Test 1":
      reply = "Success 1"
    # ----------------------------------------------------------
    if reply == None:
      help_count += 1
    bot = context.bot
    if reply != None:
      try:
        bot.send_message(chat_id=correct_chat_id, text=reply)
      except:
        bot.send_message(chat_id=correct_chat_id, text="⚠️ An error occured ⚠️")


if __name__ == "__main__":
    bot_token = token

    bot = Bot(token=bot_token)
    updater = Updater(bot=bot)
    dispatcher = updater.dispatcher
    echo_handler = MessageHandler(filters.Filters.text, echo)
    dispatcher.add_handler(echo_handler)

    updater.start_polling()
    updater.idle()

```

This script will simply reply "Success 1", when you send it "Test 1". Very simple. To create our own commands, use this format.
```
if message.text == <desired_input>:
  reply = <desired_response>
```
This script will only send the user something back nothing else.
