# LANDFALL --- PROJECT.md

## Source of Truth

This document describes the current design and implementation rules for
**Landfall**.

When working on the game:

1.  Read this file first.
2.  Inspect the current `index.html` before making changes.
3.  Treat the current working code as authoritative for implemented
    mechanics.
4.  Treat this document as authoritative for design intent.
5.  Preserve working systems unless a prompt explicitly asks to change
    them.
6.  Do not rebuild the game from scratch to make a small change.
7.  Do not silently add systems, resources, menus, meters, or simulation
    layers that are not part of this design.

Landfall is currently a single self-contained browser game in
`index.html`.

------------------------------------------------------------------------

# 1. THE GAME

**Landfall** is a quiet, real-time solo sailing game about taking a
roughly 35-foot cruising sailboat from **Shilshole Bay, Seattle** to
**Nawiliwili, Kauaʻi**.

The player is alone.

There is no character portrait, animated world, conventional map screen,
XP system, quest system, or traditional game HUD. The voyage is
experienced primarily through:

-   sparse terminal text
-   the persistent ship's log
-   boat sounds and weather ambience
-   real elapsed time
-   navigation information
-   resource management
-   decisions about sails, engine, course, food, water, sleep, repairs,
    and emergencies

The player's imagination supplies most of the world.

The experience should feel contemplative, physical, lonely, and
believable rather than gamey.

The central fantasy is not "winning a sailing game."

It is:

**You are sailing alone. The boat continues whether or not you are
looking at it.**

------------------------------------------------------------------------

# 2. CORE DESIGN PRINCIPLES

## Quiet interaction

Keep the interface sparse.

Do not add features merely because a real sailboat would contain them.

A system belongs in Landfall only when it creates a meaningful decision
for the player.

## Real time

**1 real minute = 1 game minute.**

The simulation does not stop when the browser closes.

The game catches up from actual elapsed time when the player returns.

Never make ordinary actions artificially advance the simulation clock.

Actions such as:

-   eating
-   drinking
-   setting sails
-   reefing
-   furling sails
-   starting/stopping the engine
-   repairing something
-   activating the EPIRB
-   firing a flare
-   deploying the life raft

may take a few real presentation seconds, but they do not manufacture
game time.

## No requirement for constant attention

Landfall should reward checking the boat a few times per day and taking
care of it, but it should not require the player to stare at the
browser.

A player can sleep, work, leave the app, and live their life.

The voyage continues.

Consequences may develop while they are away, but important systems
should be designed around broad real-time windows rather than tiny
moments that require the browser to be open.

## Cascading consequences

Failure should usually emerge from interacting systems rather than
arbitrary punishment.

The intended chain is broadly:

**weather → fatigue → mistakes → boat problems → repairs → spares
consumed → delays → food/water/fuel pressure → possible distress →
rescue**

Not every voyage should follow this chain, and not every problem should
escalate.

A player who checks in a few times a day, responds sensibly, manages
supplies, and has some luck should have a reasonable path to a safe
passage.

------------------------------------------------------------------------

# 3. PRESENTATION

## Terminal aesthetic

Landfall uses a dark CRT / phosphor-terminal presentation.

Current typography is IBM Plex Mono with a monospace fallback stack.

The interface should remain readable in a dark room and on a phone.

Avoid decorative UI, cards, icons, meters, badges, popups, and
conventional mobile-game chrome.

------------------------------------------------------------------------

# 4. COLOR SYSTEM

Landfall uses **three green text shades**, with extremely strict roles.

### BRIGHT GREEN

Used only for **selectable player actions and commands**.

Examples:

-   `> STATUS`
-   `> POSITION`
-   `> FULL`
-   `> REEFED`
-   `> START ENGINE`
-   `> EAT`
-   `> DRINK`
-   `> SLEEP`
-   `> BACK`

Meaning:

**I can do this.**

### SOFT GREEN

Used for **all ordinary non-interactive game text**.

This includes:

-   headings
-   log prose
-   descriptions
-   observations
-   ponderings
-   coordinates
-   navigation information
-   speed
-   region
-   inventory quantities
-   boat status
-   weather
-   action-progress text
-   action results
-   `.` / `..` / `...` sequences
-   informational labels

