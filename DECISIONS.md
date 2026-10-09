# Decisions log: AUDIO-1142 (car radio shuffle)

Tickets never cover everything. When you hit a situation the ticket doesn't
describe, you still have to make the code do _something_. This file records what
you chose, so that your lead, QA and whoever maintains this code after you can
see that it was a deliberate decision and not an accident.

For every decision:

1. **Write it down here**, using the template below.
2. **Write a test that pins it down**, so that nobody changes the behaviour by
   accident later.
3. **Note who should really make the call.** You're making a sensible choice so
   that you can keep working, but some of these questions belong to someone
   else. Say who you would ask, and what you would ask them.

Keep entries short. One or two sentences per field is plenty.

---

## Template

### D? – Short name for the decision

- **Situation:** What happened that the ticket doesn't cover?
- **What the ticket says:** Quote it, or write "Nothing".
- **Options considered:** The choices you could have made.
- **Decision:** What the code does.
- **Why:** Your reasoning.
- **Test:** The name of the test that checks it.
- **Who should decide:** Who you'd ask, and the question you'd put to them.

---

## Decisions
  Situation - A few test werent passing due to a - in the expected.
  What the ticket says: Nothing
  Options considered: I could go throght the name and if the - is seen it can skip it or read it as if its meant to be there.
  Decision: The code looks for the first position of "-" in the writing, when this is found it becomes the size_t pos. substr extracts parts of the string which tells it where the artist name should be and where the song name should be.
  Why: After trying to find out a way of it to work, when looking it up I thought that this was the quickest and easiest way to do it.
  Test: ParaseNormal spilt was meant to be the one fixed but it also fixed, ArtistDashTitle. Splits on Fist seporator.
  Who should ask: I'd ask a friend or a lecturer and ask them to explain to me more on how the subst goes through the string because its hard enough to understand, Id also ask why it fixes so many issues with so little code.

  Situation - Artist is unknown
  What the ticket says: Nothing
  Options considered : Putting an if statement after previously written code so that if the artist is put in as unknown and the string is empty to make it equal to Unknown artist
  Decision: I added a if statemnet in the song constructor which assigns the artist string to "Unknown Artist" if the string is empty.
  Why: It seemed the easiest way to do it without breaking anything and not writting to much code.
  Test: MissingArtistBecomesUnknown
  Who should ask: Id ask the lecturer if that the easiest way of doing it becuase it seems it but it mightnt be.

  Situation: shuffle function needing to shuffle
  What the ticket says: Nothing
  Options considered: How to make it so that the songs get shuffled even when asked for more than there is such as in this example 20 although only about 10 there.
  Decision: Adding a for loop so that as long as there are songs the i++ changes the song which makes it longer.
  Why: Again seemed like the plainest way to do it without writing to much code
  Test:TwoCallsGiveDifferentLists, ReturnsRequestedSong
  Who should I ask: The lecturers on explaining the whole function in greater detail since not much of it was used.


### D1 (Example) – Extra spaces inside a name

- **Situation:** The spreadsheet has a line with **two** spaces between
  "Neon" and "Saints":
  >
  ```
  Neon  Saints - Overdrive
  ```
  > With each space shown as `␣`, that's `Neon␣␣Saints␣-␣Overdrive`.
- **What the ticket says:** Nothing. The spec says whitespace _around_ the
  artist and title is ignored, but doesn't mention spaces inside them.
- **Options considered:**
  - Keep the name exactly as written: `Neon␣␣Saints`
  - Squash repeated spaces down to one: `Neon␣Saints`
- **Decision:** Names are kept exactly as written. Only leading and trailing
  spaces are removed.
- **Why:** It's the simplest rule, and changing a name could break a real one
  that's meant to look unusual.
- **Test:** `SongParse.KeepsSpacesInsideNames`
- **Who should decide:** The audio team. If `Neon␣␣Saints` and `Neon␣Saints`
  both appear in the spreadsheet, are they the same artist? With this
  decision, those two songs won't be equal.
