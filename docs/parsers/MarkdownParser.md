---
title: Markdown Parser
author: williamabradley
description: The Markdown Parser allows you to parse a Markdown String into a Markdown Document, and then Render it with a Markdown Renderer.
keywords: windows community toolkit, uwp community toolkit, uwp toolkit, microsoft community toolkit, microsoft toolkit, markdown, markdown parsing, parser, markdown rendering
dev_langs:
  - csharp
  - vb
---

# Markdown Parser

The [MarkdownDocument](https://docs.microsoft.com/en-us/dotnet/api/microsoft.toolkit.parsers.markdown.markdowndocument) class allows you to parse a Markdown String into a Markdown Document, and then Render it with a Markdown Renderer.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=Markdown%20Parser)

## Example

```csharp
string md = "This is **Markdown**";
MarkdownDocument document = new MarkdownDocument();
document.Parse(md);

// Takes note of all of the Top Level Headers.
foreach (var element in document.Blocks)
{
    if (element is HeaderBlock header)
    {
        Console.WriteLine($"Header: {header.ToString()}");
    }
}
```
```vb
Dim md As String = "This is **Markdown**"
Dim document As MarkdownDocument = New MarkdownDocument()
document.Parse(md)

For Each element In document.Blocks
    If TypeOf element Is HeaderBlock Then
        Console.WriteLine($"Header: {element.ToString()}")
    End If
Next
End Sub
```

You can customize how blocks and inline's are parsed with the [IDocmentBuilder](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.IDocumentBuilder).
An [MarkdownInline](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Inlines.MarkdownInline) can be a link or specific format like strikethrough and is part of other inline's or blocks. A [MarkdownBlock](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock) can represent a paragraph, table or similar top-level elements. A [MarkdownDocument](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument) consist of zero, one or multiple [MarkdownBlock](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock).

A [IDocumentBuilder](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.IDocumentBuilder) can be obtained from an existing [MarkdownDocument](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument) calling the [GetBulder](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument.GetBuilder) method that contains all parsers used by the document or the static [CreateBuilder](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument.CreateBuilder) method to create a new builder without any parsers.

## Example 

```csharp
string md = "This is a link: [**Markdown**](https://de.wikipedia.org/wiki/Markdown), this not: https://de.wikipedia.org/wiki/Markdown";
var document = MarkdownDocument.CreateBuilder()
    .AddInlineParser<MarkdownLinkInline.Parser>()
    .AddInlineParser<BoldTextInline.Parser>()
        .Before<ItalicTextInline.Parser>()
    .AddInlineParser<ItalicTextInline.Parser>()
    .Build();

document.Parse(md);
```
Order the Parsers relative to each other by calling the [Before<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument.DocumentBuilder.DocumentBuilderBlockConfiguration<TParser>.Before<T>()) and [After<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument.DocumentBuilder.DocumentBuilderBlockConfiguration<TParser>.After<T>()) methods after you added an Parser. Parsers may have a default ordering. The [Before<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument.DocumentBuilder.DocumentBuilderBlockConfiguration<TParser>.Before<T>()) call can be omitted in the sample and the ordering would still not change, since Italic has a default ordering after bold.

To create a new parser, extend either [MarkdownBlock.Parser<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock.Parser<T>) or [MarkdownInline.Parser<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Inlines.MarkdownInline.Parser<T>). Then it can be added in the IDocumentBuilder.

The [ParseInternal](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock.Parser<T>.ParseInternal) method of [MarkdownBlock.Parser<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock) is called for every Line in the document as long as an previous parser did not match. The method is supplied with the text that is currently parsed. The start of the line, where the current document is parsing. The position of the first non space character and the end of the first line. In addition the maximum position until the parser should look is provided in maxEnd. If the parser can parse the current part actualEnd must point to the last character parsed by this parser.

Besides that it is also reported if the current line is a new Paragraph (the previous line was empty) and the current parsing [MarkdownDocument](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument). If your parser parses something like an underline header style a StringBuilder holding all 

By implementing a [MarkdownBlock.Parser<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock.Parser<T>) or [MarkdownInline.Parser<T>](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.Inlines.MarkdownInline.Parser<T>) custom parse logic can be added to the [MarkdownDocument](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument).

## Build in Block Parsers

Block parsers pare MarkdownBlocks.

### Paragraph

The Paragraph parser will be used if no other Parser matches.

### CodeBlock

Matches a block that starts and ends with `` ``` ``. The Text starts in the line after the prefix. The prefix may also contain a language identifier after the 3 `` ` ``.
Alternatively every line is indented by 4 space or one tab.

A code block must start as a new Paragraph.

### Header - Underlined

Matches a line of text that is followed by one or more `-` or `=` in the second line. There must be no whitespace before the characters.

 * The `=` is a first level header
 * The `-` is a second level header

### Header - Hashed

A line starting with one or more `#` will be parsed as a header.  The level of the header is defined by the number of `#` at the beginning. Following the `#` is the Text of the header.

Trailing `#` will be ignored.

### HorizontalRuler

A horizontal rule is 
 * a line with at least 3 stars, optionally separated by spaces
 * a line with at least 3 dashes, optionally separated by spaces
 * a line with at least 3 underscores, optionally separated by spaces


### LinkReference

A link reference looks like `[ID]: URL "TOOLTIP"`. `ID` can be any string that does not contain `]`. `URL` must not contain whitespaces. Existing `<` at the start and `>` at the end will be removed. `TOOLTIP` is optional. Instead of two `"` to mark the tooltip `(` and `)` or two `'` can be used. 

### List

List can be marked with `*`, `-` or `+` for unordered lists. And with a number followed by a `.` fore ordered lists. The Number for ordered lists is not used. 

### Quote

Every line of the block must start with a `>` character.

### Table

A table is a line of text, with at least one vertical bar (`|`), followed by a line of
of text that consists of alternating dashes (`-`) and vertical bars (`|`) and optionally
vertical bars at the start and end.  The second line must have at least as many
interior vertical bars as there are interior vertical bars on the first line.

### YamlHeader

The header must be at the beginning of the Text and starts `---` and ends with `---`.
The text between those markers is interpreted as YAML.

## Build in Inline Parsers

Inline parsers are used to parse text.

### Text

Every Text that is can't be parsed as another inline will be Text.

### BoldItalic

Matches a sequence of 3 `*` or `_` at the start and end of an text. Will return a `BoldTextInline` that contains a `ItalicTextInline`

### Bold

Matches a sequence of 2 `*` or `_` at the start and end of an text.

### Code
Matches one tick (`` ` ``) or two ticks at the beginning and the end of an text.
### Comment

Matches HTML comments.

### Emoji

Emojis start with a `:` followed by the name.

Following emojis will be matched:

 `:smile`, `:laughing`, `:blush`, `:smiley`, `:relaxed`, `:smirk`, `:heart_eyes`, `:kissing_heart`, `:kissing_closed_eyes`, `:flushed`, `:relieved`, `:satisfied`, `:grin`, `:wink`, `:stuck_out_tongue_winking_eye`, `:stuck_out_tongue_closed_eyes`, `:grinning`, `:kissing`, `:kissing_smiling_eyes`, `:stuck_out_tongue`, `:sleeping`, `:worried`, `:frowning`, `:anguished`, `:open_mouth`, `:grimacing`, `:confused`, `:hushed`, `:expressionless`, `:unamused`, `:sweat_smile`, `:sweat`, `:disappointed_relieved`, `:weary`, `:pensive`, `:disappointed`, `:confounded`, `:fearful`, `:cold_sweat`, `:persevere`, `:cry`, `:sob`, `:joy`, `:astonished`, `:scream`, `:tired_face`, `:angry`, `:rage`, `:triumph`, `:sleepy`, `:yum`, `:mask`, `:sunglasses`, `:dizzy_face`, `:imp`, `:smiling_imp`, `:neutral_face`, `:no_mouth`, `:innocent`, `:alien`, `:yellow_heart`, `:blue_heart`, `:purple_heart`, `:heart`, `:green_heart`, `:broken_heart`, `:heartbeat`, `:heartpulse`, `:two_hearts`, `:revolving_hearts`, `:cupid`, `:sparkling_heart`, `:sparkles`, `:star`, `:star2`, `:dizzy`, `:boom`, `:collision`, `:anger`, `:exclamation`, `:question`, `:grey_exclamation`, `:grey_question`, `:zzz`, `:dash`, `:sweat_drops`, `:notes`, `:musical_note`, `:fire`, `:hankey`, `:poop`, `:+1`, `:thumbsup`, `:-1`, `:thumbsdown`, `:ok_hand`, `:punch`, `:facepunch`, `:fist`, `:v`, `:wave`, `:hand`, `:raised_hand`, `:open_hands`, `:point_up`, `:point_down`, `:point_left`, `:point_right`, `:raised_hands`, `:pray`, `:point_up_2`, `:clap`, `:muscle`, `:metal`, `:walking`, `:runner`, `:running`, `:couple`, `:family`, `:two_men_holding_hands`, `:two_women_holding_hands`, `:dancer`, `:dancers`, `:ok_woman`, `:no_good`, `:information_desk_person`, `:raising_hand`, `:bride_with_veil`, `:person_with_pouting_face`, `:person_frowning`, `:bow`, `:couple_with_heart`, `:massage`, `:haircut`, `:nail_care`, `:boy`, `:girl`, `:woman`, `:man`, `:baby`, `:older_woman`, `:older_man`, `:person_with_blond_hair`, `:man_with_gua_pi_mao`, `:man_with_turban`, `:construction_worker`, `:cop`, `:angel`, `:princess`, `:smiley_cat`, `:smile_cat`, `:heart_eyes_cat`, `:kissing_cat`, `:smirk_cat`, `:scream_cat`, `:crying_cat_face`, `:joy_cat`, `:pouting_cat`, `:japanese_ogre`, `:japanese_goblin`, `:see_no_evil`, `:hear_no_evil`, `:speak_no_evil`, `:guardsman`, `:skull`, `:feet`, `:lips`, `:kiss`, `:droplet`, `:ear`, `:eyes`, `:nose`, `:tongue`, `:love_letter`, `:bust_in_silhouette`, `:busts_in_silhouette`, `:speech_balloon`, `:thought_balloon`, `:sunny`, `:umbrella`, `:cloud`, `:snowflake`, `:snowman`, `:zap`, `:cyclone`, `:foggy`, `:ocean`, `:cat`, `:dog`, `:mouse`, `:hamster`, `:rabbit`, `:wolf`, `:frog`, `:tiger`, `:koala`, `:bear`, `:pig`, `:pig_nose`, `:cow`, `:boar`, `:monkey_face`, `:monkey`, `:horse`, `:racehorse`, `:camel`, `:sheep`, `:elephant`, `:panda_face`, `:snake`, `:bird`, `:baby_chick`, `:hatched_chick`, `:hatching_chick`, `:chicken`, `:penguin`, `:turtle`, `:bug`, `:honeybee`, `:ant`, `:beetle`, `:snail`, `:octopus`, `:tropical_fish`, `:fish`, `:whale`, `:whale2`, `:dolphin`, `:cow2`, `:ram`, `:rat`, `:water_buffalo`, `:tiger2`, `:rabbit2`, `:dragon`, `:goat`, `:rooster`, `:dog2`, `:pig2`, `:mouse2`, `:ox`, `:dragon_face`, `:blowfish`, `:crocodile`, `:dromedary_camel`, `:leopard`, `:cat2`, `:poodle`, `:paw_prints`, `:bouquet`, `:cherry_blossom`, `:tulip`, `:four_leaf_clover`, `:rose`, `:sunflower`, `:hibiscus`, `:maple_leaf`, `:leaves`, `:fallen_leaf`, `:herb`, `:mushroom`, `:cactus`, `:palm_tree`, `:evergreen_tree`, `:deciduous_tree`, `:chestnut`, `:seedling`, `:blossom`, `:ear_of_rice`, `:shell`, `:globe_with_meridians`, `:sun_with_face`, `:full_moon_with_face`, `:new_moon_with_face`, `:new_moon`, `:waxing_crescent_moon`, `:first_quarter_moon`, `:waxing_gibbous_moon`, `:full_moon`, `:waning_gibbous_moon`, `:last_quarter_moon`, `:waning_crescent_moon`, `:last_quarter_moon_with_face`, `:first_quarter_moon_with_face`, `:moon`, `:earth_africa`, `:earth_americas`, `:earth_asia`, `:volcano`, `:milky_way`, `:partly_sunny`, `:bamboo`, `:gift_heart`, `:dolls`, `:school_satchel`, `:mortar_board`, `:flags`, `:fireworks`, `:sparkler`, `:wind_chime`, `:rice_scene`, `:jack_o_lantern`, `:ghost`, `:santa`, `:christmas_tree`, `:gift`, `:bell`, `:no_bell`, `:tanabata_tree`, `:tada`, `:confetti_ball`, `:balloon`, `:crystal_ball`, `:cd`, `:dvd`, `:floppy_disk`, `:camera`, `:video_camera`, `:movie_camera`, `:computer`, `:tv`, `:iphone`, `:phone`, `:telephone`, `:telephone_receiver`, `:pager`, `:fax`, `:minidisc`, `:vhs`, `:sound`, `:speaker`, `:mute`, `:loudspeaker`, `:mega`, `:hourglass`, `:hourglass_flowing_sand`, `:alarm_clock`, `:watch`, `:radio`, `:satellite`, `:loop`, `:mag`, `:mag_right`, `:unlock`, `:lock`, `:lock_with_ink_pen`, `:closed_lock_with_key`, `:key`, `:bulb`, `:flashlight`, `:high_brightness`, `:low_brightness`, `:electric_plug`, `:battery`, `:calling`, `:email`, `:mailbox`, `:postbox`, `:bath`, `:bathtub`, `:shower`, `:toilet`, `:wrench`, `:nut_and_bolt`, `:hammer`, `:seat`, `:moneybag`, `:yen`, `:dollar`, `:pound`, `:euro`, `:credit_card`, `:money_with_wings`, `:e-mail`, `:inbox_tray`, `:outbox_tray`, `:envelope`, `:incoming_envelope`, `:postal_horn`, `:mailbox_closed`, `:mailbox_with_mail`, `:mailbox_with_no_mail`, `:door`, `:smoking`, `:bomb`, `:gun`, `:hocho`, `:pill`, `:syringe`, `:page_facing_up`, `:page_with_curl`, `:bookmark_tabs`, `:bar_chart`, `:chart_with_upwards_trend`, `:chart_with_downwards_trend`, `:scroll`, `:clipboard`, `:calendar`, `:date`, `:card_index`, `:file_folder`, `:open_file_folder`, `:scissors`, `:pushpin`, `:paperclip`, `:black_nib`, `:pencil2`, `:straight_ruler`, `:triangular_ruler`, `:closed_book`, `:green_book`, `:blue_book`, `:orange_book`, `:notebook`, `:notebook_with_decorative_cover`, `:ledger`, `:books`, `:bookmark`, `:name_badge`, `:microscope`, `:telescope`, `:newspaper`, `:football`, `:basketball`, `:soccer`, `:baseball`, `:tennis`, `:8ball`, `:rugby_football`, `:bowling`, `:golf`, `:mountain_bicyclist`, `:bicyclist`, `:horse_racing`, `:snowboarder`, `:swimmer`, `:surfer`, `:ski`, `:spades`, `:hearts`, `:clubs`, `:diamonds`, `:gem`, `:ring`, `:trophy`, `:musical_score`, `:musical_keyboard`, `:violin`, `:space_invader`, `:video_game`, `:black_joker`, `:flower_playing_cards`, `:game_die`, `:dart`, `:mahjong`, `:clapper`, `:memo`, `:pencil`, `:book`, `:art`, `:microphone`, `:headphones`, `:trumpet`, `:saxophone`, `:guitar`, `:shoe`, `:sandal`, `:high_heel`, `:lipstick`, `:boot`, `:shirt`, `:tshirt`, `:necktie`, `:womans_clothes`, `:dress`, `:running_shirt_with_sash`, `:jeans`, `:kimono`, `:bikini`, `:ribbon`, `:tophat`, `:crown`, `:womans_hat`, `:mans_shoe`, `:closed_umbrella`, `:briefcase`, `:handbag`, `:pouch`, `:purse`, `:eyeglasses`, `:fishing_pole_and_fish`, `:coffee`, `:tea`, `:sake`, `:baby_bottle`, `:beer`, `:beers`, `:cocktail`, `:tropical_drink`, `:wine_glass`, `:fork_and_knife`, `:pizza`, `:hamburger`, `:fries`, `:poultry_leg`, `:meat_on_bone`, `:spaghetti`, `:curry`, `:fried_shrimp`, `:bento`, `:sushi`, `:fish_cake`, `:rice_ball`, `:rice_cracker`, `:rice`, `:ramen`, `:stew`, `:oden`, `:dango`, `:egg`, `:bread`, `:doughnut`, `:custard`, `:icecream`, `:ice_cream`, `:shaved_ice`, `:birthday`, `:cake`, `:cookie`, `:chocolate_bar`, `:candy`, `:lollipop`, `:honey_pot`, `:apple`, `:green_apple`, `:tangerine`, `:lemon`, `:cherries`, `:grapes`, `:watermelon`, `:strawberry`, `:peach`, `:melon`, `:banana`, `:pear`, `:pineapple`, `:sweet_potato`, `:eggplant`, `:tomato`, `:corn`, `:house`, `:house_with_garden`, `:school`, `:office`, `:post_office`, `:hospital`, `:bank`, `:convenience_store`, `:love_hotel`, `:hotel`, `:wedding`, `:church`, `:department_store`, `:european_post_office`, `:city_sunrise`, `:city_sunset`, `:japanese_castle`, `:european_castle`, `:tent`, `:factory`, `:tokyo_tower`, `:japan`, `:mount_fuji`, `:sunrise_over_mountains`, `:sunrise`, `:stars`, `:statue_of_liberty`, `:bridge_at_night`, `:carousel_horse`, `:rainbow`, `:ferris_wheel`, `:fountain`, `:roller_coaster`, `:ship`, `:speedboat`, `:boat`, `:sailboat`, `:rowboat`, `:anchor`, `:rocket`, `:airplane`, `:helicopter`, `:steam_locomotive`, `:tram`, `:mountain_railway`, `:bike`, `:aerial_tramway`, `:suspension_railway`, `:mountain_cableway`, `:tractor`, `:blue_car`, `:oncoming_automobile`, `:car`, `:red_car`, `:taxi`, `:oncoming_taxi`, `:articulated_lorry`, `:bus`, `:oncoming_bus`, `:rotating_light`, `:police_car`, `:oncoming_police_car`, `:fire_engine`, `:ambulance`, `:minibus`, `:truck`, `:train`, `:station`, `:train2`, `:bullettrain_front`, `:bullettrain_side`, `:light_rail`, `:monorail`, `:railway_car`, `:trolleybus`, `:ticket`, `:fuelpump`, `:vertical_traffic_light`, `:traffic_light`, `:warning`, `:construction`, `:beginner`, `:atm`, `:slot_machine`, `:busstop`, `:barber`, `:hotsprings`, `:checkered_flag`, `:crossed_flags`, `:izakaya_lantern`, `:moyai`, `:circus_tent`, `:performing_arts`, `:round_pushpin`, `:triangular_flag_on_post`, `:keycap_ten`, `:1234`, `:symbols`, `:arrow_backward`, `:arrow_down`, `:arrow_forward`, `:arrow_left`, `:capital_abcd`, `:abcd`, `:abc`, `:arrow_lower_left`, `:arrow_lower_right`, `:arrow_right`, `:arrow_up`, `:arrow_upper_left`, `:arrow_upper_right`, `:arrow_double_down`, `:arrow_double_up`, `:arrow_down_small`, `:arrow_heading_down`, `:arrow_heading_up`, `:leftwards_arrow_with_hook`, `:arrow_right_hook`, `:left_right_arrow`, `:arrow_up_down`, `:arrow_up_small`, `:arrows_clockwise`, `:arrows_counterclockwise`, `:rewind`, `:fast_forward`, `:information_source`, `:ok`, `:twisted_rightwards_arrows`, `:repeat`, `:repeat_one`, `:new`, `:top`, `:up`, `:cool`, `:free`, `:ng`, `:cinema`, `:koko`, `:signal_strength`, `:u5272`, `:u5408`, `:u55b6`, `:u6307`, `:u6708`, `:u6709`, `:u6e80`, `:u7121`, `:u7533`, `:u7a7a`, `:u7981`, `:sa`, `:restroom`, `:mens`, `:womens`, `:baby_symbol`, `:no_smoking`, `:parking`, `:wheelchair`, `:metro`, `:baggage_claim`, `:accept`, `:wc`, `:potable_water`, `:put_litter_in_its_place`, `:secret`, `:congratulations`, `:m`, `:passport_control`, `:left_luggage`, `:customs`, `:ideograph_advantage`, `:cl`, `:sos`, `:id`, `:no_entry_sign`, `:underage`, `:no_mobile_phones`, `:do_not_litter`, `:non-potable_water`, `:no_bicycles`, `:no_pedestrians`, `:children_crossing`, `:no_entry`, `:eight_spoked_asterisk`, `:eight_pointed_black_star`, `:heart_decoration`, `:vs`, `:vibration_mode`, `:mobile_phone_off`, `:chart`, `:currency_exchange`, `:aries`, `:taurus`, `:gemini`, `:cancer`, `:leo`, `:virgo`, `:libra`, `:scorpius`, `:sagittarius`, `:capricorn`, `:aquarius`, `:pisces`, `:ophiuchus`, `:six_pointed_star`, `:negative_squared_cross_mark`, `:a`, `:b`, `:ab`, `:o2`, `:diamond_shape_with_a_dot_inside`, `:recycle`, `:end`, `:on`, `:soon`, `:clock1`, `:clock130`, `:clock10`, `:clock1030`, `:clock11`, `:clock1130`, `:clock12`, `:clock1230`, `:clock2`, `:clock230`, `:clock3`, `:clock330`, `:clock4`, `:clock430`, `:clock5`, `:clock530`, `:clock6`, `:clock630`, `:clock7`, `:clock730`, `:clock8`, `:clock830`, `:clock9`, `:clock930`, `:heavy_dollar_sign`, `:copyright`, `:registered`, `:tm`, `:x`, `:heavy_exclamation_mark`, `:bangbang`, `:interrobang`, `:o`, `:heavy_multiplication_x`, `:heavy_plus_sign`, `:heavy_minus_sign`, `:heavy_division_sign`, `:white_flower`, `:100`, `:heavy_check_mark`, `:ballot_box_with_check`, `:radio_button`, `:link`, `:curly_loop`, `:wavy_dash`, `:part_alternation_mark`, `:trident`, `:white_check_mark`, `:black_square_button`, `:white_square_button`, `:black_circle`, `:white_circle`, `:red_circle`, `:large_blue_circle`, `:large_blue_diamond`, `:large_orange_diamond`, `:small_blue_diamond`, `:small_orange_diamond`, `:small_red_triangle`, `:small_red_triangle_down`

### Hyperlink - Angle Bracket

Attempts to parse a URL within angle brackets e.g. `<http://www.reddit.com>`.

### Hyperlink - Url

Attempts to parse a URL that starts with a known scheme.

Known Schemes are:

* http
* https
* ftp
* steam
* irc
* news
* mumble
* ssh
* ms-windows-store
* sip

### Hyperlink - Redit

Parses a redit link that either starts with `/r/` for subreddit or `/u/` for user followed by the name of the subredit or user. A user name must have at least one character, a subreddit two.
The type will be set in LinkType.

### Hyperlink - PartialLink

Trys to parse links that don't have a scheme  e.g. `www.reddit.com`.

The link must start with `www`. The url that will be created will use the `http` schema.

### Hyperlink - EMail

Attempts to parse email addresses. It will look for `@` in the text.

### Image

Parses Images in the format `![ALT_TEXT](RESOURCE_URL)`.

### Italic

Matches a sequence of one `*` or `_` at the start and end of an text.

### LinkAnchor

Parses a link in the form of `<a name="URL" />`.

### MarkdownLink

Attempts to parse a markdown link e.g. `[Text](http://www.reddit.com)`. The `Text` will also be parsed as inline but will ignore other HyperLinks.

### Strikethrough

Matches a sequence of two `~` at the start and end of an text.

### Subscript

Attempts to parse a subscript text span in the form of `<sub>TEXT</sub>`.

### Superscript

Attempts to parse a superscript text span in the form of `<sup>TEXT</sup>` or `^TEXT`.


## Classes

| Class | Purpose |
| --- | --- |
| **Microsoft.Toolkit.Parsers.Markdown.MarkdownDocument** | Represents a Markdown Document. |
| **Microsoft.Toolkit.Parsers.Markdown.IDocumentBuilder** | To configure how documents are parsed. |
| **Microsoft.Toolkit.Parsers.Markdown.Blocks.MarkdownBlock.Parser\<T\>** | Base class for all block parsers. |
| **Microsoft.Toolkit.Parsers.Markdown.Inlines.MarkdownInline.Parser\<T\>** | Base class for all inline parsers. |
| **Microsoft.Toolkit.Parsers.Markdown.Render.MarkdownRendererBase** | A base renderer for Rendering Markdown into Controls. |

### MarkdownDocument

#### Properties

| Property | Type | Description |
| -- | -- | -- |
| Blocks | IList\<MarkdownBlock\> | Gets or sets the list of block elements. |

#### Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| static CreateBuilder() | IDocumentBuilder | Creates a new Builder. |
| Parse(string) | void | Parses markdown document text. |
| LookUpReference(string) | LinkReferenceBlock | Looks up a reference using the ID. |

### MarkdownBlock.Parser\<TBlock\>


#### Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| ParseInternal(string, int, int, int, int, out int, StringBuilder, bool,  MarkdownDocument) | TBlock | Parses inline text. |

### MarkdownInline.Parser\<TInline\>


#### Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| ParseInternal(string, int, int, int, MarkdownDocument, IEnumerable\<Type\>) | InlineParseResult\<TInline\> | Parses inline text. |



## Create a Markdown Renderer

In order to create a Markdown Renderer, you can either implement your own, or inherit from `MarkdownRenderBase`, this class already has all the required methods, and some assistive code to make implementing a Renderer easy, all you have to do is implement the Block and Inline Rendering, and the output.

This requires an inherited `IRenderContext`, which allows you to keep track of the Context of the rendering.

The best way to figure out how to create a Renderer, is to look at the [implementation](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.UI.Controls/MarkdownTextBlock/Render) for the UWP MarkdownTextBlock control.

## Sample Project

[Markdown Parser Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/MarkdownParser/MarkdownParserPage.xaml.cs). You can [see this in action](uwpct://Helpers?sample=Markdown%20Parser) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Implementation | .NET Standard 1.4. |
| -- | -- |
| Namespace | Microsoft.Toolkit.Parsers |
| NuGet package | [Microsoft.Toolkit.Parsers](https://www.nuget.org/packages/Microsoft.Toolkit.Parsers/)  |

## API

* [Markdown Parser source code](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Parsers/Markdown)
