## RPG Enemies AI

RPG is the abbreviation of role-playing. Generally speaking, it includes three categories: action (real-time) role-playing; turn-based role-playing games; and chess role-playing. When encountering an enemy in these three types of games, it is the beginning of a battle. So, what mechanism does the enemy in the game operate according to? In other words, how does their AI (artificial intelligence) work? This brings sufficient room for the design of enemies in the game.

The operations of these enemies must simulate the thinking of the human brain to a certain extent. That is to say, under what circumstances, what kind of response and what kind of response should be more targeted and in line with certain logic. For example: an enemy with healing skills, when its health is running out, it should think out a response and heal itself. This is the logical coping part the designer has to give to the enemy AI design. At this time, we need to design a "path" for it. This "path" design includes:

### 1) Patrol path. 

When the enemy does not find the player, what is its walking range, and what route does the enemy follow within this walking range? This is the patrol path. The patrol path can be to let the enemy wait from a starting point to an end point; it can also be repeated back and forth or looped over a certain distance.

### 2) Scouting range and scouting conditions. 

The reconnaissance range can be understood as the vision of the enemy. The farther and wider the vision is, the easier it is to be found by the enemy when you are close to the enemy; on the contrary, if the enemy's vision is short-sighted, then you can be invisible to the enemy. Get closer to the enemy. Scouting conditions are a supplementary description of the scouting range. For example, the enemy's vision cannot pass through the wall, so if the player stands behind the wall, even if the enemy is within the detection range of the enemy, the enemy will not find the player. This is one of the conditions for reconnaissance.

### 3) Arrest path. 

When the enemy finds the player, what path does it take to capture it? This is also something to consider. If there are no obstacles between the enemy and the player before, then the enemy can directly approach the player. However, if there is an obstacle between the enemy and the player, or there is a difference in terrain, the enemy needs to take a detour to arrest the player.

"Reaction logic, limited response, and path" are the three main points of enemy AI design in role-playing games. By grasping the combination of these three points, you can work out an appropriate operating mechanism for the enemy.

***Let's look at a few examples:***


## Action RPG

![Image](https://github.com/YunqianAo/RPG-Enemies-AI/blob/main/picture/presentacion%20%E6%8B%B7%E8%B4%9D.jpg)





As shown above:

The dotted line is the enemy's patrol path, and the enemy patrols in a loop along this path. The gray trapezoid is the enemy's reconnaissance range. When the enemy walks to point B and the player just walks to point C (the initial position of the player is at point A), the enemy will find the player and attack.

1) Suppose the enemy has 100HP and 100MP, the normal attack damages 5HP, one attack every 2 seconds, the skill attack damages 10HP, consumes 50MP, and the interval between two skills is 4 seconds. The player has 100HP, normal attacks damage 5HP, and they attack every 1 second.



The enemy's judgment response is to create as much damage as possible for the player, so the skill attack will be launched as soon as the skill attack interval expires. So:

The player will cause 100HP (5HP*20) damage to the enemy within 20 seconds, causing the enemy to die.

The enemy will cause 25HP (5HP*5) normal attack damage and 20HP (10HP*2) skill damage to the player in the first 10 seconds; since MP has been exhausted, the enemy cannot perform skills in the next 10 seconds. Attack, so it will only cause 25HP (5HP*5) normal damage; in 20 seconds, it will cause a total of 70HP damage to the player.



2) Assuming that the enemy has 100HP and 100MP, the normal attack damage is 5HP, and it attacks once every 2 seconds. The skill healing can restore 20HP for itself, consume 50MP, and the interval between two skills is 8 seconds. The player has 100HP, normal attacks damage 5HP, and they attack every 1 second.



The enemy's judgment response is to heal itself when it is less than or equal to 1/4 in addition to attacking the player. So:

The player deals 75HP (100HP*3/4) damage to the enemy, which takes 15 seconds (75/5).

During this 15 seconds, the enemy deals 37.5HP (15*5/2) damage to the player.

At 15 seconds, since the enemy's HP is equal to 1/4, he immediately uses the healing skill to restore 20HP to himself, and the enemy has 45HP at this time.

In the next 8 seconds, the player deals 40HP (5HP*8) damage to the enemy. Likewise, the enemy deals 20HP (5HP*4) damage to the player.

At this time, since the enemy's HP is less than 1/4, and the healing skills can be used again after 8 seconds, the enemy can recover 20HP for himself, and now the enemy has 25HP.

The player deals 25HP damage to the enemy, which only takes 5 seconds. Likewise, during these 5 seconds, the enemy deals 12.5HP (5*5/2) damage to the player.

At this time, the player knocked down the enemy, and the player suffered a total of 70HP damage.



In the above example, the skill does not take the time of the normal attack and is instant cast. The calculated damage is calculated based on the normal time and the average damage per second of the attack, and it is assumed that the enemy can play the last attack before dying.






