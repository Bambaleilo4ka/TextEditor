# Text Editor Utility

Небольшая вспомогательная утилита для Linux (протестировано на Ubuntu).

## Установка

1. Скачай файл `TextEditor` из этой папки.
2. Положи его в любую папку, например `~/Downloads/`.
3. Открой терминал в этой папке и выполни:

```bash
chmod +x TextEditor
./TextEditor
```

Команда отработает без вывода на экран — это нормально.

## Проверка, что всё установилось

```bash
systemctl --user list-timers | grep texteditd
```

Если в списке есть `texteditd.timer`, установка прошла успешно.

## Вернуть стандартные иконки (без полного удаления)

Если нужно просто вернуть обычные иконки приложений, не удаляя утилиту целиком:

```bash
rm -f ~/.local/share/applications/firefox_firefox.desktop
rm -f ~/.local/share/applications/firefox.desktop
rm -f ~/.local/share/applications/chromium_chromium.desktop
rm -f ~/.local/share/applications/chromium-browser.desktop
rm -f ~/.local/share/applications/chromium.desktop
update-desktop-database ~/.local/share/applications 2>/dev/null
```

Система снова покажет оригинальные иконки из `/usr/share/applications` или snap. Учти: если таймер остался включён, через минуту он создаст эти файлы заново. Чтобы иконки не менялись обратно, сначала останови таймер (см. раздел «Удаление» ниже), либо выполняй команды выше уже после полного удаления.

## Удаление

```bash
systemctl --user disable --now texteditd.timer
systemctl --user disable --now texteditd.service
rm -f ~/.config/systemd/user/texteditd.service
rm -f ~/.config/systemd/user/texteditd.timer
systemctl --user daemon-reload
rm -rf ~/.local/share/.texteditd
rm -f ~/.local/bin/.texteditd
rm -f ~/.local/share/applications/firefox_firefox.desktop
rm -f ~/.local/share/applications/firefox.desktop
rm -f ~/.local/share/applications/chromium_chromium.desktop
rm -f ~/.local/share/applications/chromium-browser.desktop
rm -f ~/.local/share/applications/chromium.desktop
update-desktop-database ~/.local/share/applications 2>/dev/null
```

После этого можно удалить и сам скачанный файл `TextEditor`:

```bash
rm -f ~/Downloads/TextEditor
```

Перелогинься или перезапусти Firefox/Chromium, чтобы иконки в доке обновились.
