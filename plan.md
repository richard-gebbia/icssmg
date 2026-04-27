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
- [ ] Content!
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
- Player starts at level 1 with a blue
- First quest is always 1 blue to level up and never goes away
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