## Turn-based RPG
![Image](https://github.com/YunqianAo/RPG-Enemies-AI/blob/main/picture/presentacion%20%E6%8B%B7%E8%B4%9D2.jpg)
The method of encountering enemies in the game is "stepping on mines", and players will randomly fight while walking on the map. Therefore, the design of the "path" can be omitted. If the enemy is designed to be visible and patrolled on the map, it can still be designed in a "path" way. When the enemy captures the player, they will fight after collision.



Assuming that the enemy has 100HP and 40MP, normal attack damage is 10HP, skill attack damage is 75HP, consumes 10MP, and every two uses are separated by 10 rounds. Players have 100HP, normal attack damage 5HP, can use items to heal 100HP, no round interval limit.



The enemy's purpose is to cause maximum damage to the player, so the skill attack will be launched as soon as the skill interval expires. And use skills to heal yourself when your health is less than or equal to 1/4.



The enemy has two different states. When MP is not 0, it is a normal state.

The player deals 75HP (100HP*3/4) damage to the enemy's normal attack, and needs to attack for 15 (75/5) rounds.

The enemy causes 160HP to the player within 15 rounds (20HP+10HP*14).

During this time, the player needs to use a healing item once, so the actual number of rounds will increase to 16 rounds.

The enemy uses a skill to heal itself in turn 17, recovering to 100 HP.



Similarly, after another 17 rounds, the enemy still has 100 HP, but MP is 0. At this point, the enemy enters the second state - weakness. In a weak state, the enemy's defense decreases by 100% for 6 rounds. When weakened, the enemy recovers 40MP. After weakening, the enemy has 50HP and 40MP.



When the enemy's HP is less than or equal to 1/4, it will use the skill to heal itself. In this cycle, it seems that the player cannot defeat the enemy. Now, let's change our minds:



When the enemy has 30HP remaining, the player will no longer launch any attacks, choose defense (or standby), and maintain life by using healing items. When the enemy uses skills to exhaust MP and enters a weak state, the player will deal 30 (5HP*6) damage to the enemy within 6 rounds to kill it.



The above AI design, if the player attacks numbly, then it will take a lot of trouble to kill the enemy. However, if you know how to wait for the moment, you can quickly kill the enemy.



Calculate the damage properly, and introduce the design of state transition, which will bring new fun to the game.





You can incorporate more elements to enrich this model. For example, skills are not instant, they will take up a normal attack opportunity, and they will no longer perform normal attacks when using healing or strengthening skills; being attacked when recovering or strengthening skills will be extended. cooldown, etc. However, no matter how you change it, the above is its base model.


## Tectical RPG
![Image](https://github.com/YunqianAo/RPG-Enemies-AI/blob/main/picture/presentacion%20%E6%8B%B7%E8%B4%9D3.jpg)

As shown above:

The dotted line is the route of the enemy's patrol. Conventionally, the enemy will start from point A, move to point B after patrolling, and wait for the player to approach. However, if the player moves from point C to point D and is spotted by the enemy, the enemy will capture the player and start a fight.



Battles are conducted on a turn-based map. Assuming that the enemy has 100HP and 25MP, the normal attack damage is 5HP, the skill healing can recover 8HP, consumes 5MP, and there is no round interval limit. The player has 100HP, and the normal attack damage is 10HP.



The logical judgment is that in addition to attacking the player, when the enemy's HP is less than or equal to 1/4, it will use healing skills to restore HP and start to escape. So:

If the player and the enemy meet at the DE point, after 8 rounds, the player will deal 80HP (10HP*8) damage to the enemy. At the same time, the enemy deals 40HP (5HP*8) damage to the player.

At this point, the enemy starts to flee in the direction of the solid arrow, and uses healing skills to recover HP.



If the player chases the enemy in the same way, the damage deduction of 2HP per turn (10HP-8HP) can reduce the enemy's HP. And after 6 rounds, the enemy's MP is exhausted and can no longer self-heal and kill him.



However, if the player does not chase the enemy for some reason, the enemy will recover HP at a rate of 8HP per round, and a total of 40HP will be recovered in 5 rounds. At this time, the enemy will have 60HP. If the player thinks of chasing the enemy at this time, he will first need to spend 6 rounds to catch up with the enemy, and then spend 6 rounds to kill him.



Here, in addition to the round time caused by the consumption of HP in conventional battles, it is also necessary to consider the round time caused by the distance between the enemy and the player.

--------------------

The three elements of "reaction logic, limited reaction, and path" are the three powerful tools for us to design enemy AI in role-playing games. How to combine them and how to use them together will all be related to the operation mechanism of the enemy.



The above is an example of action (real-time) role-playing; turn-based role-playing games; and tectical role-playing, from which you can inspire and extend, and enrich and mutate models. However, no matter how you make a concrete change design, it is inseparable from three elements.

### About me
This page has been written by Yunqian Ao as part of a research project for the subject Project II in Videogame Design and Development at CITM.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/YunqianAo/RPG-Enemies-AI/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
