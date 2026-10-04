# Trigger Cards

![](README/tc-01.png)

Displays small interactive portraits of all group chat members on top of the chat input bar.



## Requirements

- [Costumes Plugin](https://github.com/LenAnderson/SillyTavern-Costumes.git) (server plugin) – **required** for changing costumes (`right click` on a trigger card). Without it, right-clicking a card fails with `Failed to retrieve costumes: 404 - Not Found`.

To install the server plugin:

1. Clone it into the `plugins` folder of your SillyTavern installation (not the extensions folder):
   ```
   cd SillyTavern/plugins
   git clone https://github.com/LenAnderson/SillyTavern-Costumes.git
   ```
2. Make sure `enableServerPlugins: true` is set in SillyTavern's `config.yaml`.
3. Restart the SillyTavern server (reloading the browser is not enough).



## Basic Usage

All settings are saved to the active chat.

- `/tc-on` to enable trigger cards.
- `/tc-off` to disable trigger cards.
- `/tc?` to show this help.
- `/tc-config` to open the settings menu for the active chat. You can also open it from the Extensions panel: **Trigger Cards** → **Open Settings**.

By default, a trigger card is created for each group member with the following actions:

*   `click` – trigger the character to speak
*   `shift + click` – unmute the character
*   `alt + click` – mute the character

To restore these default settings use `/tc-on reset=true`



## Images

Each card shows an expression sprite from the character's sprite folder (`data/<user>/characters/<name>/`).

- The expression `neutral` is used by default. Pick another one in the settings or with `/tc-on emote=joy`.
- If the selected expression has no image, the card falls back to `neutral`.
- Sprite folder overrides of the Character Expressions extension are honored. This also shows your persona's sprites when Prome's user sprite is active in a group chat.
- File types are tried in the order `png`, `webp`, `gif`.

`right click` on a card to pick a costume, i.e. a subfolder of the character's sprite folder (requires the Costumes plugin, see [Requirements](#requirements)).

> **Known issue:** SillyTavern's `/costume` command, which is used to apply the costume, always changes the character who wrote the last message, not the card you clicked. In group chats, only change the costume of the character who spoke last.



## Custom cards

Instead of the member list, you can use a custom list of cards by either providing the name of a Quick Reply set (the labels of the quick replies will be used as character names and to find the corresponding expression images, add `::qr` to the label to execute the quick reply on click instead of the normal click action) or by providing a comma-separated list of names.

`/tc-on members=myQrSet`

`/tc-on Name1, Name2, Name3`



## Custom actions

To use another set of actions on the cards, you can provide the name of a Quick Reply set.

`/tc-on actions=myQrSet`

In the quick replies you can use `{{arg::name}}` to get the character's name.

`/trigger {{arg::name}}`

The quick replies should be labeled as follows (use the title field in the additional options dialog for the tooltip on the trigger card):

*   (empty label) – click (if you are using a QR set as member list, not providing this QR will result in a click calling the QR's command)
*   `c` – ctrl + click
*   `s` – shift + click
*   `a` – alt + click
*   `cs` – ctrl + shift + click
*   `ca` – ctrl + alt + click
*   `sa` – shit + alt + click
*   `csa` – ctrl + shift + alt + click
