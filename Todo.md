- https://github.com/Leont/getopt-long6/issues/13
- **(STALLED)** https://github.com/Altai-man/docs.raku.org/issues/79
	- CIAvash reworked it; I'm not fully content but it may turn out to be good
		- migrated as https://github.com/Raku/doc-website/issues/30
	- https://codepen.io/trevoreyre/pen/JjGxLEm
	- https://jsuites.net/v4/dropdown-and-autocomplete
- **(FINISHED)** https://github.com/Altai-man/docs.raku.org/issues/72
- **(STALLED)** https://github.com/Altai-man/docs.raku.org/issues/31
	- how does it relate to https://github.com/Raku/doc-website?
- **(FINISHED)** watch https://www.youtube.com/watch?v=NYBc3tQEIh4
- **(BIG)** Raku discord bot
	- port Bojler from Python (private link incoming: https://bitbucket.org/2colours/boggler-bot/src/master/)
	- music bot???
- **(BIG)** Raku desktop app (with Electron or GTK)
- **(BIG)** migrate modules.raku.org to Raku (currently Perl 5 + Mojolicious framework)
- https://github.com/2colours/HTML-Tag/issues/2
- https://github.com/2colours/HTML-Tag/issues/1
- docker run -v c:/Users/bruce:/mnt/me --rm -it jjmerelo/alpine-raku:2020.01 /mnt/me/bb02_c6.raku
- Ddt:
	- description generation should be POD6 based, not just a regex
	- generate resources part of META6 from the content of the folder
	- fix 'provides' generation
		- to-module is too optimistic
- https://github.com/Raku/raku.org/issues/174
	- https://github.com/raku-community-modules/Web-Template
		- **(FINISHED)** https://github.com/raku-community-modules/Web-Template/issues/5
- port for Text::Extract::Word of Perl5
	- tbrowder likes the idea but would want a different name with MSWord in it
	- first: demo with Inline::Perl5?
	- then
		- adopt the OLE module of Jeff Goff (R.I.P)
		- actually port the code of the Perl5 module depending on it
- **(FINISHED)** Coffeescript to JS migration of https://github.com/Raku/atom-language-perl6
	- the workflow has also been changed: the raku files under `dev/` are the input
- Tatoeba API wrapper in Raku
  - https://github.com/Tatoeba/tatoeba2/issues/2669
  - https://github.com/Tatoeba/tatoeba2/pull/3064
- add tests
	- to Roast
	- https://github.com/doomvox/darkroast
- RakuAST stuff
	- quotes: `m//`, `s// = 'blah'` (??), `tr///` kind of stuff
	- `&variables`
		- https://discord.com/channels/538407879980482560/633753335119478795/1057862136572956714
		  "note to self: PRODUCE-META-OBJECT, container descriptors"
	  - conversion "functions" like `Bool('almafa')`
  - **(FINISHED)** https://github.com/pierre-vigier/Perl6-Data-MessagePack
	  - added to calendar: 4th february
	  - still doesn't show up on the site :(
  - clearup of storage of `Map` implementations
	  - https://github.com/rakudo/rakudo/pull/5182
  - `dd` sub cleanup
	  - it often generates really bad lines
		  - on unnamed data
		  - on items in a composite data structure
  - solidifying Fez
	  - more tests
		  - perhaps with mocked backend?
	  - more documentation