# FitFindr

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, every
> command, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> python app.py listings --full -n 6      # read the data (Milestone 1)
> python app.py fields                    # what you can filter on
> python app.py ask 'vintage graphic tee under $30'
> ```
>
> All three tools are stubs, so that last command will do nothing useful yet.
> That's the starting position.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     This is your submission. Fill each section in as you finish the milestone
     it belongs to — don't leave it all to the end.

     Unit 3 asks for the first five sections. Unit 4 adds the five below them.
     Leave the unit 4 sections alone until then; they're here so you know
     what's coming.

     Everything is pasted as TEXT. No screenshots, no images, no video links.
     A typed block of output gets full credit; a picture of the same output
     gets none.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 3 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Three or four sentences: what a user asks for, and what they get back. -->

     The user asks for the kind of dress or clothes they want and they either provide the size or their budget for it. The agent gives them back a teh clothes that would work with it and also writes a caption for that. 



---

## Tool Inventory

<!-- Four lines per tool. This is worth 2 points and it's the single most
     common place students lose them.

     "Returns a list" earns NOTHING. The description has to say what is IN
     the list.

     The empty case isn't optional either — it's the thing your loop branches
     on, and if you don't decide it here you'll discover it as a crash in
     Milestone 5. -->

### `search_listings`

- **What it does:** It searches through the listings that matches the description and optially applies price t and size filters.
- **Inputs:** size(string), description(string), max_price(float)
- **Returns:** It returns a list which matches the descriptions.
- **When it has nothing:**  If nothing matches the descriptions then it returns an empty list.

### `suggest_outfit`

- **What it does:** When a item is given along with the wardrobe, this function suggests one or two outfits.
- **Inputs:** new_item(list), wardrobe(listing dict)
- **Returns:** A string with outfit suggestions.
- **When it has nothing:** It returns general outfit sugestions rather than empty string.

### `create_fit_card`

- **What it does:** This fucntion generates a short caption someone would actually post about the find.
- **Inputs:** outfit(string), new_item(listing dict)
- **Returns:** This function returns two-to-four sentence caption.
- **When it has nothing:** When the outfit is empty the it return an decriptive message rather than raising error.

---

## Planning Loop

<!-- Your branch rule, stated as a rule — the condition AND both paths — plus
     the file and function that holds it.

     Like this:
       "If search_listings returns an empty list, put a message in the session
        and stop. Otherwise take the first result and go to suggest_outfit."
        — agent.py::run_agent

     The grader checks your code against what you claim here, so the file and
     function have to be real. -->

**Branch rule:** If search_listings returns an empty list, put a message in the session and stop. Otherwise, take the first result and go to suggest_outfit.

**Where it lives:** `agent.py::run_agent`

**How the query is parsed:** <!-- regex, string splitting, or asking the model — say which --> The query is parsed regular expressions to extract the search description and optional filters such as size and maximum price.

**What moves through the session:** <!-- which fields, in what order --> The session stores the user's query first, followed by the search results. If a result is found, the first listing is stored and passed to suggest_outfit. If no results are found, a message is stored in the session instead.

---

## Sample Run

<!-- Two things go here.

     1. One FULL query and its output, pasted as text.
     2. Your three per-tool terminal tests — the command and what it printed. -->

**One full query**

```
$ python app.py ask 'vintage graphic tee under $30'

```

**The three tools, tested one at a time**


```
$ python -c "from tools import search_listings; print(search_listings('graphic tee', max_price=30))"