Meaning:

**This is happening / this is information.**

### DARK GREEN

Used for **timestamps only**.

Meaning:

**When it happened.**

The dark green must not become a generic secondary-text color.

Do not use it for descriptions, quantities, headings, status text,
observations, or other information.

Do not use opacity to create additional accidental green shades.

The current intended palette is:

-   background: `#050806`
-   soft green: `#8fd7ac`
-   bright green: `#c9f5da`
-   dark timestamp green: `#4d7a5e`

Amber and danger colors may remain for genuine warnings/errors where
already implemented, but normal hierarchy is governed by the three
greens above.

------------------------------------------------------------------------

# 5. ACTION-PROGRESS LANGUAGE

Short physical actions use the existing progression:

``` text
ACTION NAME

.
..
...

Result.
```

The dots appear sequentially.

They represent a few real seconds of physical action and are part of
Landfall's pacing language.

Do not replace them with:

-   loading spinners
-   progress bars
-   percentages
-   "please wait"
-   artificial game-time advancement

The dots themselves are the beat.

------------------------------------------------------------------------

# 6. OPENING / DEPARTURE SEQUENCE

The voyage begins at **Shilshole Bay, Seattle**.

Before departure, the game establishes that:

-   the boat is at Shilshole
-   the destination is Nawiliwili, Kauaʻi
-   the player is sailing alone

The interactive opening sequence is deliberately minimal:

``` text
You are sailing alone.

> BOARD

BOARDING

.
..
...

You step aboard.


> START ENGINE

STARTING ENGINE

.
..
...

The engine catches.


> CAST OFF

CASTING OFF

.
..
...

You ease away from the dock.

.
..
...

The voyage has begun.
```

Important rules:

-   No separate fender action.
-   No separate untie-lines action.
-   `CAST OFF` encompasses releasing the boat from the dock.
-   Remove/avoid the line `The last dock line comes aboard.`
-   The second `.` / `..` / `...` after `You ease away from the dock.`
    is the beat before `The voyage has begun.`
-   `The voyage has begun.` is a statement, not a button.
-   No `CONTINUE` button is required.
-   The opening does not artificially advance game time.

When the scripted opening ends:

-   engine is running
-   sails are furled
-   propulsion is motoring

The game must **not** automatically raise sails or stop the engine.

Those are the player's first real sailing decisions.

------------------------------------------------------------------------

# 7. REAL-TIME SIMULATION

The simulation runs at real-world speed.

Current implementation principles:

-   1 real minute = 1 game minute
-   simulation resolution is 10-minute ticks
-   the live browser periodically advances based on actual elapsed
    milliseconds
-   returning after an absence performs offline catch-up from real
    timestamps
-   local save state persists the voyage
-   no command should call simulation advancement merely to represent an
    action duration

The player's absence is part of the game.

When returning, Landfall may acknowledge how long the player has been
away, then show what happened through the persistent log.

Do not dump an excessive backlog of ambient observations after a long
absence.

------------------------------------------------------------------------

# 8. NAVIGATION

The route starts at **Shilshole Bay Marina** and proceeds through real
geographic steering waypoints toward Kauaʻi.

Current route structure:

1.  Shilshole Bay Marina
2.  mid-Sound
3.  passage north
4.  Whidbey side
5.  Admiralty Inlet
6.  Admiralty Inlet narrows
7.  Dungeness approach
8.  Strait of Juan de Fuca
9.  Cape Flattery
10. open water well offshore
11. trade wind belt
12. Kauaʻi / Nawiliwili approach

Waypoints are **steering targets**, not teleport points.

The boat's latitude and longitude must move physically from its current
position using:

-   current heading
-   actual speed
-   actual elapsed simulation time

Never interpolate the boat "as the crow flies" from Seattle to Kauaʻi
based on voyage percentage.

Never snap the boat toward a waypoint.

The intended course is the bearing from the boat's actual current
position to the current waypoint.

When close enough to a waypoint, the next waypoint becomes the steering
target.

The coordinates shown to the player therefore represent actual
dead-reckoned movement along the voyage.

------------------------------------------------------------------------

# 9. ALWAYS-ON NAVIGATION STRIP

