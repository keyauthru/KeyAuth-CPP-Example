# KeyAuth-CPP-Пример

Пример KeyAuth C++ для https://keyauth.ru система аутентификации.

Исходный код статической библиотеки для KeyAuth находится здесь https://github.com/KeyAuth/keyauth-cpp-library

## **Ошибки**

Если пример по умолчанию, не добавленный в ваше программное обеспечение, работает неправильно, пожалуйста, присоединяйтесь к серверу Discord https://discord.gg/keyauth и отправьте сообщение о проблеме в канале `#ошибки`.

Однако мы **НЕ** предоставляем поддержку для добавления KeyAuth в ваш проект. Если вы не можете в этом разобраться, вам следует воспользоваться Google или YouTube, чтобы узнать больше о языке программирования, на котором вы хотите продавать программу.

## **Методы обеспечения безопасности**

* Используйте обфускацию, предоставляемую такими компаниями, как VMProtect или Themida (также используйте их SDK для большей защиты)
* Проводите частые проверки целостности заготовки, чтобы убедиться, что память программы не была изменена
* Не записывайте байты загруженного вами файла на диск, если вы не хотите, чтобы этот файл был извлечен пользователем. Скорее, запустите файл в памяти и сотрите его из памяти в тот момент, когда выполнение завершится

*KeyAuth предоставляется в виде исходного кода. Бремя защиты на стороне клиента лежит на вас, разработчике программного обеспечения, как и в случае с любой системой аутентификации.*

## Лицензия на авторское право

KeyAuth лицензирован по **эластичной лицензии 2.0**

* Вы не имеете права предоставлять программное обеспечение третьим лицам в качестве размещенного или управляемого
сервиса, если сервис предоставляет пользователям доступ к какому-либо существенному набору
особенности или функционал программного обеспечения.

* Вы не имеете права перемещать, изменять, отключать или обходить функциональные возможности лицензионного ключа
в программном обеспечении, а также вы не имеете права удалять или скрывать какие-либо функциональные
возможности программного обеспечения, защищенные лицензионным ключом.

* Вы не имеете права изменять, удалять или скрывать какие-либо уведомления о лицензировании, авторских правах или другие уведомления
лицензиара в программном обеспечении. Любое использование товарных знаков лицензиара регулируется
применимым законодательством.

Благодарим вас за ваше согласие, мы усердно работаем над разработкой KeyAuth и не одобряем нарушения наших авторских прав.

## **Проблемы с подключением клиента?**

Это распространено среди всех систем аутентификации. Запутывание программы приводит к ложным срабатываниям антивирусных сканеров, и с учетом масштаба проверки подлинности ключа это воспринимается как вредоносный домен. Итак, `keyauth.ru " были заблокированы многими интернет-провайдерами. для панели мониторинга, панели реселлера, панели клиента используйте `keyauth.ru `

Для API, `keyauth.ru "не сработает, потому что я намеренно заблокировал его там, так что `keyauth.ru "также не блокируется. Итак, вам следует создать свой собственный домен и следовать этому обучающему видео https://www.youtube.com/watch?v=a2SROFJ0eYc . В обучающем видео показано, как создать доменное имя на 100% бесплатно, если вы не хотите его приобретать.

## **Определение экземпляра `KeyAuthApp`**

Визит https://keyauth.ru/app / и выберите свое приложение, затем перейдите на вкладку **C++**