```
* Output:
[{'id': 'lst_002', 'title': 'Y2K Baby Tee — Butterfly Print', 'description': 'Super cute early 2000s baby tee with butterfly graphic. Fitted crop length. Tag says medium but fits like a small.', 'category': 'tops', 'style_tags': ['y2k', 'vintage', 'graphic tee', 'cottagecore'], 'size': 'S/M', 'condition': 'excellent', 'price': 18.0, 'colors': ['white', 'pink', 'purple'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_006', 'title': 'Graphic Tee — 2003 Tour Bootleg Style', 'description': 'Vintage-style bootleg tee with faded graphic. Slightly boxy fit. 100% cotton, soft and worn-in.', 'category': 'tops', 'style_tags': ['graphic tee', 'vintage', 'grunge', 'streetwear', 'band tee'], 'size': 'L', 'condition': 'good', 'price': 24.0, 'colors': ['black'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_017', 'title': 'Mesh Long-Sleeve Top — Black', 'description': 'Sheer black mesh long-sleeve. Great for layering under a graphic tee or over a bralette. Stretchy material, fits true to size.', 'category': 'tops', 'style_tags': ['y2k', 'grunge', 'goth', 'layering'], 'size': 'S/M', 'condition': 'excellent', 'price': 15.0, 'colors': ['black'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_033', 'title': 'Vintage Band Tee — Faded Grey', 'description': 'Faded grey band-style tee with distressed graphic. Crew neck. Fits boxy. Well-loved but no holes or major damage.', 'category': 'tops', 'style_tags': ['vintage', 'grunge', 'band tee', 'graphic tee', 'streetwear'], 'size': 'L', 'condition': 'fair', 'price': 19.0, 'colors': ['grey', 'charcoal'], 'brand': None, 'platform': 'depop'}, {'id': 'lst_011', 'title': 'Low-Rise Cargo Pants — Khaki', 'description': 'Y2K era low-rise cargo pants. Lots of pockets. Khaki color, slightly distressed at the hems. Great for layering with a long tee.', 'category': 'bottoms', 'style_tags': ['y2k', 'cargo', '2000s', 'streetwear'], 'size': 'W29', 'condition': 'fair', 'price': 27.0, 'colors': ['khaki', 'tan'], 'brand': None, 'platform': 'poshmark'}, {'id': 'lst_015', 'title': 'Vintage Graphic Hoodie — Faded Black', 'description': 'Faded black pullover hoodie with barely-visible vintage graphic on the chest. Cozy interior. Some pilling but adds to the worn-in look.', 'category': 'tops', 'style_tags': ['vintage', 'grunge', 'graphic', 'streetwear'], 'size': 'L', 'condition': 'fair', 'price': 26.0, 'colors': ['black', 'charcoal'], 'brand': None, 'platform': 'depop'}]

```
$ python -c "from tools import suggest_outfit; from utils.data_loader import get_example_wardrobe, load_listings; print(suggest_outfit(load_listings()[0], get_example_wardrobe()))"

```
* Output:
Here are two outfit suggestions featuring your new vintage Levi's 501 jeans, styled using pieces from your existing wardrobe:

### Outfit 1: Casual & Cozy Everyday
*A classic, effortless look that leans into the vintage feel of the jeans with comfortable basics.*

* **Bottoms:** Vintage Levi's 501 Jeans (Medium Wash) *(New Item)*
* **Top:** **Oversized grey crewneck sweatshirt** *(w_004)* — let the cozy, relaxed fit contrast with the straight-leg cut of the jeans.
* **Shoes:** **Chunky white sneakers** *(w_007)* — adds a fresh, clean element to tie the casual grey and blue tones together.
* **Accessories:** **Brown leather belt** *(w_009)* to cinch the waist and **Black crossbody bag** *(w_010)* for everyday functionality.

---

### Outfit 2: Edgy Streetwear
*A cool, slightly grunge-inspired look using contrasting denim and structured black pieces.*

* **Bottoms:** Vintage Levi's 501 Jeans (Medium Wash) *(New Item)*
* **Top:** **White ribbed tank top** *(w_003)* tucked in for a fitted silhouette.
* **Outerwear:** **Vintage black denim jacket** *(w_006)* worn layered over the tank for a double-denim moment (medium wash + black denim looks great together).
* **Shoes:** **Black combat boots** *(w_008)* — grounds the outfit and leans into that vintage, slightly rugged aesthetic.
* **Accessories:** **Brown leather belt** *(w_009)* and **Black crossbody bag** *(w_010)*.

```
$ python -c "from tools import create_fit_card; from utils.data_loader import load_listings; print(create_fit_card('jeans and white sneakers', load_listings()[0]))"

