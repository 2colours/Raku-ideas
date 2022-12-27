## In recognition of
People who tried to do management tasks for the Raku community. In particular but not limited to:
- Elizabeth Mattijsen
- Zoffix Znet
- Juan Julián Merelo Guervós
- Aleks-Daniel Jakimenko-Aleksejev

## Explicit goals
- to retain maintenance of a higher proportion of modules
	- by finding volunteering new maintainers
	- by recovering original authors who seem willing
- push down the proportion of broken modules ("unbitrot" legacy)
	- cannot be installed
	- cannot be used to the slightest (immediate runtime problems)
	- deprecation notices, warnings all around
	- failing tests
- to increase consistency of conventions
	- extensions
	- naming conventions?
- gather more knowledge about the condition of the ecosystem
	- what should be switched from
	- what demands more maintenance
	- what is a good and safe choice to depend on
- pinpoint and possibly address Rakudo problems that seem relevant
## Implicit goals
- bring users, content creators, etc. together
- set up a precedent of semi-regular meetings for people contributing to Raku some way
- get people involved in deeper/more abstract Raku manners
	- creating content about Raku
	- participating in compiler/runtime development
	- participating in discussions about design/management/marketing
	- infrastructure, documentation... you name it
## Non-goals
- introduction to the Raku programming language
	- it's a noble goal but not within this scope
- to make "the right decisions" at all costs...
	- let's try to avoid bikeshedding and technical debates
	- it's more important to share work and progress than to collaboratively work on one thing

## ACTION PLAN
1. shoutout to possible participants:
	- volunteering authors who want to share their module with a broader audience
	- authors of modules to "unbitrot"
	- members who would like to get involved in the work
	- nothing to lose - let's try to use all possible channels as a kind of survey
	- it might be a good idea to take feedback on
		- "what you would like this to be"
		- "what time works for you"
	- however: no point in making some fully-blown survey, rather leave it to people how they want to respond
	- the end result is likely to be a harsh overestimation - anyway... if there seem to be only a couple of people willing to participate, it will be more up to them what they make out of it
2. preparations for the onset:
	- need to collect enough materials for 2 or 3 occasions
	- need to decide on organisation questions
		- occasion/time period
		- communication platform
			- real-time interaction preferred ("implicit goals")
			- but: those who cannot participate in a certain meeting shouldn't be left with nothing
3. announcement:
	- when there is roughly a month left until a properly prepared date/time period
	- more formal than the first "hit-up"
		- it would be preferrable to only have those people react who actually plan to show up
	- what the participants are expected to do prior
		- this also depends on the "quality and quantity" of the expected participants
		- choosing modules to work on
		- bringing complete or partial solutions
			- of issues proposed in the announcement
				- perhaps there could be an updated list of "suggestions"
			- of self-proposed/self-recognized issues
	- original module authors are an important part: it doesn't seem feasible to fork the whole universe
		- let's try to reach out to the authors of seemingly abandoned modules and ask them
			- if they are willing to take PR's and publish new versions
			- if they can pass ownership of modules they don't maintain anymore
4. the event:
	- this probably needs more actual experience to really tell
	- wouldn't expect most issues to be worked out "together" real-time
	- focus on individual stories, collect commonalities
	- widening the topic is welcome:
		- "a module for X would be nice"
		- "I came across this interesting paradigm"
		- "a common source of problems is X"
	- if some "off-topic" is useful: let's try to spawn a place for it
		- probably makes more sense somewhat later, in case interest solidifies

## Requirements
- let's reuse and repurpose https://github.com/Raku/ecosystem-unbitrot
	- it already has loads of issues for failing modules but it doesn't seem like a great idea to take them all
- let's find a way to collect and prioritise potential work
	- some automation can be reused probably
	- prefer REA over p6c
	- develop some considerations for how much something is worth fixing
		- how outdated is it, regarding use of Raku?
		- how complex is it? how easy would it be to just rewrite better?
		- how much are there better alternatives?
- _that's all I could think of now thank you have a wonderful day lol_