Once underway, the interface should provide concise always-on navigation
context including:

-   voyage day
-   speed
-   heading
-   coordinates
-   region

Region should change with the voyage, e.g.:

-   Shilshole / Puget Sound area
-   Admiralty Inlet
-   Strait of Juan de Fuca
-   coastal Pacific
-   North Pacific / offshore
-   trade-wind region
-   Kauaʻi approach

Keep this concise.

Detailed information remains available through commands such as POSITION
and WEATHER.

------------------------------------------------------------------------

# 10. COURSE MANAGEMENT

Near shore, the intended geographic route is constrained so the player
cannot casually steer across land or charted hazards.

Once genuinely offshore, COURSE may allow broad strategic adjustments
such as:

-   HOLD COURSE
-   BEAR AWAY --- easier motion, farther off the intended line
-   COME UP --- closer toward the intended line, potentially harder
    motion

Course decisions should affect actual heading and therefore actual
coordinates.

Cross-track error should be calculated from real position rather than
maintained as a fake standalone progress variable.

------------------------------------------------------------------------

# 11. SAILS

Do not model separate main and jib controls.

The player manages one abstract sail state:

-   **FULL**
-   **REEFED**
-   **MINIMAL**
-   **FURLED**

Definitions:

### FULL

Maximum normal canvas.

Fastest in suitable conditions, but potentially overpowered in strong
wind.

### REEFED

Reduced sail for stronger conditions.

### MINIMAL

Very little canvas.

Slow but appropriate when conditions become difficult.

### FURLED

No sail propulsion.

All sails are put away.

Changing sail state is a short physical action using the dot sequence.

------------------------------------------------------------------------

# 12. ENGINE AND PROPULSION

The engine can be started and stopped independently of sail state.

This is essential because Landfall supports **motor-sailing**.

Possible propulsion states:

### SAILING

Useful sail propulsion, engine off.

### MOTORING

Engine running, sails furled or not usefully contributing.

### MOTOR-SAILING

Engine running while sails are also contributing.

### DRIFTING

Neither sails nor engine provide meaningful propulsion.

The engine and sails must both affect speed.

Motor-sailing should be faster than using only the weaker source, while
respecting the realistic limitations of a roughly 35-foot displacement
sailboat.

Current implementation uses approximately:

-   base engine speed: 5.5 kt
-   hull-speed reference: 7.3 kt
-   absolute realistic speed cap: 8.5 kt
-   diesel burn: 0.65 gal/hour while running

Do not treat sail + engine speeds as simple arithmetic addition.

Approaching hull speed should reduce the benefit of the secondary
propulsion source.

Fuel continues to burn in real elapsed time if the engine remains
running while the browser is closed.

------------------------------------------------------------------------

# 13. WEATHER

Weather is simulated and drifts over time rather than remaining static.

Current relevant variables include:

-   wind direction
-   wind speed
-   sea state
-   condition
-   trend

Weather affects:

-   sail performance
-   motoring performance
-   comfort/motion
-   sleep
-   fatigue
-   sail strain
-   flooding risk
-   rescue/search difficulty
-   ambient writing

The player can inspect WEATHER and a limited FORECAST.

Forecasts should remain imperfect and restrained rather than omniscient.

------------------------------------------------------------------------

# 14. THE LOG

The voyage log is the emotional and historical center of Landfall.

There are two distinct presentation surfaces:

## Persistent history

Things that actually happened belong in the persistent voyage history.

Examples:

-   meals eaten
-   water drunk
-   sail changes
-   engine changes
-   weather events
-   repairs
-   equipment problems
-   waypoint milestones
-   observations
-   ponderings
-   EPIRB activation
-   search events
-   flare firing
-   rescue
-   the opening sequence

Persistent log entries remain visible when the player returns.

## Temporary interface

Menus and information queries are temporary.

Examples:

-   STATUS
-   POSITION
-   WEATHER
-   FORECAST
-   INVENTORY
-   PROVISIONS
-   WATER
-   FUEL
-   SPARES
-   SAFETY
-   SAILS menu
-   ENGINE menu
-   COURSE menu

These must **not** become permanent log entries.

Opening INVENTORY should never cause inventory quantities to remain in
the voyage log.

The rule is:

**The log records what happened, not what menu the player looked at.**

------------------------------------------------------------------------

# 15. TIMESTAMPS

Persistent log timestamps use the dedicated **dark green**.

They should visually recede behind the actual event text.

All other ordinary text remains soft green.

Do not use dark green for anything except timestamps.

------------------------------------------------------------------------

# 16. OBSERVATIONS AND PONDERINGS

There is no player-facing OBSERVE command.

Observations and ponderings appear **spontaneously at random intervals**
in the persistent log.

They should feel like things that surface naturally during a long
solitary passage.

## Observations

Observations describe the physical world.

Examples include:

-   shoreline
-   ferries
-   seabirds
-   clouds
-   swell
-   fog
-   dolphins
-   flying fish
-   stars
-   phosphorescence
-   changing water color
-   approaching land

They should vary by voyage region, conditions, and time of day.

## Ponderings

Ponderings are quiet, unexplained thoughts.

Examples:

-   `You think of someone you haven't thought of in a long time.`
-   `A room from your childhood comes back to you. You can't remember why.`
-   `You wonder what everyone at home is doing right now.`
-   `You realize you haven't heard your own name spoken aloud in days.`

Do not explain the thought afterward.

Do not turn ponderings into dialogue choices.

Do not make them motivational quotes.

They simply appear and pass.

## Ambient-event restraint

Ambient writing should not fire during:

-   the scripted departure
-   active emergencies
-   severe weather
-   active flooding
-   pending decisions
-   sleep / attempts to sleep
-   severe hunger or dehydration
-   life-raft survival

Do not flood the log with ambient text after a long offline absence.

------------------------------------------------------------------------

# 17. HUMAN CONDITION

Landfall does not need a conventional HEALTH meter.

The important human states are:

-   fatigue
-   hunger
-   thirst
-   morale

Hunger and thirst are shown qualitatively rather than as visible numeric
meters.

The player should feel the condition through language and consequences.

------------------------------------------------------------------------

# 18. SLEEP

There is **no separate REST command**.

Sleep is not a time-skip button.

Selecting SLEEP means:

**the sailor goes below and tries to sleep.**

Possible internal states:

-   awake
-   trying
-   sleeping

A well-rested player cannot exploit SLEEP as a guaranteed fatigue reset
every time they close the game.

Falling asleep depends on factors such as:

-   current fatigue
-   time awake
-   sea state
-   recent coffee

Rough weather can interrupt sleep.

A player may choose SLEEP before closing Landfall, and real elapsed time
determines what happens while they are away.

The player can wake manually when appropriate.

This lets players manage their own real-life sleep/check-in rhythm
without creating a free "rest whenever the app closes" exploit.

------------------------------------------------------------------------

# 19. FOOD / PROVISIONS

Food is tracked as **servings**.

Current provisions include items such as:

-   oatmeal
-   pasta
-   rice
-   soup
-   chili / beans
-   tuna
-   crackers
-   peanut butter
-   nuts
-   dried fruit
-   energy bars
-   fresh fruit
-   fresh bread
-   comfort food
-   coffee

The exact inventory lives in the game state.

Some food is cooked and some is ready to eat.

Cooked food may consume:

-   propane
-   a small amount of fresh water

Very rough conditions may make cooking unsafe.

Fresh foods can spoil over time.

Eating reduces one serving from the authoritative inventory.

The log records **what the sailor ate**, not the remaining inventory
count.

Example:

`You make oatmeal in the galley.`

Not:

`Oatmeal eaten. 13 servings remaining.`

Inventory quantities belong in INVENTORY only.

------------------------------------------------------------------------

# 20. WATER

Water is a real finite resource.

Track:

-   **Fresh water**
-   **Emergency water**

in gallons.

Fresh water is used for:

-   drinking
-   some cooking

Emergency water is a deliberate reserve and should not be silently
consumed while primary water remains available.

Distinguish:

**water aboard** = inventory

from:

**thirst** = sailor condition

Drinking affects thirst and consumes actual water.

------------------------------------------------------------------------

# 21. FUEL

FUEL contains:

-   **Diesel**
-   **Propane**

Diesel powers the engine.

Propane powers cooking.

Do not create a separate propane top-level menu.