```
* Output:
Nothing beats the effortless cool of a classic outfit featuring crisp white sneakers and these vintage Levi's 501 jeans. The medium wash and subtle knee fading give them that perfectly broken-in look right from the start. Grab this timeless piece for just $38.00 over on my Depop before they're gone! 

#vintage #classic #denim #streetwear

---

## How I Used AI

<!-- Two specific moments. What you asked, what came back, what you changed.

     "I used Claude to help me code" is not enough.

     "I gave Claude my search_listings spec. It returned None on no match
     instead of an empty list, so I changed it" is the level we want. -->

**Moment 1**

- *What I asked for:* I asked Claude to review and correct my search_listings implementation based on the provided requirements.
- *What came back:* It suggested filtering listings by price and size first, then calculating keyword overlap between the user's description and the listing information.
- *What I changed:* I updated my search logic to filter by max_price and size, rank listings using keyword overlap, and return an empty list when there are no matches.

**Moment 2**

- *What I asked for:* I asked ChatGPT how to implement the planning loop while making the session state visible between tools.
- *What came back:* It suggested storing the result of each tool in the session and having the next tool read its input back from the session. It also showed where to branch when search_listings returns an empty list.
- *What I changed:*  I implemented the branch so the agent stores an error message and stops when there are no search results. When results exist, I store the first result in session["selected_item"] and pass the session values through suggest_outfit and create_fit_card.

**Moment 3**

- *What I asked for:* I asked Claude to on the use cases of the MCP and the actual flow of that.
- *What came back:* It gave me the use case of MCP and how it actually interacts which the application or project.
- *What I changed:* Based on the above files I was able to find out what files do I need to interact with.

<!-- ═══════════════════════ UNIT 4 — THE TEST ═══════════════════════

     Don't fill these in during unit 3.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Run Log — Before

<!-- Five criteria, five tries each, in this exact format.

     Five, because your criteria are written out of five. Mark each try PASS
     or FAIL, count the passes, and read that count against your target — a
     row targeting 4 of 5 with three PASS cells is MISSED (3/5).

     `python run_eval.py --label before` runs everything and writes the table
     into results/. Paste it here and fill in the verdicts. -->

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. Full three-tool run returns a fit card  | 4 of 5 | PASS | PASS | PASS | PASS | PASS | MET |
| 2. Empty search stops before tool 2 | 5 of 5  | PASS  | PASS | PASS  | PASS | PASS | MET |
| 3. Item in session matches item passed on | 5 of 5  | PASS  | PASS  | PASS | PASS  | PASS  | MET |
| 4. Fit card mentions the item's name and price| 4 of 5 | PASS | PASS  | PASS  | PASS | PASS  | MET |
| 5. Over-budget query returns nothing over the limit | 5 of 5 | PASS  | PASS | PASS  | PASS | PASS | MET  |

**Real output from one try**, pasted as text, naming the file and function
that produced it:

```
Criterion 1: 
File: run_eval.py
Function: run_eval.py::main
- Query: `designer ballgown size XXS under $5`
- Wardrobe: example

Try 1

- stopped early: no
- selected_item: Y2K Baby Tee — Butterfly Print ($18.0, depop)
- search_results: 10

Outfit suggestion:


Here are 2 outfit suggestions incorporating your new Y2K butterfly baby tee with pieces from your wardrobe:

### Outfit 1: Classic Y2K Streetwear
Lean into the early 2000s aesthetic by balancing the fitted crop top with relaxed denim and chunky footwear. 
* **Top:** Y2K Butterfly Baby Tee (New item)
* **Bottoms:** Baggy straight-leg jeans, dark wash (`w_001`)
* **Shoes:** Chunky white sneakers (`w_007`)
* **Bag:** Black crossbody bag (`w_010`)
* **Why it works:** The ultra-fitted baby tee contrasts perfectly with the high-waisted, baggy fit of the dark wash jeans for an authentic Y2K streetwear silhouette. Finish with chunky sneakers and your black crossbody for an effortless day-to-day look.

### Outfit 2: Edgy Contrast
Mix the playful, nostalgic butterfly print with some harder, grunge-inspired textures.
* **Top:** Y2K Butterfly Baby Tee (New item)
* **Outerwear:** Vintage black denim jacket (`w_006`)
* **Bottoms:** Wide-leg khaki trousers (`w_002`)
* **Shoes:** Black combat boots (`w_008`)
* **Accessories:** Brown leather belt (`w_009`)
* **Why it works:** Pairing the feminine baby tee with wide-leg neutral trousers creates a cool high-low mix. Tossing on the slightly cropped black denim jacket and lacing up your black combat boots grounds the outfit and adds a nice touch of edge.


Fit card:


Channel your inner early 2000s pop star with this adorable Y2K butterfly baby tee, priced at just $18 over on my Depop! I love styling it with baggy denim and chunky sneakers for the ultimate effortless streetwear vibe. Grab it before it's gone and let your inner butterfly fly! 🦋✨


Trace:


[1] search_listings
      in:  dict with keys: description, size, max_price
      out: 10 items: Y2K Baby Tee — Butterfly Print, Graphic Tee — 2003 Tour Bootleg Style, Vintage Band Tee — Faded Grey … +7 more
