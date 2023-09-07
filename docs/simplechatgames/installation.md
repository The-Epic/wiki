---
sidebar_position: 1
---

# Installation

To begin using the SimpleChatGames plugin, follow these easy installation steps:

## Step 1: Downloading

Start by downloading the plugin from SpigotMC. You can find the plugin at [SimpleChatGames](https://www.spigotmc.org/resources/simplechatgames.108655/). Once downloaded, save it to your local `Downloads` folder.

## Step 2: Adding to Your Server

Upload or Transfer the plugin to your plugins folder, if you need extra help follow this guide [https://docs.papermc.io/paper/adding-plugins](https://docs.papermc.io/paper/adding-plugins) 

Once that's done restart your server.

## Step 3: Adding Rewards

### Item Reward

To set an item as a reward, hold the item you want to use in your hand and run the command `/cg reward set item`.

### Command Reward

You can configure multiple command rewards. For example, if you want to run the command `/give %player_name% diamond 16` as a reward, use the command `/cg reward set command give %player_name% diamond 16`. For other commands, type the command and use `%player_name%` where the name is required, without adding a starting slash.

### Currency Reward

**Note: This feature requires Vault to work. Make sure you have Vault installed along with an economy plugin that supports it.**

To add a currency reward, run the command `/cg reward set economy <value>`, replacing `<value>` with the desired amount.

:::info
Once you have followed any of the instructions above, run the command `/cg reload` to load the rewards and start using SimpleChatGames.
:::