Diesel use is real-time and continues while the player is away if the
engine was left running.

------------------------------------------------------------------------

# 22. INVENTORY

The top-level inventory is deliberately limited to:

``` text
INVENTORY

> PROVISIONS
  WATER
  FUEL
  SPARES
  SAFETY
  BACK
```

Do not add top-level inventory categories without a strong gameplay
reason.

In particular, do not reintroduce:

-   TOOLS
-   MEDICAL
-   ENGINE
-   RIGGING
-   ELECTRICAL
-   PLUMBING
-   generic REPAIR category

as separate top-level inventory sections.

------------------------------------------------------------------------

# 23. SPARES

Consumable repair parts are consolidated under SPARES.

Current types include things such as:

-   impellers
-   drive belts
-   fuel filters
-   oil filters
-   engine oil
-   coolant
-   fuses
-   wire
-   connectors
-   spare batteries
-   hose
-   hose clamps
-   spare line
-   shackles
-   rigging tape
-   sail repair kits
-   epoxy
-   sealant

Repairs should consume the relevant authoritative inventory.

Do not turn this into an RPG crafting system.

Ordinary hand tools are assumed to exist aboard and are **not managed
inventory**.

------------------------------------------------------------------------

# 24. NO INJURY / MEDICAL SYSTEM

Do not build an injury simulator.

Do not add managed systems for:

-   cuts
-   burns
-   broken bones
-   bleeding
-   infection
-   medical treatment
-   first aid inventory
-   injury severity

The player already has meaningful vulnerability through:

-   fatigue
-   hunger
-   thirst
-   weather
-   resource depletion
-   boat failure
-   delay
-   rescue situations

Keep the focus on the sailor managing the voyage rather than managing
wounds.

If old incidental prose mentions a trivial bruise or similar flavor, do
not expand that into a medical mechanic.

------------------------------------------------------------------------

# 25. REPAIRS AND MISTAKES

Boat problems should sometimes require intervention.

Fatigue, hunger, thirst, conditions, and missing appropriate spares may
affect repair reliability.

A failed or delayed repair can create further problems.

Keep repairs readable and physical rather than numerical/crafting-heavy.

The player should understand:

-   what is wrong
-   whether action is needed
-   whether they have the relevant spare
-   whether the repair held

------------------------------------------------------------------------

# 26. FLOODING

Flooding is a rare but important emergency.

A hull leak creates a water-ingress rate.

The bilge pump has a pumping capacity.

The fundamental relationship is:

### If ingress \<= pump capacity

The pump can keep up.

The boat may remain viable while the player monitors and repairs the
problem.

### If ingress \> pump capacity

Water accumulates in the bilge.

The player should receive increasingly serious log information as water
rises.

The player may attempt a repair using appropriate spares.

Do not immediately force abandonment.

A damaged but floating 35-foot sailboat is generally a better survival
platform than a life raft.

The life raft becomes relevant only when the vessel is becoming
genuinely untenable.

------------------------------------------------------------------------

# 27. SAFETY

Managed safety equipment is intentionally limited to:

``` text
SAFETY

EPIRB .............. READY
Life raft .......... READY
Flares ................. 6
```

Do not add:

-   VHF radio management
-   first aid kit management
-   PFD management
-   large survival-equipment inventories

Assume ordinary offshore safety equipment exists without making all of
it a game system.

The three managed items have distinct purposes:

### EPIRB

**Come find me.**

### LIFE RAFT

**I can no longer safely remain on the boat.**

### FLARES

**I'm here.**

The SAFETY inventory screen reports equipment/status only.

It does not operate the equipment.

Emergency actions live in the DISTRESS context.

------------------------------------------------------------------------

# 28. EPIRB / DISTRESS

The EPIRB is the primary offshore rescue mechanism.

The player may activate it when they determine that they cannot safely
complete the voyage.

Activation uses the normal short-action presentation.

Example:

``` text
ACTIVATING EPIRB

.
..
...

Distress beacon transmitting.
Rescue requested.
```

Activating the EPIRB does **not** end the game.

The simulation continues.

Food, water, fatigue, weather, flooding, and other relevant conditions
continue until the player is actually rescued.

------------------------------------------------------------------------

