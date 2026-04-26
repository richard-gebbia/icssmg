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
- [ ] UI (see below)
- [X] Quests give rewards
- [ ] Commit Cycle
- [ ] Actually have HP and max HP change effects do something
- [ ] Distribute wilds phase
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
        - Stats, for each
            X points currently held this cycle
            X total points this cycle
            X points player will get next cycle
            - button to add wild to stat
            - button to remove wild from stat
        X Wilds player will get next cycle
        - Button to confirm wild distribution or end cycle depending on the phase (at the bottom)