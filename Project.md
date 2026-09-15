LANDFALL — NEXT DEVELOPMENT VERSION

You are continuing development of an EXISTING working game called Landfall.

Do NOT rebuild Landfall from scratch.

First inspect the complete current index.html and understand how the existing simulation, real-time clock, navigation, menus, save system, entry sequence, sleep/fatigue systems, and interface work.

Preserve all existing working functionality unless this prompt explicitly asks for a change.

The goal of this development pass is to deepen Landfall into a persistent real-time sailing simulation built around:

- real-world time
- navigation
- human needs
- inventory
- maintenance
- finite resources
- cascading consequences
- observation
- solitude
- survival
- eventual landfall or rescue

IMPLEMENT THESE SYSTEMS CAREFULLY AND MODULARLY.

Do not rewrite unrelated systems simply because you would have designed them differently.

==================================================
CORE DESIGN PHILOSOPHY
==================================================

Landfall is a real-time solo sailing voyage from Shilshole Bay Marina in Seattle to Kauaʻi aboard a roughly 35-foot offshore cruising sailboat.

The player is the sailor.

The player should feel as though the boat continues existing while they are away.

1 REAL MINUTE = 1 GAME MINUTE.
1 REAL HOUR = 1 GAME HOUR.

There is no artificial time acceleration.

Closing the browser does not pause the voyage.

Returning after six hours means six hours have passed aboard the boat.

Landfall should generally be playable by checking the boat thoughtfully a few times per day.

A competent player who:

- checks the boat several times per day
- reads conditions carefully
- navigates sensibly
- eats and drinks reasonably
- manages sleep
- maintains the vessel
- responds to developing problems

should have a HIGH probability of reaching Kauaʻi safely.

Landfall should NOT manufacture constant emergencies.

Competence should often produce calm.

Long stretches where nothing goes wrong are desirable.

Danger should primarily emerge through accumulated circumstances:

poor decisions
→ delay
→ resource consumption
→ fatigue
→ mistakes
→ equipment problems
→ further delay
→ dwindling margins

The drama should emerge from the simulation rather than scripted constant excitement.

==================================================
DEPARTURE — SHILSHOLE BAY
==================================================

The voyage begins at Shilshole Bay Marina.

The opening portion of the voyage should be geographically constrained.

The intended opening route is broadly:

Shilshole Bay
→ Puget Sound
→ Admiralty Inlet
→ Strait of Juan de Fuca
→ Cape Flattery
→ Pacific Ocean

During this opening section, the player is learning the boat and the interface.

Do not allow arbitrary offshore course changes while geographically constrained by land.

If the player attempts to make an inappropriate course alteration, use restrained language such as:

CAN'T ALTER COURSE.
TOO CLOSE TO SHORELINE.

The player should gradually learn:

- checking weather
- checking position
- checking boat speed
- eating
- drinking
- sleeping
- observing surroundings
- checking inventory
- inspecting the vessel

without a conventional tutorial overlay.

Once the boat reaches sufficiently open blue water, unlock meaningful course alteration.

At that point the player becomes responsible for navigating the offshore passage.

==================================================
NAVIGATION
==================================================

Preserve the existing corrected navigation model.

The boat's latitude and longitude must result from its ACTUAL movement.

Never interpolate coordinates between Seattle and Kauaʻi based on voyage progress.

Position should emerge from:

- actual latitude/longitude
- heading
- boat speed
- elapsed real time
- wind
- drift/current
- player decisions

The intended route is guidance only.

The boat must be capable of sailing off course.

Do not automatically snap it back to the route.

Two voyages should be capable of producing different tracks.

==================================================
BOAT SPEED
==================================================

Add boat speed as a meaningful observable value if it is not already properly implemented.

Speed should be expressed realistically in knots.

Boat speed should result from sailing conditions rather than being a fixed voyage-progress variable.

It should be influenced by:

- wind speed
- wind direction relative to heading
- sail configuration
- sea state
- boat condition
- damage
- current
- course
- severe weather
- calm conditions

Boat speed affects actual distance traveled.

If the boat averages 6 knots for 8 real hours, approximately 48 nautical miles of actual movement should occur, subject to changes in conditions during that period.

==================================================
OBSERVE
==================================================

Add an OBSERVE action.

