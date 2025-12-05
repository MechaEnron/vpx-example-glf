
# Judge Dredd Remastered

## Required Modes

### |Attract Mode|

**Videos playing on loop:**
- JD beating up criminals
- Loading his gun
- Overview of the city
- Pages flipping through the many comics from '77 - Present
- Riding the Lawmaster
- Highscores
- Credits

`StartEvents: reset_complete, game_ended, cancel_login`

`StopEvents: login_started, game_started, stop_attract_mode`

```
timed_switches:
    login_mode:
        switch_tags: start
        time: 200
        events_when_released: login_started
```

Must adjust `glf.vbs` file to account for long press:

```
Public Sub Glf_KeyDown(ByVal keycode)
    If glf_gameStarted = True Then
		If keycode = StartGameKey Then
			If glf_canAddPlayers = True Then
				Glf_AddPlayer()
			End If
			DispatchPinEvent "s_start_active", True
		End If
	Else
		If keycode = StartGameKey Then
			DispatchRelayPinEvent "request_to_start_game", True
			DispatchPinEvent "s_start_active", True
		End If
	End If
```

### |Login Mode|

- Accessed when a player long-presses the StartButton (>=2 seconds)
- Player enteres 3-letter initials to 'log in' and track variables/stats
- Last initials entered remain as default for ease of signing in

`StartEvents: login_started`

`StopEvents: cancel_login, game_started`

```
timed_switches:
    login_mode:
        switch_tags: start
        time: 200
        events_when_released: cancel_login
```

### |Base Mode|

#### Scoring
- Slings: 
    - Left: 1,930
    - Right: 1,930
- StandUp Targets:
    - Row of 3 StandUp Targets (sw18):
        - Unlit: 50,000
        - Advance Crime Level: 50,000 + 1,000,000
    - Top Right Narrow StandUp (sw25): 50,000
    - Bottom Left StandUp (sw27): 50,000
    - Narrow StandUp at Left Ramp Entrance (sw36): 50,000
- Drop Targets:
    - Unlit/SteadyLit 'JUDGE' DT (sw54-sw58): 200,000
    - Blinking 'JUDGE' DT (sw54-sw58): 200,000 + 500,000
- Reactor:
    - First reactor rollover (sw26): 400,000
    - Second reactor rollover (sw53): 600,000
    - Reactor Target (sw68):
        - 1st time & all 'ODD' Hits: 1,000,000
        - 2nd time: 1,000,000 + 2X BONUS
        - 4th time: 1,000,000 + 5,000,000
        - 6th time: 1,000,000 + LITE EXTRA BALL
        - 8th time & all 'EVEN' Hits: 1,000,000 + 5,000,000
- Ramps:
    - Right Ramp (sw76):
        - 1st time Starts as Green Crime: 500,000 + 1,000,000
        - Subsequent times: +500,000 (e.g., 1M, 1.5M, 2M,..)
    - Air Raid Ramp: [manual] 500,000 and Start Air Raid Feature
    - Center Ramp:
        - Base 100,000
        - 2nd Time: 500,000
        - Increase by 500,000 each additional time until max 5M
- Loops:
    - Big Loop value:
        - First hit: trigger 50,000 rollover on entry (sw33), 50,000 on exit (sw72), or reverse
        - Quickly hitting Top Right Orbit Opto (sw72) into Left Rollover (sw33)
        - Scores 1,000,000 and increases by 1,000,000 with each quickly hit subsequent loop
        - Value resets after missing consecutive shot
    - Top Right Loop:
        - Trigger 50,000 rollover on entry (sw35), 50,000 on exit (sw72)
- Rollovers:
    - In-lane rollovers (sw17, sw34, sw43): 50,000
    - Out-lane rollovers (sw16, sw42): 100,000
    - Left Rollover (sw33): 50,000
    - Top Right Orbit Opto (sw72): 50,000
- Sniper Tower VUK:
    - Base 500,00
    - Starts as Green Crime so first hit really gets 50,000 + 1,000,000
- Judge Subway: 100,000
- Air Raid

### |Pursuit - Chain Link Mode|

### |Black Out - Chain Link Mode|
Can be source of point farming. **Remastered** rules will degrade points on ramp hits.