Это предоставит вам код, который вы должны заменить в [`main.cpp `](https://github.com/keyauthru/Key Файл Auth-PHP-Example/blob/main/main.cpp#L13-L16)

```cpp
std::string name = "example"; // application name. right above the blurred text aka the secret on the licenses tab among other tabs
std::string ownerid = "JjPMBVlIOd"; // ownerid, found in account settings. click your profile picture on top right of dashboard and then account settings.
std::string secret = "db40d586f4b189e04e5c18c3c94b7e72221be3f6551995adc05236948d1762bc"; // app secret, the blurred text on licenses tab and other tabs
std::string version = "1.0"; // leave alone unless you've changed version on website
std::string url = "https://keyauth.ru/api/1.2/"; // change if you're self-hosting

api KeyAuthApp(name, ownerid, secret, version, url);
```

## **Инициализировать приложение**

Вы должны вызвать эту функцию перед использованием любой другой функции проверки подлинности ключа. В противном случае другая функция аутентификации по ключу не будет работать.

```cpp
KeyAuthApp.init();
if (!KeyAuthApp.data.success)
{
	std::cout << skCrypt("\n Status: ") << KeyAuthApp.data.message;
	Sleep(1500);
	exit(0);
}
```

## **Отображение информации о приложении**

```cpp
std::cout << skCrypt("\n\n App data:");
std::cout << skCrypt("\n Number of users: ") << KeyAuthApp.data.numUsers;
std::cout << skCrypt("\n Number of online users: ") << KeyAuthApp.data.numOnlineUsers;
std::cout << skCrypt("\n Number of keys: ") << KeyAuthApp.data.numKeys;
std::cout << skCrypt("\n Application Version: ") << KeyAuthApp.data.version;
std::cout << skCrypt("\n Customer panel link: ") << KeyAuthApp.data.customerPanelLink;
```

## **Проверьте правильность сеанса**

Используйте это, чтобы узнать, вошел ли пользователь в систему или нет.

```cpp
std::cout << skCrypt("\n Checking session validation status (remove this if causing your loader to be slow)");
KeyAuthApp.check();
std::cout << skCrypt("\n Current Session Validation Status: ") << KeyAuthApp.data.message;
```

## **Проверьте статус черного списка**

Проверьте, внесен ли HWID или IP-адрес в черный список. Вы можете добавить это, если хотите, просто чтобы убедиться, что никто не сможет открыть вашу программу менее чем на секунду, если они занесены в черный список. Однако, если вы не возражаете, чтобы пользователь, занесенный в черный список, пользовался программой в течение нескольких секунд, пока он не попытается войти в систему и зарегистрироваться, и вы заботитесь о том, чтобы программа была максимально быстрой для ваших пользователей, тогда вам не следует использовать эту функцию. Если пользователь, внесенный в черный список, попытается войти в систему / зарегистрироваться, сервер проверки подлинности ключей проверит, внесен ли он в черный список, и, если да, отклонит вход. Таким образом, функция проверки черного списка - это просто вспомогательная функция, которая необязательна.

```cpp
if (KeyAuthApp.checkblack()) {
	abort();
}
```

## **Войдите в систему с помощью имени пользователя/пароля**

```cpp
std::string username;
std::string password;
std::cout << skCrypt("\n\n Enter username: ");
std::cin >> username;
std::cout << skCrypt("\n Enter password: ");
std::cin >> password;
KeyAuthApp.login(username, password);
if (!KeyAuthApp.data.success)
{
	std::cout << skCrypt("\n Status: ") << KeyAuthApp.data.message;
	Sleep(1500);
	exit(0);
}
```

## **Зарегистрируйтесь с помощью имени пользователя/пароля/ключа**

```cpp
std::string username;
std::string password;
std::string key;
std::cout << skCrypt("\n\n Enter username: ");
std::cin >> username;
std::cout << skCrypt("\n Enter password: ");
std::cin >> password;
std::cout << skCrypt("\n Enter license: ");
std::cin >> key;
KeyAuthApp.regstr(username, password, key);
if (!KeyAuthApp.data.success)
{
	std::cout << skCrypt("\n Status: ") << KeyAuthApp.data.message;
	Sleep(1500);
	exit(0);
}
```

## ** Обновить имя пользователя/ключ**

Используется для того, чтобы пользователь мог добавить дополнительное время к своей учетной записи, запросив новый ключ.

> **Предупреждение**
> Для обновления учетной записи пароль не требуется. Таким образом, в отличие от функций входа в систему, регистрации и лицензирования - вы не должны **** входить в систему пользователя после успешного обновления.

```cpp
std::string username;
std::string key;
std::cout << skCrypt("\n\n Enter username: ");
std::cin >> username;
std::cout << skCrypt("\n Enter license: ");
std::cin >> key;
KeyAuthApp.upgrade(username, key);
```

## **Войдите в систему, используя только лицензионный ключ**

Пользователи могут использовать эту функцию, если их лицензионный ключ никогда ранее не использовался и если он использовался ранее. Поэтому, если вы планируете просто разрешить пользователям использовать ключи, вы можете удалить функции входа в систему и регистрации из своего кода.

```cpp
std::string key;
std::cout << skCrypt("\n Enter license: ");
std::cin >> key;
KeyAuthApp.license(key);
if (!KeyAuthApp.data.success)
{
	std::cout << skCrypt("\n Status: ") << KeyAuthApp.data.message;
	Sleep(1500);
	exit(0);
}
```

## **Войдите в систему с помощью веб-загрузчика**

Попросите ваших пользователей войти в систему через веб-сайт. Обучающее видео здесь https://www.youtube.com/watch?v=9-qgmsUUCK4 вы также можете использовать свой собственный домен для клиентской панели, https://www.youtube.com/watch?v=iHQe4GLvgaE

```cpp
std::cout << "\n Waiting for user to login";
KeyAuthApp.web_login();
std::cout << "\n Waiting for button to be clicked";
KeyAuthApp.button("close");
```

## **Пользовательские данные**

Отображать информацию для текущего пользователя, вошедшего в систему.

```cpp
std::cout << skCrypt("\n User data:");
std::cout << skCrypt("\n Username: ") << KeyAuthApp.data.username;
std::cout << skCrypt("\n IP address: ") << KeyAuthApp.data.ip;
std::cout << skCrypt("\n Hardware-Id: ") << KeyAuthApp.data.hwid;
std::cout << skCrypt("\n Create date: ") << tm_to_readable_time(timet_to_tm(string_to_timet(KeyAuthApp.data.createdate)));
std::cout << skCrypt("\n Last login: ") << tm_to_readable_time(timet_to_tm(string_to_timet(KeyAuthApp.data.lastlogin)));
std::cout << skCrypt("\n Subscription name(s): ");
std::string subs;
for (std::string value : KeyAuthApp.data.subscriptions)subs += value + " ";
std::cout << subs;
std::cout << skCrypt("\n Subscription expiry: ") << tm_to_readable_time(timet_to_tm(string_to_timet(KeyAuthApp.data.expiry)));
```

## **Проверьте имя пользователя для подписки**

Если вы хотите запретить доступ к частям вашего приложения только определенным пользователям, у вас может быть несколько подписок с разными именами. Затем, когда вы создадите лицензии, соответствующие уровню этой подписки, пользователи, которые используют эти лицензии, получат подписку с названием подписки, соответствующим уровню используемого ими лицензионного ключа.

```cpp
for (std::string subs : KeyAuthApp.data.subscriptions)
{
	if (subs == "default")
	{
		std::cout << skCrypt("\n User has subscription with name: default");
	}
}
```

## **Переменные приложения**

Строка, которая хранится на стороне сервера Key Auth. На панели мониторинга вы можете выбрать для каждой переменной аутентификацию (доступ могут получить только зарегистрированные пользователи) или не аутентификацию (любой пользователь может получить доступ до входа в систему). Они являются глобальными и статичными для всех пользователей, в отличие от пользовательских переменных, которые будут рассмотрены ниже в этом разделе.

```cpp
// get data from global variable with name 'status'
std::cout << "\n status - " + KeyAuthApp.var("status");
```

## **Пользовательские переменные**

Пользовательские переменные - это строки, хранящиеся на стороне сервера Key Auth. Они специфичны для пользователей. Их можно установить на панели мониторинга на вкладке "Пользователи", через SellerAPI или через ваш загрузчик, используя приведенный ниже код. "discord" - это имя пользовательской переменной, по которому вы извлекаете пользовательскую переменную. `test#0001` - это данные переменной, которые вы получаете при извлечении пользовательской переменной.

```cpp
std::cout << "\n user variable - " + KeyAuthApp.getvar("discord"); // get value of the user variable 'discord'
```

И вот как вы извлекаете пользовательскую переменную:

```cpp
KeyAuthApp.setvar("discord", "test#0001"); // set the value of user variable 'discord' to 'test#0001'
```

## **Журналы приложений**

Может использоваться для регистрации данных. Хорошо подходит для предупреждений об отладке и, возможно, для отладки ошибок. Если вы настроите Discord webhook в настройках приложений панели мониторинга, он будет отправлять сообщения журнала на ваш Discord webhook, а не сохранять их на сайте. Рекомендуется установить Discord webhook, так как логи на сайте удаляются через 1 месяц после отправки.

Вы можете использовать функцию регистрации до входа в систему и после входа в систему.

```cpp
KeyAuthApp.log("user logged in"); // send event to logs. if you set discord webhook in app settings, it will send there instead of dashboard
```

## **Забанить пользователя**

Заблокируйте пользователя и внесите в черный список его HWID и IP-адрес. Хорошая функция для вызова, если вы используете защиту от отладки и обнаружили попытку вторжения.

Функция работает только после входа в систему.

```cpp
KeyAuthApp.ban();
```

## **Забанить пользователя (с указанием причины)**

Заблокируйте пользователя и внесите в черный список его HWID и IP-адрес. Хорошая функция для вызова, если вы используете защиту от отладки и обнаружили попытку вторжения.

Функция работает только после входа в систему.

Параметром reason будет причина запрета, отображаемая пользователю при попытке входа в систему и видимая на панели управления KeyAuth.

```cpp
KeyAuthApp.ban("Don't try to crack my loader, cunt.");
```

## **Веб-хуки на стороне сервера**

Обучающее видео https://www.youtube.com/watch?v=ENRaNPPYJbc

> **Примечание**
> > Прочитайте документацию по веб-ссылкам для проверки подлинности ключей здесь https://docs.keyauth.ru/website/dashboard/webhooks

Безопасно отправляйте HTTP-запросы по URL-адресам, не допуская утечки URL-адреса в вашем приложении. Вам обязательно следует использовать, если вы хотите отправлять запросы к Seller API из своего приложения, в противном случае, если вы этого не сделаете, вы передадите свой ключ продавца всем. И тогда кто-то может испортить ваше приложение.

```cpp
std::string resp = KeyAuthApp.webhook("Sh1j25S5iX", "&mak=best&debug=1");
if (!KeyAuthApp.data.success) // check whether webhook request sent correctly
{
	std::cout << skCrypt("\n\n Status: ") << KeyAuthApp.data.message;
	Sleep(1500);
	exit(0);
}
std::cout << "\n Response recieved from webhook request: " + resp;
```

## **Загрузить файл**

> **Примечание**
> > Ознакомьтесь с документацией по ключевым файлам аутентификации здесь https://docs.keyauth.ru/website/dashboard/files

Обеспечьте безопасность файлов, предоставив KeyAuth ссылку для скачивания вашего файла на панели управления KeyAuth. Убедитесь, что это прямая ссылка для скачивания (как только вы перейдете по ссылке, она начнет загружаться без вашего нажатия на что-либо). Функция загрузки KeyAuth предоставляет байты, а затем вы сами решаете, что с ними делать. В этом примере показано, как записать его в файл с именем `text.txt ` в той же папке, что и программа, хотя вы могли бы выполнить ее с помощью RunPE или чего угодно еще.

`362906` - это идентификатор файла, который вы получаете на панели мониторинга после добавления файла.

```cpp
// remember, certain paths like windows folder will require you to turn on auto run as admin https://stackoverflow.com/a/19617989
std::vector<std::uint8_t> bytes = KeyAuthApp.download("362906");
if (!KeyAuthApp.data.success) // check whether file downloaded correctly
{
	std::cout << skCrypt("\n\n Status: ") << KeyAuthApp.data.message;
	Sleep(1500);
	exit(0);
}
std::ofstream file("file.dll", std::ios_base::out | std::ios_base::binary);
file.write((char*)bytes.data(), bytes.size());
file.close();
```

## **Каналы чата**

Разрешите пользователям общаться между собой в вашей программе.

```cpp
KeyAuthApp.chatget("test");
for (int i = 0; i < KeyAuthApp.data.channeldata.size(); i++)
{
	std::cout << "\n Author:" + KeyAuthApp.data.channeldata[i].author + " | Message:" + KeyAuthApp.data.channeldata[i].message + " | Send Time:" + tm_to_readable_time(timet_to_tm(string_to_timet(KeyAuthApp.data.channeldata[i].timestamp)));
}
```

```cpp
std::cout << skCrypt("\n Type Chat message: ");
std::string message;
std::getline(std::cin, message);
if (!KeyAuthApp.chatsend("test", message))
{
	std::cout << KeyAuthApp.data.message << std::endl;
}
```

Вот пример ImGui https://github.com/KeyAuth-Archive/KeyAuth-Chat-ImGui-CPP

## **Изменение имени пользователя**

Разрешите пользователям изменять свое имя пользователя при входе в систему.

```cpp
std::cout << skCrypt("\n Change Username To: ");
std::string newusername;
std::cin >> newusername;
KeyAuthApp.changeusername(newusername);
if (KeyAuthApp.data.success) 
{
        std::cout << KeyAuthApp.data.message << std::endl;
}
```