OBSERVE is not primarily informational.

It exists to make the voyage feel physical, beautiful, lonely, and real.

When selected, describe something the sailor notices around the boat.

Observations should be influenced by:

- geographic position
- distance from land
- time of day
- weather
- sea state
- latitude
- phase of voyage
- recent conditions

Near Puget Sound observations might include:

- shoreline
- ferries
- mountains
- seabirds
- lights
- distant vessels
- rain over land

Offshore observations might include:

- swell
- cloud formations
- flying fish
- seabirds
- moonlight
- stars
- phosphorescence
- distant ships
- empty horizon
- sunrise
- sunset
- rain squalls
- changing color of the sea

Approaching Hawaiʻi might eventually include appropriate signs of land and subtropical conditions.

Do not make every observation extraordinary.

Most should be quiet.

Occasionally create genuine moments of awe.

Do not use repetitive poetic writing.

Keep Landfall's restrained observational voice.

==================================================
HUMAN CONDITION
==================================================

The sailor has several interacting human needs.

These should influence judgment and physical ability without turning Landfall into a collection of visible videogame meters.

The primary systems are:

- hunger
- thirst
- fatigue
- sleep
- physical condition

Use natural language wherever possible.

==================================================
HUNGER
==================================================

Use FOUR broad internal hunger states.

Do not display a numerical hunger percentage.

Hunger should meaningfully progress approximately every four real-world hours without adequate food.

The exact simulation may account for recent meals and meal quality.

Example qualitative states:

FED
GETTING HUNGRY
HUNGRY
VERY HUNGRY / WEAKENING

Use natural language rather than exposing underlying numbers.

Missing one meal should not be dangerous.

Several days of inadequate food should gradually contribute to:

- weakness
- fatigue
- poorer concentration
- mistakes
- reduced repair quality

==================================================
THIRST
==================================================

Use FOUR broad internal thirst states.

Thirst should normally worsen approximately every four real-world hours without adequate hydration.

Hot conditions should increase water requirements.

Physical exertion may also increase thirst.

Do not display a numerical hydration percentage.

Repeated dehydration should gradually affect:

- concentration
- fatigue
- physical performance
- repair ability
- judgment

Severe prolonged dehydration can eventually become life-threatening.

==================================================
SLEEP
==================================================

There is NO REST action.

Remove REST if any remnants remain.

The sailor is normally AWAKE.

Closing Landfall does NOT mean the sailor is sleeping.

SLEEP is an explicit player decision.

However:

SLEEP means ATTEMPT TO SLEEP.

It does NOT simply activate automatic fatigue recovery.

The sailor should have an internal sleep-pressure system based on:

- how long they have been awake
- restorative sleep received recently
- sleep interruptions
- current fatigue
- sea state
- weather
- noise
- stress
- problems aboard the boat

A well-rested sailor who selects SLEEP every time the player closes Landfall should NOT sleep for the entire absence.

They may:

- fail to fall asleep
- sleep briefly
- wake naturally
- remain awake afterward

For example:

YOU SLEPT FOR 24 MINUTES.

THE REST WOULDN'T COME.

An exhausted sailor should fall asleep more easily and generally sleep more deeply.

Rough seas, noise, weather, stress, or problems aboard the boat may reduce sleep quality or interrupt sleep.

Do not expose:

SLEEP PRESSURE: 74%

or any similar numerical meter.

The player experiences sleep naturally.

Short nighttime check-ins should NOT be heavily punished.

If the player wakes at 2:30 AM, checks the boat for a few minutes, and selects SLEEP again, they should generally be able to continue their night's sleep if sufficient sleep pressure remains.

The purpose of this system is to make sleep human and prevent the exploit:

CLOSE GAME
→ SELECT SLEEP
→ NEVER EXPERIENCE FATIGUE

==================================================
FOOD / PROVISIONS
==================================================

Implement a complete food inventory.

Food is represented as ACTUAL PROVISIONS, not a generic FOOD percentage.

ALL edible food inventory uses one unit:

SERVINGS.

Do not track edible provisions using:

- cans
- boxes
- jars
- pounds
- ounces
- calories
- percentages

One serving represents one reasonable portion of that particular food.

Create thoughtful starting provisions appropriate for one sailor undertaking approximately a 3–4 week offshore passage with a reasonable emergency margin.

