#!/bin/bash
set -e
MAIN_PATH="/var/www"

#Проверяем есть ли архив и не создана ли уже дирректория с проектом
#Если архива нет, или дирректория существует - скрипт прерывается
if [ ! -f $MAIN_PATH/project*.zip ]; then
echo -e "Архив не найден!\nПиздуй проверять $MAIN_PATH/"
exit 1
fi

if [ $(ls $MAIN_PATH/ | grep -c ^project*) -gt "1" ]; then
echo -e "У тебя в $MAIN_PATH/ уже несколько архивов или распакованных папок с проектом, а должен быть один архив!\nПиздуй проверять $MAIN_PATH/"
exit 1
fi

#Объявляется функция для html
for_html() {
  mkdir "/var/www/backups/html_bak_$(($(ls -1d /var/www/backups/html_bak_* | cut -c 27- | sort -n | tail -n1) + 1))" 2>/dev/null |
  cp -r /var/www/html/ "/var/www/backups/html_bak_$(($(ls -1d /var/www/backups/html_bak_* | cut -c 27- | sort -n | tail -n1) + 1))"
  echo "Забэкапил в $MAIN_PATH/backups OK"
  result=`7z x $MAIN_PATH/project* -o"$MAIN_PATH/" 2>/dev/null` && echo "Распаковал в $MAIN_PATH/ OK" || echo 'Не распаковал FAIL';  echo $result
  rm -rf $MAIN_PATH/$page/{css,files,images,js,page*.html,404.html}
  cp -r $MAIN_PATH/project*/{css,files,images,js,page*.html,404.html} $MAIN_PATH/$page/
  cp $MAIN_PATH/$page/page*.html $MAIN_PATH/$page/index.html
}

#Объявляется функция для services
for_services() {
  mkdir "/var/www/backups/services_bak_$(($(ls -1d /var/www/backups/services_bak_* | cut -c 31- | sort -n | tail -n1) + 1))" 2>/dev/null |
  cp -r /var/www/services/ "/var/www/backups/services_bak_$(($(ls -1d /var/www/backups/services_bak_* | cut -c 31- | sort -n | tail -n1) + 1))"
  echo "Забэкапил в $MAIN_PATH/backups OK"
  result=`7z x $MAIN_PATH/project* -o"$MAIN_PATH/" 2>/dev/null` && echo "Распаковал в $MAIN_PATH/ OK" || echo 'Не распаковал FAIL';  echo $result
  rm -rf $MAIN_PATH/$page/{css,files,images,js,page*.html,404.html}
  cp -r $MAIN_PATH/project*/{css,files,images,js,page*.html,404.html} $MAIN_PATH/$page/
  cp $MAIN_PATH/$page/page*.html $MAIN_PATH/$page/index.html
}


echo "Введи имя страницы которую необходимо обновить:"
read page

if [[ $page == "html" ]] ||
   [[ $page == "html/avans" ]] ||
   [[ $page == "html/cargo-owner" ]] ||
   [[ $page == "html/carrier" ]] ||
   [[ $page == "html/v1" ]] ||
   [[ $page == "html/v2" ]] ||
   [[ $page == "services" ]] ||
   [[ $page == "services/analytics" ]] ||
   [[ $page == "services/avans" ]] ||
   [[ $page == "services/free-ts" ]] ||
   [[ $page == "services/insurance" ]] ||
   [[ $page == "services/mobile-app" ]]; then

case $page in
  html)
  for_html;;

  html/avans)
  for_html;;

  html/cargo-owner)
  for_html;;

  html/carrier)
  for_html;;

  html/v1)
  for_html;;

  html/v2)
  for_html;;

  services)
  for_services;;

  services/analytics)
  for_services;;

  services/avans)
  for_services;;

  services/free-ts)
  for_services;;

  services/insurance)
  for_services;;

  services/mobile-app)
  for_services;;

esac
else
  echo "$page - такая страница не существует или ты опечатался"
  exit 1
fi

#Подчищаем за собой мусор
rm -r $MAIN_PATH/project*