# 29. RESCUE

Rescue occurs in real elapsed time.

The delay should depend broadly on factors such as:

-   voyage region
-   distance offshore
-   weather
-   sea state
-   visibility
-   whether the sailor is aboard the sailboat or in the life raft

Do not expose artificial rescue percentages to the player.

Current conceptual phases are:

1.  none
2.  traveling
3.  searching
4.  rescued

Once rescue is requested, the state must persist through closing and
reopening the browser.

------------------------------------------------------------------------

# 30. LIFE RAFT

The life raft is a **last resort**.

It becomes a meaningful option when flooding or another severe boat
condition makes remaining aboard unsafe.

Do not automatically deploy it.

Do not immediately tell the player to abandon ship when a leak begins.

Allow the player to:

-   monitor the flooding
-   rely on the bilge pump if it is keeping up
-   attempt repairs
-   activate the EPIRB
-   decide whether the boat remains viable

Once the sailor enters the life raft, the nature of the voyage changes.

Normal sailing, engine, steering, and boat-repair gameplay should no
longer apply.

The sailor is now waiting and surviving until rescue.

A life raft is a much smaller visual target than the sailboat, which
makes flares more valuable.

------------------------------------------------------------------------

# 31. FLARES

Flares are finite.

Current starting quantity:

**6**

Flares are primarily useful during the active rescue/search phase.

When rescuers are plausibly nearby, the player may receive an
opportunity such as:

``` text
You hear an aircraft.

It circles somewhere to the east.

Rescuers are searching the area.

> FIRE FLARE
```

Firing a flare:

-   consumes one flare
-   improves the chance/speed of visual acquisition
-   should be especially useful at night, in poor visibility, rough
    conditions, or from a life raft

A flare does **not** initiate rescue.

The EPIRB does that.

A flare helps rescuers visually identify the sailor's exact location.

------------------------------------------------------------------------

# 32. ASYNCHRONOUS RESCUE

The player is unlikely to have Landfall open continuously.

Therefore rescue must not depend on catching a tiny live interaction
window.

Search encounters should remain relevant for broad real-time periods.

Missing one search event does not automatically mean death or permanent
rescue failure.

The EPIRB remains active.

Search efforts continue.

A missed encounter may be recorded in the log, and another opportunity
can occur later.

Flares should improve rescue, not be an absolute requirement for rescue.

This preserves the game's central rule:

**Checking in matters, but real life is allowed.**

------------------------------------------------------------------------

# 33. FAILURE / RESCUE PHILOSOPHY

A player may eventually determine that the voyage cannot safely be
completed.

Calling for rescue is a legitimate outcome.

The game continues after the rescue call until the sailor is actually
found.

If the player fails to request rescue despite an unrecoverable survival
situation, death may remain a possible terminal outcome.

Do not make death melodramatic.

Do not turn rescue into a cinematic action sequence.

Keep terminal outcomes sparse and consistent with the rest of Landfall.

The game's title is tied to the final state:

**LANDFALL**

or

**NO LANDFALL**

Use restrained presentation around endings.

------------------------------------------------------------------------

# 34. MENUS / COMMANDS

The interface is button-driven, not a free-text command parser.

Current core commands include:

### Information

-   STATUS
-   POSITION
-   WEATHER
-   FORECAST
-   INVENTORY

### Boat / navigation

-   SAILS
-   ENGINE
-   COURSE
-   REPAIR

### Human needs

-   EAT
-   DRINK
-   SLEEP

### Emergency

-   DISTRESS

Keep menus concise.

Use submenus when necessary rather than allowing the main command list
to become overwhelming.

Bright green always indicates something selectable.

------------------------------------------------------------------------

# 35. STATUS

STATUS provides qualitative condition information.

It may include:

-   fatigue
-   morale
-   hunger
-   thirst
-   water availability
-   diesel
-   propane
-   hull
-   rigging
-   sails
-   electrical condition

Prefer qualitative language where exact numbers are not useful.

Exact consumable quantities belong in INVENTORY.

------------------------------------------------------------------------

# 36. POSITION

POSITION can show:

-   coordinates
-   heading
-   intended course
-   propulsion mode
-   speed
-   distance sailed
-   approximate distance remaining
-   meaningful cross-track deviation

