# gwn-word-api-docs

> Open documentation and TypeScript typings for the dictionary + word-finder
> API powering [A2Z Word Finder](https://a2zwordfinder.com/), part of the
> [Grande Web Network](https://grandewebnetwork.com/) family.

## Why this repo exists

If you're building a word-game client, crossword helper, Scrabble scoring
engine, or anything that needs fast dictionary lookups across 11 languages,
these endpoints give you low-latency lookups without running your own server.

## Endpoints (v1)

### Anagram / unscramble

```
GET https://a2zwordfinder.com/api/v1/anagrams?letters=TESTING&lang=en&limit=20
```

Response shape:

```ts
interface AnagramResponse {
  letters: string;     // echo of input
  lang: string;        // en, es, fr, de, it, pt, nl, sv, no, da, fi
  count: number;
  words: Array<{
    word: string;
    score: number;     // Scrabble tile score
    length: number;
  }>;
}
```

### Pattern match (crossword-style)

```
GET https://a2zwordfinder.com/api/v1/pattern?p=C_A_E&lang=en&limit=50
```

Underscore characters (`_`) are blanks. Returns all words in the requested
language dictionary matching the pattern.

### Word validation

```
GET https://a2zwordfinder.com/api/v1/validate?word=QUIXOTIC&lang=en
```

Returns `{valid: boolean, source: "sowpods|twl|enable"}`.

## TypeScript types

```ts
export type GwnLang = "en" | "es" | "fr" | "de" | "it" | "pt" | "nl" | "sv" | "no" | "da" | "fi";

export interface GwnAnagramResult {
  word: string;
  score: number;
  length: number;
}

export interface GwnAnagramResponse {
  letters: string;
  lang: GwnLang;
  count: number;
  words: GwnAnagramResult[];
}
```

## Rate limits

Anonymous: ~60 req/min per IP. If you need more, create a free account at
[members.grandewebnetwork.com](https://members.grandewebnetwork.com/) — signed
requests get 1,000 req/min.

## Related GWN tools

- [A2Z Word Finder](https://a2zwordfinder.com/) — the primary word-finder
- [Letters Into Words](https://lettersintowords.com/) — simpler unscrambler
- [Word Unscrambler.ai](https://wordunscrambler.ai/) — AI-assisted variant
- [Puzz.com](https://puzz.com/) — live multiplayer Scrabble using this API

## Contributing

Typo fixes welcome via PR. For protocol additions, open an issue first.

## License

[CC0-1.0](LICENSE).

---

_Auto-maintained by [awesome-gwn-word-tools](https://github.com/chimera00/awesome-gwn-word-tools).
 Part of the [Grande Web Network](https://grandewebnetwork.com/)._