[2] suggest_outfit
      in:  dict with keys: item, wardrobe
      out: Here are 2 outfit suggestions incorporating your new Y2K butterfly baby tee with pieces from your wardrobe:  #…
[3] create_fit_card
      in:  dict with keys: outfit, item
      out: Channel your inner early 2000s pop star with this adorable Y2K butterfly baby tee, priced at just $18 over on …

Criterion 2: 
File: run_eval.py
Function: run_eval.py::main
- Query: `designer ballgown size XXS under $5`
- Wardrobe: example

Try 1:

- stopped early: yes — No matching items were found. Try changing the description, size, or maximum price.
- selected_item: (none)
- search_results: 0

Trace:


[1] search_listings
      in:  dict with keys: description, size, max_price
      out: [] (empty)

     
Criterion 3: 
File: run_eval.py
Function: run_eval.py::main
- Query: `denim jacket under $50`
- Wardrobe: empty
**Try 1**

- stopped early: no
- selected_item: Denim Jacket — Light Wash, Cropped ($42.0, poshmark)
- search_results: 7

Outfit suggestion:


Here are two general outfit ideas for a light-wash, cropped denim jacket:

**1. The Off-Duty Model (Streetwear & Casual)**
*   **Top:** A fitted, ribbed white or grey baby tee.
*   **Bottoms:** High-waisted, wide-leg cargo pants in olive green or black to balance the cropped silhouette of the jacket.
*   **Footwear:** Chunky retro sneakers (like a vintage runner or a classic retro court shoe).
*   **Accessories:** A nylon shoulder bag and rectangular sunglasses to lean into the 90s streetwear aesthetic.

**2. The Elevated Classic (Smart Casual & Vintage-Inspired)**
*   **Top:** A sleek black bodysuit or a tucked-in black turtleneck.
*   **Bottoms:** High-waisted pleated trousers in a neutral tone like beige, camel, or houndstooth. 
*   **Footwear:** Pointed-toe black leather boots or minimalist loafers.
*   **Accessories:** A structured leather handbag and delicate gold hoop earrings to contrast the rugged texture of the denim.


Fit card:


The ultimate 90s streetwear aesthetic is calling with this light-wash cropped denim jacket! It’s a total blank canvas waiting for your custom patches and pins, giving off major off-duty model vibes when paired with cargos and chunky sneakers. Grab this vintage staple now over on my Poshmark closet for just $42!


Trace:


[1] search_listings
      in:  dict with keys: description, size, max_price
      out: 7 items: Denim Jacket — Light Wash, Cropped, Vintage Levi's 501 Jeans — Medium Wash, 90s Track Jacket — Navy/White Stripe … +4 more