Possible starting inventory:

Oatmeal ............. 18 servings
Pasta ............... 12 servings
Rice ................ 16 servings
Soup ................. 8 servings
Chili / Beans ......... 8 servings
Tuna ................. 10 servings
Crackers ............. 12 servings
Peanut Butter ........ 10 servings
Nuts ................. 16 servings
Dried Fruit .......... 12 servings
Energy Bars .......... 12 servings
Fresh Fruit ........... 8 servings
Fresh Bread ........... 6 servings
Comfort Food .......... 6 servings
Coffee ............... 24 servings

Adjust quantities if necessary for realistic balance.

The boat should start with enough food for a normal passage plus reasonable emergency margin.

==================================================
EATING
==================================================

Add or improve an EAT action.

Selecting EAT shows currently available provisions.

The player chooses what to eat.

Normally:

1 selection = 1 serving consumed.

Do not create complicated recipe construction.

Meals can be simple.

Examples:

Oatmeal
Soup
Pasta
Rice
Tuna
Crackers + Peanut Butter
Nuts + Dried Fruit

Use restrained feedback:

YOU MAKE OATMEAL AND COFFEE.

YOU EAT TUNA AND CRACKERS IN THE COCKPIT.

THE SEA IS ROUGH.
YOU EAT PEANUT BUTTER AND CRACKERS BELOW.

Never show:

+15 ENERGY
+5 MORALE

==================================================
FOOD CHARACTERISTICS
==================================================

Foods may have hidden characteristics including:

- satiety
- basic nutrition
- requires cooking
- requires water
- requires propane
- spoilage
- ease of eating in rough conditions
- comfort value

Do not expose these statistics.

==================================================
COOKING
==================================================

Some foods require cooking.

Examples:

- oatmeal
- rice
- pasta

Cooking may consume small realistic amounts of:

- fresh water
- propane

Other foods are immediately edible.

Examples:

- tuna
- crackers
- peanut butter
- nuts
- dried fruit
- energy bars
- fresh fruit
- bread

Weather should sometimes affect cooking.

During severe conditions:

THE BOAT IS MOVING TOO VIOLENTLY
TO COOK SAFELY.

The player must choose ready-to-eat food.

Do not make cooking a minigame.

==================================================
SPOILAGE
==================================================

Fresh food should gradually spoil in real time.

Keep this simple.

Fresh bread and fresh fruit can deteriorate during the early voyage.

Shelf-stable food should remain usable.

Do not create elaborate expiration systems.

==================================================
COFFEE
==================================================

Coffee is measured in servings.

Coffee may temporarily improve alertness or concentration.

Coffee DOES NOT:

- eliminate fatigue
- remove sleep debt
- substitute for sleep

Poorly timed/excessive coffee may make falling asleep somewhat more difficult.

Keep this subtle.

Coffee is not a videogame power-up.

==================================================
WATER
==================================================

Fresh water is a finite inventory resource.

Track:

- primary fresh-water supply
- emergency water reserve

Drinking consumes water.

Cooking may consume water.

Heat increases water consumption.

Leaks or contamination may threaten the supply if appropriate failures occur.

A normal passage should begin with sufficient water plus an appropriate safety margin.

Running low on water should be significantly more urgent than running low on food.

==================================================
FUEL AND PROPANE
==================================================

Track finite:

- diesel
- propane

Diesel may be required for:

- engine use
- charging systems where appropriate
- maneuvering under power

Propane is primarily used for cooking.

Do not artificially replenish either resource.

==================================================
VESSEL INVENTORY
==================================================

Inventory management is one of Landfall's CORE systems.

Track a thoughtful set of finite supplies appropriate for a roughly 35-foot offshore cruising sailboat.

Include appropriate quantities of:

PROVISIONS
FRESH WATER
EMERGENCY WATER
DIESEL
PROPANE

ENGINE:
- engine oil
- coolant
- fuel filters
- oil filters
- spare impellers
- drive belts

RIGGING:
- spare line
- shackles
- appropriate rigging repair materials

PLUMBING:
- spare hose
- hose clamps
- plumbing repair materials

ELECTRICAL:
- wire
- fuses
- connectors
- batteries

REPAIR:
- sail repair materials
- epoxy
- sealant

