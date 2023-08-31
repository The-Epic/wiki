---
sidebar_position: 2
---

#  Commands

- [Reward Commands](#reward-commands)
- [Leaderboard](#leaderboard)
- [Reload](#reload)
- [Skip](#skip)

## Reward Commands

The reward sub-command (`/cg reward`) allows you to configure various types of rewards for your players. After executing any of the following commands, kindly remember to [reload](#reload) the plugin to apply the changes.

{: .note}
Should any of the following commands tell you that the item was added but the reward is disabled, follow the next guide

### Setting Item Rewards


**Quick Use**
Hold the item you want and run `/cg reward set item`

**Extended Guide**

To add an item reward, please follow this guide:

1. Create or obtain the item you want for the reward.
2. Hold the item in your main hand (By default the right hand).
3. Run the command `/cg reward set item`.

### Adding Command Rewards

**Quick Use**
Figure out your command, replace any player names needed with `%player_name%` and run `/cg reward set command cmdhere` without a starting slash

**Extended Guide**

1. Determine the desired command (e.g., `/give MyName diamond 16`).
2. Write the command `/cg reward set command`, `%player_name%` and remove the beginning slash.
   For example, if the command is `/give MyName diamond 16`, the full command would be `/cg reward set command give %player_name% diamond 16`.

### Adding Economy Rewards

**Quick Use**
Run `/cg reward set economy <amount>` and just replace `<amount>` with how much you want to be given

**Extended Guide**
For economy rewards, it is required to have the Vault plugin installed. Confirm its on the server with the `/plugins` command.

1. Run the command `/cg reward set economy <value>`, where `<value>` means the desired amount. For example, `/cg reward set economy 100` would grant players 100 units of your chosen currency.


### Enabling and Disabling Rewards

The enable and disable sub-commands facilitate reward management.

To enable a reward, run the command `/cg reward enable <reward>`, replacing `<reward>` with a valid option of "item", "command" or "economy"

To disable a reward, run the command `/cg reward disable <reward>`

### Clearing Rewards

The `/cg reward clear` command is designed to remove all defined rewards and then also disables them. In most cases this will never be used

## Leaderboard

The leaderboard command (`/cg leaderboard`) displays the current rankings based on answered questions.

You have the option to execute the command as-is to view the existing leaderboard, which includes player names and their total correct answers. Or you can specify a page number, such as `/cg leaderboard 2`, to access results for a specific page.

## Reload

The reload command (`/cg reload`) effectively refreshes the plugin, updating all game configurations, including the plugin's config and messages config. It is advised to execute this command after modifying rewards or altering questions, answers, messages, or game duration settings.

## Skip

The skip command (`/cg skip`) grants you the ability to bypass the current question and reveal its answer in the chat. Once ran, the plugin will automatically send a new random question from the available games.