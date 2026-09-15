# LANDFALL

## Project

Landfall is a slow, real-time solo sailing game about sailing a roughly 35-foot cruising sailboat from Seattle to Kauaʻi.

The player is alone.

The game is experienced primarily through text, sound, time, navigation information, weather, ship's logs, decisions, and consequences.

The ocean largely exists in the player's imagination.

## Core Design Principle: Real Time

THIS RULE MUST NOT BE CHANGED.

Landfall runs in real-world time.

1 real-world minute = 1 game minute.
1 real-world hour = 1 game hour.

The game continues while the browser is closed.

There is NO time skipping.

No action such as:

- sleep
- rest
- wait
- repair
- eat
- navigate

may artificially advance the game clock.

Sleep and rest are STATES, not time-advancement actions.

If the player goes to sleep at 11:00 PM and returns at 7:00 AM, exactly 8 real-world hours have elapsed aboard the boat.

When the player returns, the simulation calculates what occurred during that elapsed real-world period.

## Philosophy

Landfall should not feel like a conventional video game.

Avoid:

- health bars
- XP
- levels
- quests
- constant notifications
- excessive buttons
- excessive statistics
- artificial urgency
- conventional game HUDs
- time acceleration

The player should feel alone, uncertain, and responsible for the boat.

Information should sometimes be incomplete.

Quiet periods are important.

Not every check-in needs an event.

The player should want to check the game because they are wondering:

"What happened while I was gone?"

## Player Rhythm

Landfall is designed to be checked a few times throughout a real day.

A player might:

- wake up and check the boat
- check weather
- inspect position
- make a course or sail decision
- leave
- return several hours later
- read what happened
- prepare the boat for night
- go to sleep in real life

The game should fit around the player's life rather than demand constant attention.

## Simulation

The simulation may internally track numerical values including:

- latitude
- longitude
- heading
- intended course
- boat speed
- wind direction
- wind speed
- sea state
- weather
- food
- water
- fatigue
- sleep
- morale
- hull condition
- sails
- rigging
- electrical system
- engine
- equipment condition
- voyage time

However, the interface should usually translate these numbers into natural observations.

For example, instead of:

FATIGUE: 73%

prefer:

FATIGUE
Severe. Concentration is becoming difficult.

## Cascading Consequences

Systems should influence one another.

Example:

bad weather
→ course change
→ course deviation
→ longer voyage
→ reduced supplies
→ rationing
→ fatigue
→ mistakes
→ unreliable repairs
→ greater risk

Failure should generally emerge from accumulated circumstances and decisions rather than arbitrary instant death.

## Interface

The interface should resemble an old marine computer / early computer terminal.

Visual direction:

- nearly black background
- soft desaturated green phosphor text
- monospaced typography
- restrained CRT glow
- extremely subtle scanlines
- minimal animation
- comfortable in a dark room
- no modern cards or dashboard aesthetic
- very limited color

The webpage itself is the game.

## Navigation

Do not permanently display a progress map.

The player deliberately checks information such as:

- position
- heading
- intended course
- weather
- forecast
- distance
- recent movement

Navigation should require interpretation and judgment.

## Audio

Audio is a major storytelling system.

Eventually use layered environmental sounds such as:

- water against the hull
- wind
- rigging
- hull creaks
- rain
- cabin rattles
- sail movement
- mechanical sounds
- objects shifting below deck

Avoid constant music.

Silence is useful.

Changes in familiar sounds can communicate danger before text does.

## Writing

Writing should be sparse, observational, and restrained.

Do not over-explain events.

Do not add a narrator companion, radio friend, AI assistant, or other character simply to provide exposition.

The player is alone.

The ship's log should become the story of each individual voyage.

## Current Development Scope

Do NOT attempt to build the entire Seattle-to-Kauaʻi voyage yet.

Current priority:

Make the first 24 hours compelling.

Before adding major systems, test whether the core experience of checking the boat, making decisions, leaving, and returning in real time is interesting.

## Development Rule

Preserve working functionality.

Make small changes.

Test before expanding.

Do not add features merely because they are technically possible.

Atmosphere, consequence, solitude, and anticipation are more important than feature count.