[2] suggest_outfit
      in:  dict with keys: item, wardrobe
      out: Here are two general outfit ideas for a light-wash, cropped denim jacket:  **1. The Off-Duty Model (Streetwear…
[3] create_fit_card
      in:  dict with keys: outfit, item
      out: The ultimate 90s streetwear aesthetic is calling with this light-wash cropped denim jacket! It’s a total blank…

Criterion 4: 
File: run_eval.py
Function: run_eval.py::main
- Query: `floral dress under $50`
- Wardrobe: empty

**Try 1**

- stopped early: no
- selected_item: 90s Silk Slip Dress — Floral, Midi Length ($30.0, depop)
- search_results: 1

Outfit suggestion:


Here are two ways to style your new 90s floral silk slip dress using pieces already in your wardrobe:

### Outfit 1: 90s Grunge-Chic (Layered with Denim & Boots)
Lean into the authentic 90s aesthetic of the slip dress by pairing it with heavier, edgy textures to create a cool high-low contrast.
*   **New Item:** 90s Silk Slip Dress
*   **Outerwear:** Vintage black denim jacket (`w_006`)
*   **Shoes:** Black combat boots (`w_008`)
*   **Accessories:** Black crossbody bag (`w_010`)
*   *Why it works:* The delicate, feminine drape of the floral silk looks effortlessly cool when toughened up with a black denim jacket thrown over the shoulders and lace-up combat boots. 

### Outfit 2: Laid-Back Streetwear (The Slip-as-a-Skirt Look)
Transform the midi slip dress into a skirt by layering an oversized knit right over top, bridging the gap between cozy streetwear and vintage slip dress styling.
*   **New Item:** 90s Silk Slip Dress
*   **Top:** Oversized grey crewneck sweatshirt (`w_004`)
*   **Shoes:** Chunky white sneakers (`w_007`)
*   **Accessories:** Black crossbody bag (`w_010`)
*   *Why it works:* Pulling your oversized grey crewneck directly over the slip dress turns the top half into a relaxed sweater while letting the floral midi hem peek out at the bottom. Finish with chunky white sneakers for an easy, everyday errand-running outfit.


Fit card:


Channel your inner 90s icon with this dreamy floral silk slip dress, styled here with a worn-in denim jacket and combat boots for that ultimate grunge-chic contrast. It’s the ultimate throw-on-and-go piece for effortless romcom vibes all season long. Grab it on my Depop right now for just $30.00 before it’s gone!


Trace:


[1] search_listings
      in:  dict with keys: description, size, max_price
      out: 1 items: 90s Silk Slip Dress — Floral, Midi Length
[2] suggest_outfit
      in:  dict with keys: item, wardrobe
      out: Here are two ways to style your new 90s floral silk slip dress using pieces already in your wardrobe:  ### Out…
[3] create_fit_card
      in:  dict with keys: outfit, item
      out: Channel your inner 90s icon with this dreamy floral silk slip dress, styled here with a worn-in denim jacket a…

Criterion 5: 
File: run_eval.py
Function: run_eval.py::main
- Query: `floral dress under $50`
**Try 1**

- stopped early: no
- selected_item: High-Waisted Denim Shorts — Cutoff ($24.0, poshmark)
- search_results: 4

Outfit suggestion:

Here are two effortless summer outfit suggestions using your new Levi's cutoff denim shorts and pieces from your wardrobe:

### Outfit 1: Classic Casual Minimal
*A clean, breezy, everyday look that lets the vintage denim take center stage.*
* **Top:** White ribbed tank top (`w_003`)
* **Accessories:** Brown leather belt (`w_009`) threaded through the high-waisted shorts, and the Black crossbody bag (`w_010`)
* **Shoes:** Chunky white sneakers (`w_007`)
* **Why it works:** Tucking in the white ribbed tank highlights the high waist of the 501 cutoffs, while the brown belt adds a nice touch of contrast. Paired with chunky sneakers, it’s the ultimate cool-girl summer uniform for running errands or grabbing iced coffee.

### Outfit 2: Grungy Contrast (Cool Summer Nights)
*An edgy, texturally rich look that plays with proportions and contrasts.*
* **Top:** Black cropped zip hoodie (`w_005`)
* **Outerwear:** Vintage black denim jacket (`w_006`) worn over top for extra texture and warmth
* **Shoes:** Black combat boots (`w_008`)
* **Accessories:** Black crossbody bag (`w_010`)
* **Why it works:** Pairing raw-hem denim cutoffs with heavy black combat boots leans into a cool, grunge-inspired aesthetic. The cropped zip hoodie keeps the waistline defined against the high-waisted shorts, and throwing on the black denim jacket creates an effortless all-black contrast against the blue denim.


Fit card:


Nothing beats a classic pair of vintage Levi’s 501 cutoffs for effortless summer style, whether you're keeping it casual with a white tank and sneakers or leaning into an edgy grunge vibe with combat boots. These high-waisted denim shorts are the ultimate warm-weather staple and are ready for all your upcoming adventures. Grab them now for just $24.00 exclusively over on my Poshmark closet!


Trace:


[1] search_listings
      in:  dict with keys: description, size, max_price
      out: 4 items: High-Waisted Denim Shorts — Cutoff, Biker Shorts — Black, Shiny, Straight Leg Black Jeans — Faded … +1 more
[2] suggest_outfit
      in:  dict with keys: item, wardrobe
      out: Here are two effortless summer outfit suggestions using your new Levi's cutoff denim shorts and pieces from yo…
[3] create_fit_card
      in:  dict with keys: outfit, item
      out: Nothing beats a classic pair of vintage Levi’s 501 cutoffs for effortless summer style, whether you're keeping…
```

---

## Verdicts and Diagnoses

<!-- MET or MISSED per criterion against LAST UNIT's target, plus a sentence on
     how you decided.

     Then, for every miss: which of the four places it happened — a tool, the
     loop's branch, the session, or the model's output — AND the mechanism.

     Not a diagnosis:  "The fit card was bad."
     A diagnosis:      "The fit card criterion missed on 2 of 5 items. Both had
                        an empty brand field. My prompt puts the brand in the
                        first sentence, so the card opened with a blank and read
                        like a fragment. The tool worked; the prompt assumed a
                        field that isn't always there."

     Look for a pattern. Three misses on the same tool is one problem, not
     three. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Full three-tool run returns a fit card |  4 of 5  | MET | Manually verified to see if every run runs all three tools |
| 2 | Empty search stops before tool 2 | 5 of 5 | MET | Manually checked if the search stops before too2 if the search is empty |
| 3 | Item in session matches item passed on | 5 of 5 | MET | Manually verified if the same item is being passed on from one tool to another  |
| 4 | Fit card mentions the item's name and price | 4 of 5  | MET | Manually verified if the fit card as the item's name and price in it. |
| 5 | Over-budget query returns nothing over the limit | 5 of 5  | MET | Manually verified if the returned outfit or dress is with the budget limit  |

**Diagnoses**



---

## Loop Trace

<!-- One full run, printed step by step, with the MCP call visible in it.

     `python app.py ask '...' --trace` once you've added the trace.step()
     calls in Milestone 2.

     Worth pasting BOTH the happy path and the empty-search path. The empty
     one should be visibly shorter, because it stops. If your two traces are
     the same length, your branch isn't working — and this is the fastest way
     anyone will ever find that out. -->

**Happy path**

```
python app.py ask 'satin slip dress under $50' --trace
[1] search_listings
      in:  dict with keys: description, size, max_price
      out: 1 items: 90s Silk Slip Dress — Floral, Midi Length
[2] suggest_outfit
      in:  dict with keys: item, wardrobe
      out: Here are two ways to style your new 90s floral silk slip dress using pieces already in your wardrobe:  ### Out…
[3] create_fit_card
      in:  dict with keys: outfit, item
      out: Channel your inner 90s icon with this dreamy floral silk slip dress, perfect for throwing on with combat boots…

```

**Empty search**

```
python app.py ask '...' --trace
[1] search_listings
      in:  dict with keys: description, size, max_price
      out: [] (empty)

  No matching items were found. Try changing the description, size, or maximum price.
```

**On the MCP move:** <!-- what changed in your code, and whether anything behaved differently afterwards. If the rewire didn't work, say exactly where it broke — the error text and the last thing that worked. That earns the point in full. -->

I believe now it is acting like an true AI agent where it decides which tool to call based on the requirements.




---

## The Improvement

<!-- What you changed, why your diagnosis pointed at it, and the after-run in
     the same table format. One change, measured properly.

     `python run_eval.py --label after` -->

**What I changed:**

**Which failure it was meant to fix:**

### Run Log — After

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Full three-tool run returns a fit card |  4 of 5  | MET | Manually verified to see if every run runs all three tools |
| 2 | Empty search stops before tool 2 | 5 of 5 | MET | Manually checked if the search stops before too2 if the search is empty |
| 3 | Item in session matches item passed on | 5 of 5 | MET | Manually verified if the same item is being passed on from one tool to another  |
| 4 | Fit card mentions the item's name and price | 4 of 5  | MET | Manually verified if the fit card as the item's name and price in it. |
| 5 | Over-budget query returns nothing over the limit | 5 of 5  | MET | Manually verified if the returned outfit or dress is with the budget limit  |

**Did it help, and how do I know:**

<!-- If it made things worse, say that. Honestly reported, that earns full
     credit and is more interesting than one that worked. -->

It did not help, because all of my conditions are met in the intial log itself.



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped where
     you did. "I ran out of time" is fine if it's true. Pretending nothing is
     left is not. -->

I ran out of time and I still think that it's needs to be evaluated against more questions in order to find where it breaks.


<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 3

       [ ] criteria.md has five numbered criteria, each with a target
       [ ] Each criterion has a reason underneath it
       [ ] All five unit 3 sections above have real content
       [ ] Tool Inventory: all three tools, inputs WITH TYPES, a specific
           return value, and the empty case
       [ ] Planning Loop names the branch rule and agent.py::run_agent
       [ ] Sample Run: one full query plus the three per-tool tests, as text
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN, you submit the same one
           next unit

     SUBMISSION CHECKLIST — unit 4

       [ ] mcp_server.py exists with one tool registered
           (or a written record of exactly where the rewire broke)
       [ ] Run Log — Before, five criteria, five tries each
       [ ] Real output pasted underneath, naming file and function
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, naming a place AND a mechanism
       [ ] Loop Trace, with the MCP call visible in it
       [ ] All three failure modes triggered and handled
       [ ] One improvement, with Run Log — After in the same format
       [ ] What's Still Broken
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository. Your commit history is what
     shows your criteria existed before your results did.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
