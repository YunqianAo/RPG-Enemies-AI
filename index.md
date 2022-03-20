## RPG Enemies AI

RPG is the abbreviation of role-playing. Generally speaking, it includes three categories: action (real-time) role-playing; turn-based role-playing games; and chess role-playing. When encountering an enemy in these three types of games, it is the beginning of a battle. So, what mechanism does the enemy in the game operate according to? In other words, how does their AI (artificial intelligence) work? This brings sufficient room for the design of enemies in the game.

The operations of these enemies must simulate the thinking of the human brain to a certain extent. That is to say, under what circumstances, what kind of response and what kind of response should be more targeted and in line with certain logic. For example: an enemy with healing skills, when its health is running out, it should think out a response and heal itself. This is the logical coping part the designer has to give to the enemy AI design. At this time, we need to design a "path" for it. This "path" design includes:

###1) Patrol path. 

When the enemy does not find the player, what is its walking range, and what route does the enemy follow within this walking range? This is the patrol path. The patrol path can be to let the enemy wait from a starting point to an end point; it can also be repeated back and forth or looped over a certain distance.

###2) Scouting range and scouting conditions. 

The reconnaissance range can be understood as the vision of the enemy. The farther and wider the vision is, the easier it is to be found by the enemy when you are close to the enemy; on the contrary, if the enemy's vision is short-sighted, then you can be invisible to the enemy. Get closer to the enemy. Scouting conditions are a supplementary description of the scouting range. For example, the enemy's vision cannot pass through the wall, so if the player stands behind the wall, even if the enemy is within the detection range of the enemy, the enemy will not find the player. This is one of the conditions for reconnaissance.

###3) Arrest path. 

When the enemy finds the player, what path does it take to capture it? This is also something to consider. If there are no obstacles between the enemy and the player before, then the enemy can directly approach the player. However, if there is an obstacle between the enemy and the player, or there is a difference in terrain, the enemy needs to take a detour to arrest the player.

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
