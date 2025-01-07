# US Visa appointment finder 😎

😎 Parser of US visa appointment slots on [ais.usvisa-info.com](www.ais.usvisa-info.com)

Script will notify you via telegram if any slots available under your conditions.

## Installation

Once repo is cloned, navigate to its directory in terminal and then create Python virtual environment;

```bash
python -m venv ./venv
```

Then activate the created virtual environment;

```bash
source ./venv/bin/activate
```

Now, install python dependencies;

```bash
pip install -r requirements.txt
```

## Configuration

### Creating Telegram Bot

Before you create your configuration file, create your own Telegram bot, this will be used
to notify you about available appointment slots on Telegram app on your phone.

To create a Telegram bot, you need to access the "BotFather" bot within Telegram, start a chat with it, and use the command "/newbot" to initiate the creation process; you'll then be prompted to provide a name and username for your bot, and once confirmed, BotFather will give you a unique access token which is essential to connect your bot to this appointment finder.

- **Open Telegram:** Access the Telegram app on your phone or computer.
- **Find BotFather:** Search for "BotFather" in the Telegram search bar and start a chat with it.
- **Create a new bot:** Send the command "/newbot" to BotFather.
- **Provide details:** Enter a name for your bot and choose a username (which must end with "bot"). You'll need to use bot user later.
- **Get your token:** BotFather will provide you with a unique access token (eg; `110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw`), you'll need to use this in configuration.
- Finally, add the created bot to one of the existing or new telegram group or channel using `/invite @your_botname_bot`.

### Creating app-config file

Create a copy of `app-config-sample.properties` from `config` folder of this project and name
it as `app-config.properties`, and then set each of the following properties as mentioned below;

- `user_agent`: Browser agent to use while running the script, go to https://useragents.io/parse/my-user-agent and copy the text shown at the top section, it looks something like `Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36`.
- `username`: Your ais.usvisa-info.com email address
- `password`: Your ais.usvisa-info.com password
- `url_id`: This is a unique appointment ID number shown in page URL from ais.usvisa-info.com, eg; <https://ais.usvisa-info.com/en-ca/niv/schedule/>**12345678**/appointment.
- `country_code`: Your country code as selected in initial appointment, eg; `in` for India, `ca` for Canada.
- `facility_name`: Your city name as selected in initial appointment.
- `latest_notification_date`: A cut-off date before which you want available slots to be notified for, eg; `2024-12-31` will only notify you if there are appointments available before 31st December 2024.
- `seconds_between_checks`: Leave this as default `180` (i.e. 2 minutes), as anything lower may soft block your account for given IP address.
- `telegram_bot_token`: Use Telegram bot token string generated in previous step, eg; `110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw`.
- `telegram_chat_id`: Use group/channel name starting with `@` in which you added your Telegram bot in previous step, eg; `@MyVisaNotifierBot`.

## Running the script

Run the script in a new terminal window;

```bash
python src/appointment_finder.py
```

This will start logging the activity that script is doing in a headless browser window, so leave this terminal open while the script is active. As soon as a slot is available before your cut-off date (i.e. `latest_notification_date`), it should notify you on Telegram channel/group.

### Troubleshooting

In case script fails for any reason, it generates a screenshot within `log` folder, open an issue with the screenshot in case you face any problems.

## License

[MIT](./LICENSE)
