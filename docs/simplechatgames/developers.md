---
sidebar_position: 5
---

# The Developer API

- [Repository Infomation](#repository-info)
  - [Maven](#maven)
  - [Gradle (Grooy)](#gradle-groovy)
- [Using the API](#using-the-api)

# Repository Info

{: .note}
Make sure to replace `VERSION` with the latest version. Shown on the image below
![Latest version](https://repo.epicebic.xyz/api/badge/latest/public/me/epic/chatgames?color=40c14a&name=SimpleChatGames)  
If you come across any issues or need help with anything, come to my [Discord](https://discord.com/invite/bpG46SDstM) or DM me directly `@epicebic`

## Maven
```xml
<repository>
<name>Epic's Maven Repository</name>
<url>https://repo.epicebic.xyz/public</url>
</repository>
```

```xml
<dependency>
<groupId>me.epic</groupId>
<artifactId>chatgames</artifactId>
<version>VERSION</version>
</dependency>
```

## Gradle (Groovy)
```groovy
maven {
    url = "https://repo.epicebic.xyz"
}
```

```groovy
compileOnly('me.epic:chatgames:VERSION')
```

# Using the API

## plugin.yml setup

In order for your plugin to load correctly and add content to SimpleChatGames, it must be loaded after SimpleChatGames in your `plugin.yml` file. \
If your plugin requires SimpleChatGames to work add `depend: [SimpleChatGames]` \
If it can function without it use `soft-depend: [SimpleChatGames]`
## Creating your game config

To create your game configuration, navigate to src/main/resources in your project and create a YAML file with a name that represents your game. For example, you can call it coolgame.yml.

Inside this YAML file, you need to define two required values: enabled and duration. Feel free to add any other custom values as needed. Here's an example of the structure:

```yaml
enabled: true
duration: 30 # This is in seconds
```

## Setting up your main class
New format (v2.0.0)
{: .label .label-green }

```java
import me.epic.chatgames.SimpleChatGames;
import me.epic.chatgames.spigotlib.utils.FileUtils;
import org.bukkit.configuration.file.YamlConfiguration;
import org.bukkit.plugin.java.JavaPlugin;

public class MyPlugin extends JavaPlugin {

    private SimpleChatGames simpleChatGames;

    @Override
    public void onEnable() {
        this.simpleChatGames = SimpleChatGames.getPlugin();
    }
    
    private void loadGameConfig() {
        File file = new File(getDataFolder(), "coolgame.yml");
        
        if (!this.getDataFolder().exists()) {
            this.getDataFolder().mkdirs();
        }
        
        if (!file.exists()) {
            this.saveResource("coolgame.yml", false);
        }
        
        simpleChatGames.getGameManager().registerGame(new CoolGameData(file));
    }
}
```

## Creating the Game Data
New format (v2.0.0)
{: .label .label-green }

```java
import me.epic.chatgames.games.ChatGame;
import me.epic.chatgames.games.GameManager;
import me.epic.chatgames.games.data.GameData;
import org.bukkit.configuration.file.YamlConfiguration;

public class CoolGameData extends GameData {

    public CoolGameData(File file) {
        super(super);
    }

    @Override
    public ChatGame<CoolGame> createGame(GameManager manager) {
        return new CoolGame(this, manager);
    }
}
```

## Creating the Game Class
New format (v2.0.0)
{: .label .label-green }

```java
import me.epic.chatgames.games.ChatGame;
import me.epic.chatgames.games.GameManager;
import me.epic.chatgames.spigotlib.Timings;
import me.epic.chatgames.utils.Utils;
import org.bukkit.Bukkit;
import org.bukkit.configuration.file.YamlConfiguration;
import org.bukkit.entity.Player;
import org.bukkit.event.player.AsyncPlayerChatEvent;

public class CoolGame extends ChatGame<CoolGameData> {

    private String answer = "";
    private YamlConfiguration gameConfig = gameData.getGameConfig();

    public CoolGame(CoolGameData data, GameManager manager) {
        super(data.getDuration(), manager, data);
    }

    @Override
    protected void start() {
        super.start();

        // Handle start logic
        // This includes loading your questions, choosing a question, and setting the answer

      super.sendDebugAnswer(this.answer);
      Timings.startTimings("coolgame-chatgame");
    }

    @Override
    protected void win(Player player) {
        super.win(player);

        // Handle win logic
      
        Utils.giveRewardAndNotify(manager.getPlugin(), player, gameData, Timings.endTimings("coolgame-chatgame"));
        answer = "";
    }

    @Override
    protected void end(boolean timeout) {
        super.end(timeout);

        // Handle timeout logic
    }

    @Override
    public void handleChat(AsyncPlayerChatEvent event) {
        if (event.getMessage().equals(answer)) {
            win(event.getPlayer());
        }
    }
}
```