MEDICAL:
- appropriate first-aid supplies

SAFETY:
- EPIRB
- flares
- life raft
- appropriate emergency equipment

TOOLS:
Track enough information to determine whether particular repairs can reasonably be attempted.

Do not make inventory feel like RPG loot.

These are simply the finite things aboard the boat.

Once Shilshole is behind you:

WHAT IS ABOARD IS WHAT YOU HAVE.

No store.
No crafting economy.
No loot.
No artificial replenishment.

==================================================
REPAIRS
==================================================

Repairs consume appropriate inventory.

Examples:

DAMAGED IMPELLER
→ spare impeller

SPLIT HOSE
→ hose + clamps

TORN SAIL
→ sail repair material

ELECTRICAL FAULT
→ fuse / wire / connectors

LEAK
→ sealant / epoxy / repair materials

Avoid magic-item failures.

If the ideal replacement is unavailable, allow plausible improvisation when appropriate materials exist.

Improvised repairs should be less reliable.

Repair success should be influenced by:

- fatigue
- hunger/thirst
- sea state
- weather
- available tools
- materials
- severity
- previous repairs

A poor repair may initially appear successful and fail later.

==================================================
MAINTENANCE
==================================================

Not every problem should begin as a catastrophic failure.

Small observable problems should sometimes appear first.

Examples:

- unusual vibration
- chafing line
- small leak
- battery behaving strangely
- belt wear
- loose fitting
- abnormal engine temperature
- sail wear

An attentive player can catch some problems early.

Ignoring them may allow them to become larger failures.

Checking the boat a few thoughtful times per day should usually be sufficient under ordinary conditions.

==================================================
CASCADING CONSEQUENCES
==================================================

This is a critical Landfall principle.

Failure should usually emerge through understandable chains.

Example:

POOR ROUTING
→ longer voyage
→ dwindling provisions
→ reduced eating
→ poor recovery
→ fatigue
→ mistake
→ poor repair
→ equipment failure
→ further delay

Another:

BAD WEATHER
→ sail damage
→ repair material consumed
→ later damage
→ insufficient ideal material
→ improvised repair
→ reduced speed
→ longer voyage
→ dwindling supplies

The player should usually be able to understand afterward:

THIS IS HOW THINGS GOT BAD.

Do not kill the sailor because of one unlucky random number.

==================================================
SUCCESS
==================================================

Success does NOT require arriving in perfect condition.

A 21-day passage with abundant supplies and a healthy boat is successful.

A 31-day passage arriving with:

- patched sails
- little diesel
- limited food
- exhausted sailor

is ALSO successful.

The question is:

WHAT CONDITION WERE YOU AND THE BOAT IN
WHEN YOU FINALLY MADE LANDFALL?

==================================================
DISTRESS / EPIRB
==================================================

If the voyage becomes unsafe or impossible to continue, the player may call for rescue.

Provide an appropriate emergency/safety menu.

The player can activate the EPIRB.

ACTIVATING THE EPIRB DOES NOT END THE GAME.

THIS IS CRITICAL.

It changes the objective from:

REACH KAUAʻI

to:

SURVIVE UNTIL RESCUE.

The simulation continues in strict real time.

==================================================
AFTER CALLING FOR RESCUE
==================================================

Everything continues to matter:

- weather
- sea state
- boat condition
- flooding
- injuries
- fatigue
- food
- water
- remaining equipment
- EPIRB functionality
- actual position
- drift

Do NOT show:

RESCUE ARRIVES IN 07:32.

The player should not know exactly when help will arrive.

Internally, rescue time should depend on plausible factors such as:

- location
- distance offshore
- signal reception
- weather
- sea conditions
- nearby vessels
- rescue resources
- aircraft availability
- sailor/vessel condition

Provide restrained indications as rescue develops.

For example:

DISTRESS SIGNAL TRANSMITTING.

Later:

AIRCRAFT OVERHEAD.

Later:

VESSEL SIGHTED.

Later:

VESSEL ALTERING COURSE TOWARD YOU.

Only when the sailor is physically rescued does the voyage end.

==================================================
LIFE RAFT
==================================================

If the sailboat becomes untenable before rescue arrives, allow the player to face the decision to abandon ship.

Deploying the life raft is a major decision.

Do not make it routine.

