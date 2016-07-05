## get_iplayer Metadata Tagging

## Usage

### Options

|Command&#160;Line|Option&#160;File|Description
|-----------------|----------------|-----------
|`--no-artwork`|noartwork&#160;(0/1)|Do not embed thumbnail image in output file.  All other metadata values will be written.
|`--no-tag`|notag&#160;(0/1)|Do not tag downloaded programmes
|`--tag-cnid` **[DEPRECATED]**|tag_cnid&#160;(0/1)|Use AtomicParsley `--cnID` option (if supported) to add catalog ID used for combining HD and SD versions in iTunes
|`--tag-format-show`|tag_formatshow (string)|Format template for programme name in metadata (use [substitution parameters](/wiki/documentation#substitution-parameters)). Default: none
|`--tag-format-title`|tag_formattitle (string)|Format template for episode title in metadata (use [substitution parameters](/wiki/documentation#substitution-parameters)). Default: none
|`--tag-fulltitle` **[DEPRECATED]**|tag_fulltitle&#160;(0/1)|Use complete title (including series) instead of shorter episode title
|`--tag-hdvideo` **[DEPRECATED]**|tag_hdvideo&#160;(0/1)|AtomicParsley accepts `--hdvideo` option for HD video flag
|`--tag-id3sync` **[DEPRECATED]**|tag_id3sync&#160;(0/1)|Save ID3 tags for MP3 files in synchronised form. Provides workaround for corruption of thumbnail images in Windows. Has no effect unless using MP3::Tag Perl module.
|`--tag-isodate`|tag_isodate&#160;(0/1)|Use ISO8601 dates (YYYY-MM-DD) in album/show names and track title
|`--tag-longdesc` **[DEPRECATED]**|tag_longdesc&#160;(0/1)|AtomicParsley accepts `--longdesc` option for long description text
|`--tag-longdescription` **[DEPRECATED]**|tag_longdescription&#160;(0/1)|AtomicParsley accepts `--longDescription` option for long description text
|`--tag-longepisode` **[DEPRECATED]**|tag_longepisode&#160;(0/1)|Use `<episode>` instead of `<episodeshort>` for track title
|`--tag-longtitle` **[DEPRECATED]**|tag_longtitle&#160;(0/1)|Prepend `<series>` (if available) to track title. Ignored with --tag-fulltitle.
|`--tag-podcast`|tag_podcast&#160;(0/1)|Tag downloaded radio and tv programmes as iTunes podcasts
|`--tag-podcast-radio`|tag_podcast_radio&#160;(0/1)|Tag only downloaded radio programmes as iTunes podcasts
|`--tag-podcast-tv`|tag_podcast_tv&#160;(0/1)|Tag only downloaded tv programmes as iTunes podcasts
|`--tag-shortname` **[DEPRECATED]**|tag_shortname&#160;(0/1)|Use `<nameshort>` instead of `<name>` for album/show title
|`--tag-utf8`|tag_utf8&#160;(0/1)|Use UTF-8 encoding for non-ASCII characters in AtomicParsley parameter values (Linux/Unix/OS X only). Use only if auto-detect fails.

#### AtomicParsley Variants

The options related to AtomicParsley are provided to support variations in different versions that emerged after primary development ceased at version 0.9.0.

#### Content Encoding

The get_iplayer metadata is assumed to be encoded as UTF-8 and is then re-encoded as necessary for the different tagging applications.  This doesn't always hold true, so substitution characters may sometimes appear in the tags, particularly _lyrics_ or _longDescription_.

## Tag Scheme

The table below describes the scheme used to convert get_iplayer metadata into tags for downloaded programmes.  The tag names were selected to match AtomicParsley parameter names.  Each tag is mapped, where possible, to the corresponding get_iplayer substitution parameter, AtomicParsley arg, MP4 atom, id3v2 param, and ID3 frame.  The list of iTunes fields indicate where each tag will appear in the iTunes *Get Info* dialog.  Conversion rules specific to particular fields are indicated in the footnotes.  If you wish to experiment with variations, the conversion of get_iplayer metadata to tag values is encapsulated in the *Tagger::tags_from_metadata* subroutine.

|Tag&#160;Name|Substitution&#160;Param<sup>1</sup>|AtomicParsley&#160;arg|MP4 atom|id3v2 Param |ID3 Frame|iTunes Field
|-----|-----|-----|-----|-----|-----|-----
|stik<sup>2</sup>|`<ext>`|`--stik`|stik|||Options:Media&#160;Kind
|advisory<sup>3</sup>|`<guidance>`|`--advisory`|rtng|||Summary:Advisory
|copyright<sup>4</sup>|`<dldate>`|`--copyright`|cprt|``--TCOP``|TCOP|Summary:Copyright
|title|`<episode>`<sup>5</sup>|`--title`|©nam|`--TIT2`|TIT2|Info:Name
|artist|`<channel>`|`--artist`|©ART|`--TPE1`|TPE1|Info:Artist
|albumArtist|BBC `<type>`<sup>6</sup>|`--albumArtist`|aART|`--TPE2`|TPE2|Info:Album&#160;Artist
|album|`<name>`|`--album`|©alb|`--TALB`|TALB|Info:Album
|grouping|`<categories>`|`--grouping`|©grp|`--TIT1`|TIT1|Info:Grouping
|composer|BBC iPlayer|`--composer`|©wrt|`--TCOM`|TCOM|Info:Composer
|comment|`<descshort>`|`--comment`|©cmt|`--COMM`|COMM|Info:Comments
|genre<sup>7</sup>|`<categories>`|`--genre`|©gen|`--TCON`|TCON|Info:Genre
|year|`<firstbcast>`<sup>8</sup>|`--year`|©day|`--TYER`|TYER|Info:Year
|tracknum|`<episodenum>`|`--tracknum`|trkn|`--TRCK`|TRCK|Info:Track&#160;Number
|disk|`<seriesnum>`|`--disk`|disk|`--TPOS`|TPOS|Info:Disc&#160;Number
|lyrics|`<desc>`<sup>9</sup>|`--lyrics`|©lyr|`--USLT`|USLT|Lyrics
|description|`<descshort>`|`--description`|desc||TIT3<sup>15</sup>|Video:Description
|longDescription|`<desc>`|`--longdesc`<sup>10</sup>&#160;*OR*<br/>`--longDescription`<sup>11</sup>|ldes||TDES<sup>15</sup>|(Hidden):Long&#160;Description
|hdvideo<sup>12</sup>|`<mode>`|`--hdvideo`<sup>13</sup>|hdvd|||(Browser):HD&#160;Icon
|TVShowName|`<name>`|`--TVShowName`|tvsh|||Video:Show
|TVEpisode|`<senum>`<sup>14</sup>|`--TVEpisode`|tven|||Video:Episode&#160;ID
|TVSeasonNum|`<seriesnum>`|`--TVSeasonNum`|tvsh|||Video:Season&#160;Number
|TVEpisodeNum|`<episodenum>`|`--TVEpisodeNum`|tves|||Video:Episode&#160;Number
|TVNetwork|`<channel>`|`--TVNetwork`|tvnn|||(Hidden):TV&#160;Network
|artwork|`<thumbfile>`|`--artwork`|covr||APIC|Artwork
|podcastFlag<sup>15</sup>|true|`--podcastFlag`|pcst||PCST|Options:Media&#160;Kind
|category<sup>15</sup>|`<categories>`<sup>16</sup>|`--category`|catg||TCAT|(Hidden):Podcast&#160;Category
|keyword<sup>15</sup>|`<categories>`|`--keyword`|keyw||TKWD|(Hidden):Podcast&#160;Keywords
|podcastGUID<sup>15</sup>|`<player>`|`--podcastGUID`|egid||TGID|(Hidden):Podcast&#160;GUID
|||||`--TDAT`|TDAT<sup>17</sup>|---
|||||`--TIME`|TIME<sup>17</sup>|---
||||||TDRL<sup>18</sup>|---

1. Full list of substitution parameters may be found [here](/wiki/documentation#substitution-parameters).

2. *TV Show* if MP4/M4V, *Movie* if MP4/M4V and `<categories>` contains "Film", *Normal* otherwise

3. *explicit* if `<guidance>` non-empty, *remove* otherwise

4. Year taken from `<dldate>`, e.g.: (C) 2011 British Broadcasting Corporation, all rights reserved

5. `<title>` used if `--tag-fulltitle` given

6. *BBC TV*, *BBC Radio*, *BBC Podcast*

7. First item in `<categories>` used unless it is one of: ("Films", "Sign Zone", "Audio Described", "Northern Ireland", "Scotland", "Wales", "England"), in which case second item is used.  If `<categories>` is empty, set to *get_iplayer*

8. If `<firstbcast>` is not valid date, current date is used

9. `<player>` and `<web>` appended if present

10. `--tag-longdesc` required for compatible AtomicParsley version

11. `--tag-longdescription` required for compatible AtomicParsley version

12. *true* if `<mode>` contains "hd", *false* otherwise

13. `--tag-hdvideo` required for compatible AtomicParsley version

14. If `<senum>` empty, `<pid>` is used

15. `--tag-podcast` required if `<type>` != "podcast"

16. Uses same rules as genre [6]

17. Used with `TYER` to record full date

18. Podcast release date for iTunes
