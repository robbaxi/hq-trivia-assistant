# HQ trivia assistant

![Software License][ico-license]

A small bot to help aide you in picking the right answer in the HQ app trivia game. This small app hooks into HQ's websocket stream and automatically searches Google and Yahoo! for the correct answer using a variety of searches. 


## Install

``` bash
$ git clone https://github.com/mikealmond/hq-trivia-assistant .
$ cd hq-trivia-assistant
$ composer install
$ cp .env.dist .env
```
After you've created the `.env` file, fill in your HQ user ID and bearer token. You can find your ID and token by sniffing the web traffic from your phone using a tool such as [Charles Proxy](https://www.charlesproxy.com/).

Note: installation assumes that you have installed [Composer](https://getcomposer.org/doc/00-intro.md#globally) already.

## Usage

``` bash
$ php run.php
```


## Contributing

All contributions welcome.

## Credits

- [Mike Almond][link-author]
- [All Contributors][link-contributors]

## License

The MIT License (MIT)

[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[link-author]: https://github.com/mikealmond
[link-contributors]: ../../contributors


## Complete tutorial


Before starting few things: First of all you need to use Mac os (But it's possible on Windows too), have some kind of a text editor installed (atom, sublime text etc.) and between steps never close the terminal window. And this will not work on android 7.0+ and jailbreaked IPhones.

1. Install Charles Proxy (https://www.charlesproxy.com).

2. Install php 7.1 or later so open terminal and paste ``` curl -s https://php-osx.liip.ch/install.sh | -s 7.2 ``` (It will take few minutes to download and install) (press enter)

Make sure that the version is correct by typing ``` php -v ``` in terminal if php version is 5.6 or something similar type ``` export PATH=/usr/local/php5/bin:$PATH now ``` type ``` php -v ``` again and it should say php 7.2 or something similar

3. Create a folder anywhere

4. Download the hq-trivia-assistant repository and place it in your created folder.

5. Write cd press space and drag and drop your folder again (press enter)

6. Paste in ``` php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');" ```
(press enter)

7. Open your folder and there should be a file named composer.phar select it, press enter and then delete ``` bash .phar ``` extension (so it’s named only composer) and press enter

8. In terminal write php composer install (there shold now be a new folder named vendor in your folder)

9. Now open charles proxy you installed previously

•	Go to Proxy > Proxy Settings
•	In the Proxies tab enter "8888" in the HTTP Proxy Port field
•	Go to Proxy > SSL Proxying Settings
•	On the SSL Proxying tab check the checkbox for Enable SSL Proxying and configure a location. By default, Charles will only perform SSL proxying for specific domains you include in the list. To save listing all URLs you wish to inspect, you can use a location of . as a wildcard, and SSL proxying will be enabled for all domains
•	Next you have to identify your IP Go to System Preferences: Network: Wifi: Advanced: TCP/IP and make note of the IPV4 Address (e.g. 10.0.1.101). You will use this later.
•	Go to Help > SSL Proxying > Save Charles Root Certificate
•	Change the file type from the default ".pem" to ".cer" and save in a location you can find later e.g. desktop
•	Transfer the .cer file to your device

On android phones:
•	Open the file from a file manager such as File Commander. You will be prompted to save the certificate.
•	Give the certificate a name and Okay it as trusted (be sure to disable or remove it once you're done).
•	You are required to set up a PIN once the certificate is installed. A prompt will appear asking to set up a PIN. Add the new PIN.
•	Go to the Settings App > Wifi > Press and hold down the Wifi Network currently connected to. When the modal appears click Modify Network.
•	Select Show Advanced Options to reveal proxying options.
•	Under Proxy select Manual.
•	In the Proxy Host Name box enter the enter in the IPV4 Address you got from your computer.
•	In the Proxy Port Field enter the Port (8888), as you did when configuring Charles.
•	Save

On Samsung phones:
•	Open Charles certificate and instead of Vpn and apps select Wi-fi, press ok
•	Go to Settings > Wifi > Press and hold down the Wifi Network currently connected to. When the modal appears click Modify Network Config.
•	Select Show Advanced Options to reveal proxying options.
•	Under Proxy select Manual.
•	In the Proxy Host Name box enter in the IPV4 Address you got from your computer.
•	In the Proxy Port Field enter the Port (8888), as you did when configuring Charles.
•	Save

On Iphones:
•	Go to the Settings app, tap Wi-Fi, find the network you are connected to and then tap the blue disclosure arrow to configure the network. Scroll down to the HTTP Proxy setting, tap Manual.
•	enter in the IPV4 Address you got from your computer. And port 8888
•	Leave Authentication set to Off.
• Go to general - about - certificate trust settings and give Charles full root access. (Settings > General > About > Certificate Trust Testings)


Now open hq trivia app and get back to your computer

10. In terminal type ``` cp .env.dist .env ```

11. Open your folder and press cmd+shift+. (Don't forger the dot) To see hidden files. Locate .env file and open it with your text editor (text edit, atom, sublime text etc.)

12. In Charles find ``` https://api-quiz.hype.space ``` and expand it, locate folder named users and expand it, select a file named me, left click it and press Enable SSL proxying. Then go to contents

13. Locate the word ``` authorization ``` and next to it there is a very long string. Double click it and copy it, but don’t copy the word bearer just what comes after it and paste it into .env file right after ``` HQ_BEARER_TOKEN= ```

14. Select JSON Text below, There should be a string named userId and 8 numbers next to it. Copy them, and paste them into .env file next to ``` HQ_USER_ID= ```

After that’s done turn the proxy off on your phone ( On Samsung set proxy to none, on android device, open the Settings App then navigate to Security > Clear Credentials (all the way to the bottom). Click Clear credentials and confirm. Navigate to Settings > Lock Screen > Screen Lock and remove the PIN if desired. And On Iphone turn HTTP proxy to off)

And that’s it. Now when the game is starting type ``` php run.php ``` in terminal (always make sure you are in your hq assistant directory (if not type cd press space and drag and drop your folder) and everything should work just fine.
