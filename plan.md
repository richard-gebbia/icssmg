- [x] Init the repo
- [x] Find a palette
- [X] Get icons for the stats
    - [X] white circle
    - [X] yellow star
    - [X] blue square
    - [X] purple parallelogram
    - [X] pink diamond
    - [X] green triangle
- [X] Render the shapes
    - [X] Now do it in Gren
- [X] Build a simple runnable model
- [X] UI (see below)
- [X] Quests give rewards
- [X] Commit Cycle
- [X] Actually have HP and max HP change effects do something
- [X] Scrollable quest display
- [X] Cycle number
- [X] Rework wilds (player has wilds, additional buttons to spend wilds on quest requirements)
- [X] Test many points for a requirement
- [X] Grid layout for quest
- [X] Font
- [X] Background
- [X] Generate initial seed
- [X] Expiration effects
- [X] Content!
- [X] Display three turns worth of stat boosts
- [X] Off-by-one bug: effects last 1 more cycle than they should, though before their last cycle it's not displayed in the "next cycle" counter
- [ ] Maybe consider a way to convert one stat to another at a really bad exchange rate (easy quests kinda facilitate this)
- [ ] Make easy quests take two different stats
- [ ] Maybe consider a recycle quest button
- [X] Prevent another Level Up or Spawner from showing up if there's already one
- [X] Display the number of quests at the top
- [X] Display number of quests completed
- [X] Easy and medium quests should always return a stat that they don't take, this makes them poor but useful conversions
- [X] Change "on expiration" language to "when this goes away"
- [X] Find a way to show what spawned a quest
- [ ] Weight upcoming points and potentially partially-filled quest rewards
- [X] Possibly lower the cost for permanent stat upgrades
- [ ] Make ever-present bosses that will cause you to lose (or take a lot of damage) after a certain number of cycles
    - Once you beat the boss, you level up, get a bunch of resources, and a new boss appears (maybe after some cycles)
- [ ] Find minimal repro for a bug with Gren formatter

# UI
Two panes, horizontally laid out:
- Pane 1
    - larger
    - scrollable
    - info:
        - Quests, for each
            X title
            - requirements, for each
                X how many points to complete
                X button to add one point toward
                X button to add max possible points toward
                X button to remove one point from
                X button to remove all points that were put toward this cycle
            X rewards
            X expiration
            - what (if anything) happens on expiry
- Pane 2
    - smaller, fixed width, not scrollable
    - info:
        X Player HP/Max HP
        X Player HP/Max HP next cycle
        X Player Level
        X Player level next cycle
        X Stats, for each
            X points currently held this cycle
            X total points this cycle
            X points player will get next cycle
        X Wilds player will get next cycle
        X Button to end cycle depending

# Content
- Player starts at level 1 with a white
- First quest is always 1 white to level up and never goes away
- Content
    - quests scale with level
    - split of bespoke and procedurally generated quests
    - bespoke quests
        - Get N points of each non-white stat to summon level-up quest next cycle
        - FAFO
            - easy-ish quest that summons 2-3 harder quests next cycle, with good rewards but low expiration time
            - the summoner quest requires all one stat (or maybe 2 or 3), and the summoned quests require that stat (or like if the summoner requires pink, yellow, green; there would be 3 summoned quests, one requiring all pink, one requiring all yellow, and one requiring all green)
            - the summoned quests will deal the player damage if they don't complete them in time
    - procedurally generated quests
        - easy
            - 1-2 can be done in 1-2 cycle
        - medium
            - 1 can be done in 3 cycles
        - hard
            - 1 can be done in 4-5 cycles
        - require random inputs (decide number of input stats first, only partially by looking at what the player has), produce random outputs, obv scaling with "difficulty"
    - ideas
        1. quest to level up
            - should require lots of white, which no other quest uses
        2. quest to spawn the level up quest
            - get N points of each non-white stat to complete
        3. FAFO
            - easy-ish quest that summons 2-3 harder quests next cycle, with good rewards but low expiration time
            - the summoner quest requires all one stat (or maybe 2 or 3), and the summoned quests require that stat (or like if the summoner requires pink, yellow, green; there would be 3 summoned quests, one requiring all pink, one requiring all yellow, and one requiring all green)
            - the summoned quests will deal the player damage if they don't complete them in time
        4. quests to "level up" each individual stat
            - should require lots of that stat to get
        5. Easy procuderally generated quest
            - 1-2 of these can be done in 1-2 cycles
            - see "procedurally generated quests" above for more details
        6. Medium procedurally generated quest
            - 1 can be done in ~3 cycles
            - see "procedurally generated quests" above for more details
        7. Hard procedurally generated quest
            - 1 can be done in 4-5 cycles
            - see "procedurally generated quests" above for more details
        8. Easy quest that damages you on expiration
        9. Medium quest that heals you on completion
        10. Hard quest that raises max HP on completion
        11. Easy quests that summon a harder quest, which summons a harder quest, which summons a recurring quest that provides +N to a stat for two cycles
        12. Easy quest that summons a harder quest, which summons a harder quest, which summons a recurring quest that heals you
- Content pipeline
    - Write a small CSV to gren thing, make content in Excel
        - Develop notation for this to make importing automatic
- Content cadence
    - 1 new quest every ~3 cycles
    - don't make a new quest if the player is already dealing with 10 or more

## Effect resolution
- Upon clicking "Next Cycle", this happens in order:
    - the player resets all their points to zero
    - all effects from the previous cycle tick down, those that are at 0 go away
    - collect any effects from quests completed last cycle
    - collect any effects from quests that are at 1 cycle to go, have expiration effects, and aren't completed
    - quest durations tick down, those that are at 0 go away
    - apply all previous effects that haven't gone away and all collected effects to the player
    - spawn any new quests from effects
    - if it's time to add a new quest, generate a new quest
    - if we're still at < 5 quests, generate quests up to the 5 minimum


## Feedback
Stephen:
- game is decently fun once you get into a groove
- it can get a little impossible at higher levels
- you sometimes get boned; the weighting to determine new quest inputs isn't strong enough
- "you can get stuck in a cycle where you're getting Channel quests for the nebulae you've completed over and over, and it sorta shoehorns what resources you have available in larger amounts"
- the stat level up quests are (maybe) a bait
- "on expiration" verbiage not clear
- quest was spawned from what not clear

Victor:
- strategy to play the game is too simple
- game is a 1-2 out of 10, only sees 4/10 potential