- Hits 1–4:  100% value (original intended double-scoring value)
- Hits 5–8:   50% value
- Hits 9–12:  25% value
- Hits 13+:   10% “token” value (just to keep shots worth *something*)


### |Sniper - Chain Link Mode|

### |Battle Tank - Chain Link Mode|

### |Bad Impersonator - Chain Link Mode|

### |Melt Down - Chain Link Mode|

### |Safe Cracker - Chain Link Mode|

### |Manhunt Millions - Chain Link Mode|

### |Stake Out - Chain Link Mode|

### |Ultimate Challenge (6-ball Mode) - Chain Link Mode|

### |Dead World - Multiball|

### |Ultimate Challenge (4-ball Mode) - Multiball|

### |Crime Boss - Multiball - **REMASTERED**|

### |Bonus|

### |Tilt|

## Variables

### |Player Variables (per Game)|
>- Score
>- Ball
>- Crime Level
>- Multiballs earned (Increase value of jackpot based on number of MBs)

### |Player Variables (Persistent)|
>- Captured Criminals
>- Games Played
>- Highest Score
>- XP system to increase rank in the Judges?
>- Achievements


### |Machine Variables|

## Misc Notes

### Criminals to collect
>**Major Archvillains & Mega-Threats**
>- Judge Death – Leader of the Dark Judges
>- Judge Fear
>- Judge Mortis
>- Judge Fire
>- Judge Kraken – Corrupted clone of Dredd
>- Sabbat the Necromagus – World-ending necromancer**
>- The Mutant Brotherhood / Brother Morgar
>- Judge Cal – Dictator of Mega-City One
>- Chief Judge Volt – Fell to insanity & tyranny
>- P.J. Maybe (Philip Janet Maybe) – Serial killer, political manipulator
>
>**Classic Villains (Early-Era)**
>
>- The Angel Gang (Pa Angel)
>- Mean Machine Angel
>- Fink Angel
>- Junior Angel
>- Link Angel
>- Nero Narcos – Cyborg Mafia boss of the Robot Wars
>- Captain Skank – Mutant pirate leader
>- The Ape Gang (Don Uggie Apelino) – Ape Mafia
>- Uncle Fester – Ape Gang consigliere
>- Joe Bananas – Ape Gang soldier
>
>**Mid-Era Crime Syndicates & Perps**
>
>- Muzak Killer (Kenny Who?) – Vigilante artist/serial killer
>- Chopper (Marlon Shakespeare) – Although sympathetic, still a wanted criminal
>- The Hunters Club – Cannibal thrill killers (any member may be used)
>- The Bloodline Gang – Mutant criminals
>- Kreegs – From the Apocalypse War
>- Bludd the Berserker – Crazed warrior in Cursed Earth
>- The Organ Smugglers / Organleggers (leader of your choice)
>- The Frendz Mafia (Don Vito Frendz)
>- Whitey (William White) – First criminal Dredd ever sent to the Iso-Cubes
>- The Invisible Man (Clarkus Goom) – Cloaked criminal
>
>**Late-Era / Modern-Era Threats**
>
>- Mr. Bones – Mutant gang leader
>- The Chaos Bug Cult (Brother Grice)
>- The Serial Killer "The Stig"
>- The Judda clones (Kill-Judges)
>- The Scrawl (Graffiti terrorist)
>- The Psychic Assassin “Faustus”
>- Archie the Robot / Rogue Robot Perps
>- The SJS traitor Judge Gerhart
>- Sinfield – Corrupt Judge/traitor Chief Judge
>- The Titan Ex-Judges (Any member, e.g., Gratius)
>
>**Mutants, Freaks, and Cursed Earth Criminals**
>
>- The Mutie Slavers (leader "Slaughterhouse Dave")
>- The Brotherhood of Trash (any named member)
>- The Mutant Horse Warriors
>- The Resyk Flesh Harvesters
>- The Chimera Mutant Gang
>- The Cursed Earth Desperado “Stump Gun Yancy”
>- The Cannibal Muties of Crater City
>- The Spug Squad – Petrol-bombing juves
>- The Rad-ghoul “Moloko”
>- Marauder King “Kleg-Hunter Vox” – Kleg-ally aligned criminal

