# AuroraHuntersBot
Java written Telegram Bot, which helps photographers catch northern lights.
## About the project
## What this bot do?

## Buld and run

### Prerequisites:

Linux machine with 1+ Gb RAM (CentOS 7,8 tested. Any other distributive which supported required software versions may used);

PostgreSQL 10+ installed;

java-1.8.0-openjdk or oracle Java 8 installed (both tested);

maven installed; (yum install maven on CentOS 7-8)

git installed; (yum install git on CentOS 7-8)

### Installation:

AuroraHunters telegramBot installation may take up to 15 minutes.

`ssh username@yourserver`

Once you have logged to the server, clone the project to desirable directory (I used my user home subdirectory):

`git clone https://github.com/erdees/AuroraHuntersBot.git `

When repository cloned, cd to project folder:

`cd AuroraHuntersBot/`

And perform build process:

`mvn clean install`

Project build may take up to 5 minutes depends on the Internet connection speed and server performance. When building will be finished you will see the following message:

[INFO] ------------------------------------------------------------------------\
[INFO] BUILD SUCCESS\
[INFO] ------------------------------------------------------------------------\
[INFO] Total time: 01:27 min\
[INFO] Finished at: 2020-08-14T01:30:05+03:00\
[INFO] ------------------------------------------------------------------------

It means that maven downloaded all dependences and already built .jar file. with our bot. To see .jar with bot, cd to target subdirectory which appears once build finished:

`cd target/`

You will se some files in the folder, including “AuroraTelegramBot-1.0-SNAPSHOT-jar-with-dependencies.jar”. This file is our bot. You may leave it in the same folder or move/copy to a different place depending on your preferences. In this example, I’ll leave it here. Bot has a configuration file, which should be completed before starting the bot:

`mv config.properties.example config.properties`

Edit configuration file with your parameters.

`vim config.properties`

And replace example variables by yours:

db.host = jdbc:postgresql://127.0.0.1:5432/yourdbname //postgresql host, port and database name\
db.login = yourdbuser //database user\
db.password = yourdbpassword //database password\
bot.username = @botusername //telegram bot username\
bot.token = YOUR-TELEGRAM-APIKEY //telegram bot api key\
bot.site = yoursite.com //project website. this parameters will put watermarks on generated by bot graphics

After save and exit. Once it done, make sure, that PostgreSQL up and running and the database, its user and password created correctly. In case, if database is unavailable or its credentials is wrong, bot will not start and return an error. 

Last thing we should do, is to make the bot automatically up and running when operating system starts. To do it, we need to create systemd .service file which you can copy and configure from root repository folder:

`cp Aurora.service /etc/systemd/system/`

Edit required parameters in the .service file.

`vim  /etc/systemd/system/Aurora.service`

Change the bot working directory where .jar file located, for example: 

`WorkingDirectory=/opt/bots/AuroraTelegramBot`

Once done, check java parameters with required quantity of RAM for working application. I recommend to configure it with 128GB, but I have tested it with 32Gb and it worked without any problems. 128Gb is preferable to receive generated graphs faster. An example of this parameter:

`ExecStart=/bin/java -Xms128m -Xmx128m -jar AuroraTelegramBot-1.0-SNAPSHOT-jar-with-dependencies.jar`

If you have changed anything in .service file, please reload a configuration by using following command:

`systemctl daemon-reload`

To add the bot to autostart, use the command:

`systemctl enable Aurora`

and finally, to start the bot:

`systemctl start Aurora`

Now the bot up and running, you are beautiful. 

## Bot Usage