Coordinates must come from actual simulated movement.

Do not fabricate progress from a percentage-of-route interpolation.

------------------------------------------------------------------------

# 37. AUDIO

Audio is atmospheric, not musical UI feedback.

Current procedural ambience includes elements such as:

-   wind
-   waves
-   rigging
-   rain

Audio should react subtly to conditions.

The player can turn sound on/off.

Future recorded audio may replace or supplement procedural sounds, but
audio should continue telling the physical story of the boat rather than
becoming a soundtrack-heavy game.

------------------------------------------------------------------------

# 38. SAVE SYSTEM

The current voyage is stored locally in the browser.

Save state should preserve all important ongoing conditions, including:

-   real-time timestamps
-   voyage minutes
-   actual latitude/longitude
-   current waypoint
-   heading/course offset
-   weather
-   sail state
-   engine state
-   diesel
-   boat condition
-   fatigue/hunger/thirst/morale
-   sleep state
-   food
-   water
-   propane
-   spares
-   safety equipment
-   flooding
-   rescue state
-   life raft state
-   flare count
-   departure stage
-   persistent log

When adding new state fields, preserve compatibility with existing saves
where practical.

Use migration/default logic instead of casually breaking active voyages.

------------------------------------------------------------------------

# 39. RESTART

RESTART begins a genuinely new voyage from Seattle at the current real
time.

It discards the old save.

Restarting is not a time-skip mechanic.

Require confirmation before destroying the current voyage.

------------------------------------------------------------------------

# 40. THINGS LANDFALL IS NOT

Landfall is not:

-   an RPG
-   a crafting game
-   a medical simulator
-   a sailing-school exam
-   a detailed marine-electronics simulator
-   a conventional survival meter game
-   a map-following game
-   an idle game where the optimal strategy is never to open it
-   a game that demands constant notifications or check-ins
-   a menu-heavy management sim

Avoid feature creep toward those forms.

------------------------------------------------------------------------

# 41. WRITING STYLE

Writing should be:

-   concise
-   concrete
-   restrained
-   sensory when useful
-   slightly literary without becoming purple
-   comfortable with silence

Avoid:

-   exposition dumps
-   tutorials disguised as prose
-   excessive nautical jargon
-   jokes that break the atmosphere
-   motivational language
-   melodrama
-   constant danger
-   explaining the meaning of ponderings

Good Landfall writing often stops one sentence earlier than another game
would.

------------------------------------------------------------------------

# 42. DEVELOPMENT WORKFLOW

For each meaningful development pass:

1.  Read `PROJECT.md`.
2.  Inspect the current `index.html`.
3.  Identify the smallest set of code paths that need to change.
4.  Preserve unrelated working systems.
5.  Make the change.
6.  Test the affected flow.
7.  Test save/load behavior if state changed.
8.  Test mobile layout if UI changed.
9.  Return the complete updated `index.html`.
10. If the design itself changed, update `PROJECT.md` afterward so it
    remains the source of truth.

Prefer focused prompts and focused changes over repeatedly rebuilding
the whole application.

Large prompts are appropriate when defining a coherent new system. Small
prompts are preferable for visual tweaks, copy changes, bug fixes, and
isolated behavior changes.

------------------------------------------------------------------------

# 43. CURRENT CANONICAL SUMMARY

Landfall begins in **Shilshole Bay**.

You board.

You start the engine.

You cast off.

You ease away from the dock.

The voyage has begun.

From there, nothing important is automated for the player.

They decide when to:

-   raise or reduce sail
-   furl the sails
-   motor
-   motor-sail
-   stop the engine
-   eat
-   drink
-   sleep
-   inspect the boat
-   repair problems
-   alter course offshore
-   conserve resources
-   call for rescue

Meanwhile:

-   the boat keeps moving
-   the weather keeps changing
-   fuel keeps burning if the engine is running
-   hunger and thirst develop
-   sleep happens in real time
-   supplies are consumed
-   problems may develop
-   observations appear
-   thoughts surface
-   the coordinates change
-   the log grows

The player does not control time.

They only decide what to do with the time that passes.

The voyage ends in:

**LANDFALL**

or

**NO LANDFALL**.
