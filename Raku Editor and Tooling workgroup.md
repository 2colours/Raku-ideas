I will try to not overkill this but also kind of explain the motives and goals for this entity.
# Overture
Raku's tooling is not really appealing to newcomers. It is uncomfortable and particularly bad for marketing.
- There is little support to most editors (if at all) and even that little support often comes under the name `Perl 6`.
- We barely have one decent highlighter - even the "official" [atom package](https://github.com/Raku/atom-language) was lying around for years without any maintenance, while [atom even got discontinued](https://github.blog/2022-06-08-sunsetting-atom/).
- People have kept asking for an LSP and now we do have one not too outdated (thanks to Brian Scannell) but it needs support.
- It bothers me personally that [Discord](https://discord.com/) supports dozens if not hundreds of languages in its markdown formatting thanks to [highlight.js](https://highlightjs.org/) and Raku is nowhere among them. It won't just magically pop up.
- There are [some](https://github.com/Raku/nqp/tree/main/src/vm/moar/profiler) [profilers](https://github.com/tadzik/p6profiler-qt) but nothing really maintained.
The overall message is (my two cents) that we in fact **do have** the knowledge, resources and possibility to improve the situation and it would do a great service to the overall look and feel of the technical offer.
# Goals
This is something that the participants will have to set since we will be on our own either way. I can say my goals and give some clues about what I can imagine additionally:
- get Raku highlighting to Discord
	- this is definitely a final goal, whatever leads to it is good to go, I'd hope that it can be connected to existing highlighter efforts
- "atom highlighter"
	- repository polishing
		- get rid of Atom, focus on the Textmate files and how to obtain them
		- sort issues, maybe get a new issue template
	- actually solve highlighter issues
		- needs [Textmate grammar](https://markdown-all-in-one.github.io/docs/contributing/textmate-language-grammar.html#introduction) knowledge (don't count on people who already know it, there might be none)
- HTML-generating highlighter
	- could use the Textmate-based highlighter
	- could be plain Raku parsing for greater accuracy (possibly no prior art though)
- BScan's [RakuNavigator](https://github.com/bscan/RakuNavigator) could become the state of art Raku LSP
	- many issues are related to Rakudo knowledge - hopefully we can attract some help to specific questions
- Collecting profilers and taking care of them
	- one obvious example: the built-in profiler could have a better, more up-to-date HTML template, making use of the history API for proper navigability
- Rakudoc a.k.a POD6 related tooling
	- it also needs highlighting
	- Github rendering would be truly awesome
	- there is a kind of [wysiwyg editor](https://github.com/podlite/podlite-desktop) to it that might deserve some care
	- this is probably a shared field of interest with documentation and overall language design