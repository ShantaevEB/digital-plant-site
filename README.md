# Сайт «Цифровой завод»: публикация на GitHub Pages

Статический сайт без сборщиков и внешних запросов: девять страниц (визитка, политика конфиденциальности, поддержка на ru/en/es), общий `assets/style.css`, иконка и скриншоты. Папку `docs/site/` целиком кладут в **отдельный публичный репозиторий** сайта: исходников игры в нём быть не должно.

## Что подставить до публикации

В страницах стоят три заглушки. Замените их во всех файлах одной командой (значения — свои; символ `|` в значениях не использовать):

```bash
cd docs/site
supportebsg@gmail.com="support@example.com"      # почта поддержки (она же контакт в политике)
Eduard Shantaev="Имя Фамилия"             # как в App Store Connect (продавец)
APP_STORE_URL="https://apps.apple.com/app/id0000000000"  # после выхода игры
find . -name '*.html' -exec sed -i '' \
  -e "s|supportebsg@gmail.com|$supportebsg@gmail.com|g" \
  -e "s|Eduard Shantaev|$Eduard Shantaev|g" \
  -e "s|APP_STORE_URL|$APP_STORE_URL|g" {} +
```

(`sed -i ''` — синтаксис macOS.) До выхода игры `APP_STORE_URL` не трогайте: кнопка «Скоро в App Store» ни на что не ведёт. После выхода подставьте ссылку и в трёх файлах `index.html` (ru, `en/`, `es/`) уберите у кнопки `aria-disabled="true"`; подпись под кнопкой («Ссылка появится после выхода игры» и её переводы) можно удалить.

Дата в политике (`privacy.html`, `en/privacy.html`, `es/privacy.html`) — 3 ноября 2026; перед подачей поставьте дату публикации.

## Шаги публикации

1. На github.com под профилем ShantaevEB создайте **публичный** репозиторий `digital-plant-site` (без README, лицензии и .gitignore).
2. На компьютере:

   ```bash
   mkdir digital-plant-site && cd digital-plant-site
   git init -b main
   cp -R /путь/к/digital-plant/docs/site/. .
   rm README.md   # необязательно: сайту эта инструкция не нужна
   git add . && git commit -m "Сайт игры «Цифровой завод»"
   git remote add origin git@github.com:ShantaevEB/digital-plant-site.git
   git push -u origin main
   ```

3. В репозитории: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, ветка `main`, папка `/ (root)`, **Save**.
4. Через минуту сайт откроется по адресу `https://shantaeveb.github.io/digital-plant-site/` (точный адрес написан на той же странице Settings → Pages).
5. Проверьте все девять адресов ниже и переключатель ru/en/es на телефоне. В репозитории не должно быть ничего, кроме содержимого `docs/site/`: ни папки `game/`, ни сейвов, ни ключей.

## Адреса для App Store Connect

Для репозитория `digital-plant-site` (иначе замените имя). `BASE` = `https://shantaeveb.github.io/digital-plant-site`:

| Поле в App Store Connect | ru (основной язык) | en | es |
| --- | --- | --- | --- |
| Маркетинговый URL | `BASE/` | `BASE/en/` | `BASE/es/` |
| URL политики конфиденциальности (обязательный) | `BASE/privacy.html` | `BASE/en/privacy.html` | `BASE/es/privacy.html` |
| URL поддержки (обязательный) | `BASE/support.html` | `BASE/en/support.html` | `BASE/es/support.html` |

Все три URL задаются на каждый язык карточки отдельно (политика — в «Информации о приложении», маркетинг и поддержка — в версии). Если какое-то поле у вас окажется одно на все языки, впишите адрес русской страницы: английская и испанская версии открываются из неё переключателем языка.

## Что в папке

```
index.html  privacy.html  support.html          ru
en/index.html  en/privacy.html  en/support.html
es/index.html  es/privacy.html  es/support.html
assets/style.css  icon-64.png  icon-512.png
assets/shots/{ru,en,es}/1…6.jpg                  скриншоты 540×1174 из docs/store/screenshots
```

Палитра сайта — палитра игры: фон `#1b1c1e`, панели `#222427`, акцент `#ff7a1a`, системный шрифт. Скриншоты на сайте — уменьшенные копии кадров магазина (`docs/store/screenshots/<язык>/1320x2868/`); при пересъёмке их нужно уменьшить заново.