If the player abandons the boat:

THE SIMULATION CONTINUES.

Inventory becomes limited to realistic emergency supplies aboard or carried into the raft.

The sailor must survive in real time until rescue.

The sailboat may disappear from view.

This should feel consequential.

==================================================
RESCUE OUTCOME
==================================================

Only actual rescue ends a rescue scenario.

A possible voyage record:

LANDFALL
VOYAGE 03

SHILSHOLE BAY → NORTH PACIFIC

27 DAYS
2,941 NM

VESSEL ABANDONED
CREW RESCUED

NO LANDFALL

Being rescued is different from dying.

Recognizing that a voyage has become unrecoverable and requesting rescue is GOOD SEAMANSHIP.

The ultimate responsibility is survival, not reaching Kauaʻi at any cost.

==================================================
DEATH
==================================================

The sailor can perish.

However, death should be:

- rare
- serious
- understandable
- usually preventable through good decisions
- preceded by evidence that the situation is becoming life-threatening

Do not create cheap deaths.

FOOD = 0 does not mean instant death.

WATER = 0 does not mean an immediate GAME OVER.

A damaged sail does not mean death.

Physical deterioration and danger develop through time and interacting circumstances.

The player should generally have an opportunity to recognize:

THIS VOYAGE IS NO LONGER RECOVERABLE.

and call for rescue.

==================================================
INTERFACE
==================================================

Preserve Landfall's sparse old marine-computer / terminal aesthetic.

Avoid:

- modern cards
- progress bars
- colorful meters
- icons
- RPG statistics
- conventional HUD design

Inventory might simply appear:

PROVISIONS

Oatmeal ............. 12 servings
Rice ................ 14 servings
Soup ................. 6 servings
Tuna .................. 8 servings
Crackers ............. 10 servings
Peanut Butter ......... 7 servings
Nuts ................. 13 servings
Dried Fruit ........... 9 servings
Coffee ............... 18 servings

> EAT
> BACK

The interface should communicate through words and quantities.

==================================================
SAVE SYSTEM
==================================================

ALL new systems must persist correctly.

Persist at minimum:

- actual boat position
- heading
- boat speed
- navigation state
- inventory quantities
- food quantities
- hunger
- thirst
- water
- fuel
- propane
- sleep history
- sleep pressure
- fatigue
- coffee consumption
- spoilage
- equipment condition
- repairs
- repair quality
- maintenance state
- distress state
- EPIRB state
- life raft state if applicable
- sailor condition
- relevant event history

Everything must reconcile correctly against REAL ELAPSED TIME when the player returns.

==================================================
IMPLEMENTATION STRATEGY
==================================================

DO NOT attempt to recklessly rewrite the entire game in one pass.

First inspect the existing code.

Then:

1. Explain briefly which requested systems already exist.
2. Identify which systems need modification.
3. Identify which systems are new.
4. Identify any conflicts with the existing implementation.
5. Create a sensible implementation order.
6. Implement the systems incrementally while preserving existing functionality.
7. Keep the architecture understandable and maintainable.
8. Test interactions between systems.
9. Do not remove existing functionality unless explicitly instructed.
10. Preserve the current working entry sequence and menu behavior.

If implementing every system safely in one response would risk destabilizing the current build, prioritize a stable foundation and clearly tell me which portions should be implemented in the following development pass.

DO NOT fake systems merely so they appear in the interface.

A system should either genuinely participate in the simulation or wait for the next implementation pass.

==================================================
FINAL TESTING
==================================================

Before returning the updated build, test conceptually for:

- returning after several real hours
- hunger progression
- thirst progression
- eating
- drinking
- food consumption
- cooking resource consumption
- spoilage
- sleeping while tired
- attempting sleep while well rested
- interrupted sleep
- coffee and sleep interaction
- inventory persistence
- equipment damage
- repairs consuming inventory
- fatigue affecting repairs
- long passage causing resource pressure
- boat speed affecting actual coordinates
- Puget Sound course restrictions
- open-ocean course changes
- distress activation
- continued simulation after EPIRB activation
- life raft transition
- rescue ending the voyage
- save/reload during all major states

Do not introduce artificial time advancement to test these systems in normal gameplay.

Preserve Landfall's strict real-time premise.

Return the complete updated index.html when finished.
