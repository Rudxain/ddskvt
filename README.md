# Drop-Dead Simple Key-Value Tree data format

```
If you are...
	Tired of JSON's obnoxious quotes
		Like\ these `{"ugly": "redundant"}`
	Confused by Tom's "Obvious" "Minimal" Language
		WTF is the diff between
			`[table]`
			and
			`[[table]]`
			???
	Got sent to an asylum, thanks to YAML
		https://noyaml.com
```

Then this format is for you!

This format isn't just minimalist, it's [brutalist](https://en.wikipedia.org/wiki/Brutalist_architecture). The motto is **"Pure structure, no semantics"**. This is a *data format* not a _language_.
This format embraces the fact that schemas are inevitable, so you are expected to explicitly define a schema or implicitly assume it.

## FAQ
> If it's so simple, why trees? Aren't trees complicated?

No, the tree-like structure of this format is merely a consequence of recursion:
```
table is set of entries
entry is key-value pair
key is string
value is string or table
```
Trees are **everywhere** in nature, math, and comp-sci, even in unexpected places. So I'd argue this format must be able to express them easily.

If you insist on flatness, INI exists ;)

## Name
The name is meant to evoke a "no bullshit" vibe.

The "drop dead" part can be interpreted as "dead-simple and elegant" or as an [insult to other formats](https://www.urbandictionary.com/define.php?term=KYS), [depending on your mood](https://github.com/git/git/blob/73fd77805fc6406f31c36212846d9e2541d19321/README.md?plain=1#L55-L66) ;)

File extension is `.skvt`. I suggest you pronounce it as "scot".
People can make jokes about "TOML skvt" being similar to "[Tom Scott](https://en.wikipedia.org/wiki/Tom_Scott_(YouTuber))"

## Grammar & Types
This is the normative part of the specification

> [!IMPORTANT]
> I haven't fully settled on this, so the format is technically unstable. Expect breaking-changes

The only data-types are
- UTF-8 text string
- table of unordered key-value entries
- ordered list: this might be removed from the spec

Line-breaks (`\n` only; `\r` is undefined for now) delimit entries, ` ` delimits the key from its value.
So far, I think the 1st space should be assumed to be the delimiter, rather than the last one.
If a key is associated to a table or list value, then any ` ` in the key-string should be assumed to be a character like any other.

Indentation is significant, and specifies nesting. Only "hard" tabs (`\t`) because I [hate YAML](https://noyaml.com) and [tabs are superior](https://lea.verou.me/blog/2012/01/why-tabs-are-clearly-superior)

I'm hesitant to support comments, as the empty key can be used as alternative:
```
name foobar
 this is a comment
version 0.1.0
dependencies
	yeet 0.2
	 version from the future, lol
	anyhow 69.0
	regex 1.0
```

Implementors are free to choose how to handle duplicate keys. For debugging, I recommend printing an error or warning

## Usage in the wild
This format is so damn simple that you might be already using it!

- Many special files in Linux `/proc/*` have similar format
- [This tool I made](https://github.com/Rudxain/fr3) uses a flat subset of this format, where last ` ` delimits key-value
- etc... (let me know of other examples)

## See also
- [CSVZ](https://github.com/secretGeek/csvz)
