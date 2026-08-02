import json
from telegram import Update, ReplyKeyboardMarkup
from telegram.ext import Application, CommandHandler, MessageHandler, ContextTypes, filters
from config import BOT_TOKEN

FILE = "users.json"

def load_users():
    try:
        with open(FILE, "r", encoding="utf-8") as f:
            return json.load(f)
    except:
        return {}

def save_users(users):
    with open(FILE, "w", encoding="utf-8") as f:
        json.dump(users, f, ensure_ascii=False, indent=4)


async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = str(update.message.from_user.id)
    users = load_users()

    if user_id in users:
        lang = users[user_id]

        if lang == "uz":
            await update.message.reply_text(
                "👋 Assalomu alaykum!\n\n"
                "🛍 Miks Market Saudiya\n\n"
                "Kerakli bo‘limni tanlang:"
            )
        else:
            await update.message.reply_text(
                "👋 Здравствуйте!\n\n"
                "🛍 Miks Market Saudiya\n\n"
                "Выберите раздел:"
            )
    else:
        keyboard = [
            ["🇺🇿 O‘zbekcha"],
            ["🇷🇺 Русский"]
        ]

        await update.message.reply_text(
            "Tilni tanlang / Выберите язык:",
            reply_markup=ReplyKeyboardMarkup(
                keyboard,
                resize_keyboard=True
            )
        )


async def language(update: Update, context: ContextTypes.DEFAULT_TYPE):
    text = update.message.text
    user_id = str(update.message.from_user.id)

    users = load_users()

    if text == "🇺🇿 O‘zbekcha":
        users[user_id] = "uz"
        save_users(users)

        await update.message.reply_text(
            "✅ Til o‘zbekcha tanlandi.\n\n"
            "🛍 Miks Market Saudiya ga xush kelibsiz!"
        )

    elif text == "🇷🇺 Русский":
        users[user_id] = "ru"
        save_users(users)

        await update.message.reply_text(
            "✅ Язык выбран: русский.\n\n"
            "🛍 Добро пожаловать в Miks Market Saudiya!"
        )


def main():
    app = Application.builder().token(BOT_TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT, language))

    print("Bot ishga tushdi...")
    app.run_polling()


if __name__ == "__main__":
    main()
